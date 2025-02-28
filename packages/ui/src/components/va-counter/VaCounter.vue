<template>
  <va-input-wrapper
    class="va-counter"
    v-bind="{ ...fieldListeners, ...inputWrapperPropsComputed }"
    :class="classComputed"
    :style="styleComputed"
    :focused="isFocused"
    @keydown.up.prevent="increaseCount"
    @keydown.down.prevent="decreaseCount"
  >
    <template v-if="$props.buttons" #prepend="slotScope">
      <div class="va-counter__prepend-wrapper"
        :style="{ marginRight: marginComputed }"
        @mousedown.prevent="focus"
      >
        <slot name="decreaseAction" v-bind="{ ...slotScope, decreaseCount }">
          <va-button
            class="va-counter__button-decrease"
            :aria-label="t('decreaseCounter')"
            v-bind="decreaseButtonProps"
            @click="decreaseCount"
          />
        </slot>
      </div>
    </template>

    <template v-else #prependInner="slotScope">
      <div @mousedown.prevent="focus" class="va-counter__prepend-inner">
        <slot name="decreaseAction" v-bind="{ ...slotScope, decreaseCount }">
          <va-button v-bind="decreaseIconProps" />
        </slot>
      </div>
    </template>

    <template v-if="$props.buttons"  #append="slotScope">
      <div class="va-counter__append-wrapper"
        :style="{ marginLeft: marginComputed }"
        @mousedown.prevent="focus"
      >
        <slot name="increaseAction" v-bind="{ ...slotScope, increaseCount }">
          <va-button
            class="va-counter__button-increase"
            :aria-label="t('increaseCounter')"
            v-bind="increaseButtonProps"
            @click="increaseCount"
          />
        </slot>
      </div>
    </template>

    <template v-else #appendInner="slotScope">
      <div @mousedown.prevent="focus" class="va-counter__append-inner">
        <slot name="increaseAction" v-bind="{ ...slotScope, increaseCount }">
          <va-button v-bind="increaseIconProps" />
        </slot>
      </div>
    </template>

    <template v-if="$slots.content" #default="slotScope">
      <div
        ref="input"
        tabindex="0"
        class="va-counter__content-wrapper"
      >
        <slot name="content" v-bind="{ ...slotScope, value: Number(valueComputed) }" />
      </div>
    </template>

    <input
      v-if="!$slots.content"
      ref="input"
      class="va-input__content__input"
      type="number"
      inputmode="decimal"
      v-bind="{ ...inputAttributesComputed, ...inputListeners }"
      :value="valueComputed"
      @input="setCountInput"
      @change="setCountChange"
    >
  </va-input-wrapper>
</template>

<script lang="ts">
import {
  toRefs,
  computed,
  shallowRef,
  defineComponent,
  InputHTMLAttributes,
  PropType,
  ComputedRef,
} from 'vue'
import omit from 'lodash/omit'
import pick from 'lodash/pick'

import { safeCSSLength } from '../../utils/css'
import {
  useComponentPresetProp,
  useFormProps,
  useEmitProxy,
  useFocus, useFocusEmits,
  useStateful, useStatefulProps,
  useColors,
  useTranslation,
} from '../../composables'
import useCounterPropsValidation from './hooks/useCounterPropsValidation'

import { VaInputWrapper } from '../va-input'
import VaButton from '../va-button/VaButton.vue'

const { createEmits: createInputEmits, createListeners: createInputListeners } = useEmitProxy(
  ['change'],
)

const { createEmits: createFieldEmits, createListeners: createFieldListeners } = useEmitProxy([
  { listen: 'click-prepend', emit: 'click:decrease-button' },
  { listen: 'click-append', emit: 'click:increase-button' },
  { listen: 'click-prepend-inner', emit: 'click:decrease-icon' },
  { listen: 'click-append-inner', emit: 'click:increase-icon' },
])

export default defineComponent({
  name: 'VaCounter',

  components: { VaInputWrapper, VaButton },

  props: {
    ...useFormProps,
    ...useStatefulProps,
    ...useComponentPresetProp,
    // input
    modelValue: { type: [String, Number], default: 0 },
    manualInput: { type: Boolean, default: false },
    stateful: { type: Boolean, default: false },
    min: { type: Number, default: undefined },
    max: { type: Number, default: undefined },
    step: { type: Number, default: 1 },
    label: { type: String, default: '' },
    // hint
    messages: { type: [Array, String] as PropType<string[] | string>, default: () => [] },
    // style
    width: { type: [String, Number], default: '160px' },
    color: { type: String, default: 'primary' },
    outline: { type: Boolean },
    bordered: { type: Boolean },
    // icons & buttons
    increaseIcon: { type: String, default: 'add' },
    decreaseIcon: { type: String, default: 'remove' },
    buttons: { type: Boolean, default: false },
    flat: { type: Boolean, default: true },
    rounded: { type: Boolean, default: false },
    margins: { type: [String, Number], default: '4px' },
    textColor: { type: String, default: undefined },
  },

  emits: [
    'update:modelValue',
    ...createInputEmits(),
    ...createFieldEmits(),
    ...useFocusEmits,
  ],

  inheritAttrs: false,

  setup (props, { emit, attrs }) {
    const input = shallowRef<HTMLInputElement | HTMLDivElement>()
    const { min, max, step } = toRefs(props)

    const {
      isFocused,
      focus,
      blur,
    } = useFocus(input, emit)

    const { valueComputed } = useStateful(props, emit)

    const setCountInput = ({ target }: Event) => {
      valueComputed.value = Number((target as HTMLInputElement | null)?.value)
    }

    const setCountChange = ({ target } : Event) => {
      calculateCounterValue(Number((target as HTMLInputElement | null)?.value))
    }

    const getRoundDownWithStep = (value: number) => {
      if (typeof min.value === 'undefined' || !step.value) { return value }

      // If the user enters a value manually, then we must round it to the nearest valid value,
      // taking into account the initial value (`props.min`) and the step size (`props.step`)
      return min.value + step.value * Math.floor((value - min.value) / step.value)
    }

    const calculateCounterValue = (counterValue: number) => {
      if (typeof min.value !== 'undefined' && counterValue < min.value) {
        valueComputed.value = min.value
        return
      }

      if (max.value && (counterValue > max.value)) {
        // since the `props.step` may not be a multiple of `(props.max - props.min)`,
        // we must round the result taking into account the allowable value
        valueComputed.value = (typeof min.value !== 'undefined' && step.value)
          ? getRoundDownWithStep(max.value)
          : max.value

        return
      }

      valueComputed.value = getRoundDownWithStep(counterValue)
    }

    const isMinReached = computed(() => {
      if (typeof min.value === 'undefined') { return false }

      return Number(valueComputed.value) <= min.value
    })

    const isMaxReached = computed(() => {
      if (!max.value) { return false }

      return step.value
        ? Number(valueComputed.value) > (max.value - step.value)
        : Number(valueComputed.value) >= max.value
    })

    const tabIndexComputed = computed(() => props.disabled ? -1 : 0)

    const isDecreaseActionDisabled = computed(() => (
      isMinReached.value || props.readonly || props.disabled
    ))

    const isIncreaseActionDisabled = computed(() => (
      isMaxReached.value || props.readonly || props.disabled
    ))

    const decreaseCount = () => {
      if (isDecreaseActionDisabled.value) { return }
      calculateCounterValue(Number(valueComputed.value) - step.value)
    }

    const increaseCount = () => {
      if (isIncreaseActionDisabled.value) { return }
      calculateCounterValue(Number(valueComputed.value) + step.value)
    }

    const { getColor } = useColors()
    const colorComputed = computed(() => getColor(props.color))

    const decreaseIconProps = computed(() => ({
      class: { 'va-counter__icon--inactive': isDecreaseActionDisabled.value },
      color: colorComputed.value,
      icon: props.decreaseIcon,
      plain: true,
      disabled: isDecreaseActionDisabled.value,
      tabindex: -1,
      ...(!isDecreaseActionDisabled.value && { onClick: decreaseCount }),
    }))

    const increaseIconProps = computed(() => ({
      class: { 'va-counter__icon--inactive': isIncreaseActionDisabled.value },
      color: colorComputed.value,
      icon: props.increaseIcon,
      plain: true,
      disabled: isIncreaseActionDisabled.value,
      tabindex: -1,
      ...(!isIncreaseActionDisabled.value && { onClick: increaseCount }),
    }))

    const isSquareCorners = computed(() => (
      (typeof props.margins === 'string' ? parseFloat(props.margins) : props.margins) === 0
    ))

    const buttonProps = computed(() => ({
      ...pick(props, ['rounded', 'color', 'textColor']),
      flat: props.flat && !props.outline,
      outline: props.flat && props.outline,
    }))

    const decreaseButtonProps = computed(() => ({
      ...buttonProps.value,
      icon: props.decreaseIcon,
      disabled: isDecreaseActionDisabled.value,
    }))

    const increaseButtonProps = computed(() => ({
      ...buttonProps.value,
      icon: props.increaseIcon,
      disabled: isIncreaseActionDisabled.value,
    }))

    const { t } = useTranslation()

    const inputAttributesComputed = computed(() => ({
      tabindex: tabIndexComputed.value,
      'aria-label': props.label || t('counterValue'),
      'aria-valuemin': min.value,
      'aria-valuemax': max.value,
      ...omit(attrs, ['class', 'style']),
      ...pick(props, ['disabled', 'min', 'max', 'step']),
      readonly: props.readonly || !props.manualInput,
    }) as InputHTMLAttributes)

    const inputWrapperPropsComputed = computed(() => ({
      ...pick(props, ['color', 'readonly', 'disabled', 'messages', 'label', 'bordered', 'outline']),
    }))

    const classComputed = computed(() => ([
      attrs.class,
      { 'va-counter--input-square': isSquareCorners.value },
    ]))

    const styleComputed: ComputedRef<Partial<CSSStyleDeclaration>> = computed(() => ({
      width: safeCSSLength(props.width),
      ...((attrs.style as Partial<CSSStyleDeclaration>) || {}),
    }))

    const marginComputed = computed(() => safeCSSLength(props.margins))

    useCounterPropsValidation(props)

    return {
      ...useTranslation(),
      input,
      valueComputed,
      isFocused,

      fieldListeners: createFieldListeners(emit),
      inputListeners: createInputListeners(emit),
      inputAttributesComputed,
      inputWrapperPropsComputed,
      setCountInput,
      setCountChange,

      decreaseCount,
      increaseCount,

      decreaseIconProps,
      increaseIconProps,
      decreaseButtonProps,
      increaseButtonProps,

      colorComputed,
      classComputed,
      styleComputed,
      marginComputed,

      focus,
      blur,
    }
  },
})
</script>

<style lang="scss">
@import "variables";

.va-counter {
  --va-input-wrapper-min-width: none;

  &.va-counter--input-square {
    .va-input__container {
      border-radius: 0;
      border-left: none;
      border-right: none;
    }

    .va-counter__prepend-wrapper {
      .va-counter__button-decrease {
        border-top-right-radius: 0;
        border-bottom-right-radius: 0;
      }

      .va-counter__button-decrease:not(.va-button--square) {
        width: unset;

        .va-button__content {
          padding-right: var(--va-counter-button-inner-padding);
          padding-left: var(--va-counter-button-outer-padding);
        }
      }
    }

    .va-counter__append-wrapper {
      .va-counter__button-increase {
        border-top-left-radius: 0;
        border-bottom-left-radius: 0;
      }

      .va-counter__button-increase:not(.va-button--square) {
        width: unset;

        .va-button__content {
          padding-left: var(--va-counter-button-inner-padding);
          padding-right: var(--va-counter-button-outer-padding);
        }
      }
    }
  }

  &:not(.va-counter--input-square) {
    .va-counter__prepend-wrapper,
    .va-counter__append-wrapper {
      .va-counter__button-decrease,
      .va-counter__button-increase {
        .va-button__content {
          padding: unset;
        }
      }
    }
  }

  .va-counter__content-wrapper {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  .va-input__content__input {
    text-align: center;

    // Chrome, Safari, Edge, Opera
    &::-webkit-outer-spin-button,
    &::-webkit-inner-spin-button {
      -webkit-appearance: none;
      margin: 0;
    }
    // Firefox
    &[type=number] {
      -moz-appearance: textfield;
    }
  }

  .va-input-wrapper__field {
    align-items: stretch;
    padding: 0;

    .va-input-wrapper__text,
    .va-input__container {
      padding-right: 0;
    }
  }

  &__prepend-inner,
  &__append-inner {
    display: flex;
    align-items: stretch;
    height: 100%;
  }
}
</style>
