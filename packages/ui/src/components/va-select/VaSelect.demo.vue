<template>
  <VbDemo>
    <VbCard
      title="Basic usage"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        :options="defaultSingleSelect.options"
      />
      <p>Value: {{ defaultSingleSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Autocomplete"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        :options="defaultSingleSelect.options"
        autocomplete
      />
      <p>Value: {{ defaultSingleSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Multiple autocomplete"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        :options="defaultMultiSelect.options"
        multiple
        autocomplete
      />
      <p>Value: {{ defaultMultiSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Multiple autocomplete with max visible options"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        :options="defaultMultiSelect.options"
        :max-visible-options="2"
        multiple
        autocomplete
      />
      <p>Value: {{ defaultMultiSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Autocomplete with create new option"
      style="width: 400px;"
    >
      <va-select
        v-model="allowCreateSelect.value"
        class="mb-6"
        :options="allowCreateSelect.options"
        autocomplete
        allow-create
        @create-new="addNewOption"
      />
      <p>Value: {{ allowCreateSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Multiple autocomplete with content slot"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        :options="defaultMultiSelect.options"
        multiple
        autocomplete
      >
        <template #content="{ value }">
          <va-chip
            v-for="chip in value"
            :key="chip"
            class="mr-1"
            size="small"
          >
            {{ chip }}
          </va-chip>
        </template>
      </va-select>
      <p>Value: {{ defaultMultiSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Min chars (2) to trigger autocomplete"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        :options="defaultSingleSelect.options"
        :min-search-chars="2"
        autocomplete
      />
      <p>Value: {{ defaultSingleSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Selected options at the top"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-4"
        :options="defaultMultiSelect.options"
        selected-top-shown
        multiple
      />
      <p>Value: {{ defaultMultiSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Max visible options"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-4"
        :options="defaultMultiSelect.options"
        :max-visible-options="2"
        multiple
      />
      <p>Value: {{ defaultMultiSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Max visible options with content slot"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-4"
        :options="defaultMultiSelect.options"
        :max-visible-options="2"
        multiple
      >
        <template #content="{ value }">
          <va-chip
            v-for="chip in value"
            :key="chip"
            class="mr-1"
            size="small"
          >
            {{ chip }}
          </va-chip>
        </template>
      </va-select>
      <p>Value: {{ defaultMultiSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Disabled options"
      style="width: 400px;"
    >
      <va-select
        v-model="disabledOptions.value"
        class="mb-6"
        :options="disabledOptions.options"
      />
      <p>Value: {{ disabledOptions.value }}</p>
    </VbCard>
    <VbCard
      title="Option slot"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        :options="defaultSingleSelect.options"
      >
        <template v-slot:option="{ option, index, selectOption }">
          <div
            class="mb-2"
            @click="selectOption(option)"
          >
            option {{ option }} with index {{ index }}
          </div>
        </template>
      </va-select>
      <p>Value: {{ defaultSingleSelect.value }}</p>
    </VbCard>
    <VbCard
      title="Virtual Scroller"
      style="width: 400px;"
    >
      <va-select
        v-model="withVirtualScroller.value"
        class="mb-6"
        :options="withVirtualScroller.options"
        virtual-scroller
      />
      <p>Value: {{ withVirtualScroller.value }}</p>
    </VbCard>
    <VbCard
      title="Style"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Default (solid)"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Outline"
        :options="defaultSingleSelect.options"
        outline
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Bordered"
        :options="defaultSingleSelect.options"
        bordered
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Default (solid) (Purple color)"
        color="#990099"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Outline (Purple color)"
        :options="defaultSingleSelect.options"
        color="#990099"
        outline
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Bordered (Purple color)"
        :options="defaultSingleSelect.options"
        color="#990099"
        bordered
      />
    </VbCard>
    <VbCard
      title="Single select"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Default"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Default, hide selected"
        :options="defaultSingleSelect.options"
        hide-selected
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="No options"
        :options="[]"
      />
    </VbCard>
    <VbCard title="html select for example">
      <select>
        <option value="one">one</option>
        <option value="two">two</option>
        <option value="three">three</option>
      </select>
    </VbCard>
    <VbCard
      title="Multi select"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        label="Default"
        :options="defaultMultiSelect.options"
        multiple
      />
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        label="Default, hide selected"
        :options="defaultMultiSelect.options"
        multiple
        hide-selected
      />
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        label="Max selections (3)"
        :options="defaultMultiSelect.options"
        multiple
        :max-selections="3"
      />
    </VbCard>
    <VbCard
      title="Object options"
      style="width: 400px;"
    >
      <va-select
        v-model="objectSingleSelectWithIcons.value"
        class="mb-6"
        label="Options with icon"
        :options="objectSingleSelectWithIcons.options"
        text-by="text"
        key-by="icon"
      />
      <p>Value: {{ objectSingleSelectWithIcons.value }}</p>
      <va-select
        v-model="objectSingleSelect.value"
        class="mb-6"
        label="Single select text by text (default)"
        :options="objectSingleSelect.options"
        text-by="text"
      />
      <va-select
        v-model="objectSingleSelect.value"
        class="mb-6"
        label="Text by value"
        :options="objectSingleSelect.options"
        text-by="value"
      />
      <va-select
        v-model="objectSingleSelect.value"
        class="mb-6"
        label="Track by text property"
        :options="objectSingleSelect.options"
        track-by="text"
      />
      <va-select
        v-model="objectSingleSelect.value"
        class="mb-6"
        label="Track by text property (function)"
        :options="objectSingleSelect.options"
        track-by="text"
      />
      <p>Value: {{ objectSingleSelect.value }}</p>
      <va-select
        v-model="objectMultiSelect.value"
        class="mb-6"
        label="Multi select Text by value"
        :options="objectMultiSelect.options"
        text-by="value"
        multiple
      />
      <va-select
        v-model="objectMultiSelect.value"
        class="mb-6"
        label="Searchable multiselect text-by value"
        :options="objectMultiSelect.options"
        text-by="value"
        multiple
        searchable
      />
      <p>Value: {{ objectMultiSelect.value }}</p>
      <va-select
        v-model="objectMultiSelectByValue.value"
        class="mb-6"
        label="Multi select value by value"
        :options="objectMultiSelectByValue.options"
        text-by="value"
        value-by="value"
        multiple
      />
      <p>Value: {{ objectMultiSelectByValue.value }}</p>
    </VbCard>
    <VbCard
      title="Grouped"
      style="width: 400px;"
    >
      <va-select
        v-model="objectGrouped.value"
        class="mb-6"
        :options="objectGrouped.options"
      />

    </VbCard>
    <VbCard
      title="Decorators"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="With label"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,"
        placeholder="Long label"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        placeholder="With placeholder"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Long placeholder"
        placeholder="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,"
        :options="defaultSingleSelect.options"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="No options"
        :options="[]"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="No options with custom text"
        :options="[]"
        no-options-text="Sorry, nothing to show :("
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Clearable"
        :options="defaultSingleSelect.options"
        clearable
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Clearable and custom clear icon"
        :options="defaultSingleSelect.options"
        clearable
        clearable-icon="cancel"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Hint messages"
        :options="defaultSingleSelect.options"
        :messages="['Hint message 1', 'Hint message 2']"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Prepend slot"
        :options="defaultSingleSelect.options"
      >
        <template #prepend>
          <va-icon name="share" />
        </template>
      </va-select>
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Prepend inner slot"
        :options="defaultSingleSelect.options"
      >
        <template #prependInner>
          <va-icon name="share" />
        </template>
      </va-select>
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Append inner slot"
        :options="defaultSingleSelect.options"
      >
        <template #appendInner>
          <va-icon name="share" />
        </template>
      </va-select>
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Append slot"
        :options="defaultSingleSelect.options"
      >
        <template #append>
          <va-icon name="share" />
        </template>
      </va-select>
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="All slots"
        :options="defaultSingleSelect.options"
        clearable
        :messages="['Hint message 1', 'Hint message 2']"
      >
        <template #prepend>
          <va-icon name="share" />
        </template>
        <template #prependInner>
          <va-icon name="share" />
        </template>
        <template #appendInner>
          <va-icon name="share" />
        </template>
        <template #append>
          <va-icon name="share" />
        </template>
      </va-select>
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        label="Content slot"
        :options="defaultMultiSelect.options"
        multiple
      >
        <template #content="{ value }">
          <va-chip>{{ value || 'no value :(' }}</va-chip>
          <span class="ml-6">
            Click on share ;)
            <va-icon
              name="share"
              @click="alert('Thank you for click!')"
            />
          </span>
        </template>
      </va-select>
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Custom list placement (top)"
        :options="defaultSingleSelect.options"
        placement="top"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Custom list placement (bottom)"
        :options="defaultSingleSelect.options"
        placement="bottom"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Custom list height (320px)"
        :options="defaultSingleSelect.options"
        max-height="320px"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Custom select width (50%)"
        :options="defaultSingleSelect.options"
        width="50%"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Required Mark"
        :options="defaultSingleSelect.options"
        required-mark
      />
    </VbCard>
    <VbCard
      title="State"
      style="width: 400px;"
    >
      <va-checkbox
        class="my-3"
        label="Clearable"
        v-model="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Readonly"
        placeholder="Try to type in ..."
        :options="defaultSingleSelect.options"
        readonly
        :clearable="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Disabled"
        placeholder="Try to focus ..."
        :options="defaultSingleSelect.options"
        disabled
        :clearable="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Loading"
        :options="defaultSingleSelect.options"
        loading
        :clearable="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Error state"
        :options="defaultSingleSelect.options"
        error
        :clearable="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Error state with messages"
        :options="defaultSingleSelect.options"
        error
        :error-messages="['Error message']"
        :clearable="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Success state"
        :options="defaultSingleSelect.options"
        success
        :clearable="isClearable"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Success state with messages"
        :options="defaultSingleSelect.options"
        success
        :messages="['Success message']"
        :clearable="isClearable"
      />
    </VbCard>
    <VbCard
      title="Searchable"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Searchable single select"
        :options="defaultSingleSelect.options"
        searchable
      />
      <va-select
        v-model="defaultMultiSelect.value"
        class="mb-6"
        label="Searchable multi select"
        :options="defaultMultiSelect.options"
        multiple
        searchable
      />
       <va-select
        v-model="defaultSingleSelect.value"
        class="mb-6"
        label="Searchable changed text"
        :options="defaultSingleSelect.options"
        searchable
        searchtext="test"
      />
      <va-select
        v-model="defaultSingleSelect.value"
        label="Search with throttling"
        :options="defaultSingleSelect.options"
        :delay="1000"
        searchable
      />
    </VbCard>
    <VbCard
      title="Allow create new"
      style="width: 400px;"
    >
      <va-select
        v-model="allowCreateSelect.value"
        class="mb-6"
        label="'true' mode and single select"
        :options="allowCreateSelect.options"
        @create-new="addNewOption"
        track-by="id"
        allow-create
      />
      <va-select
        v-model="allowCreateSelect.allowUniqueValue"
        class="mb-6"
        label="'unique' mode and single select"
        :options="allowCreateSelect.options"
        @create-new="addNewOption"
        track-by="id"
        allow-create="unique"
      />
      <va-select
        v-model="allowCreateSelect.valueMultiple"
        class="mb-6"
        label="'true' mode and multi select"
        :options="allowCreateSelect.options"
        @create-new="addNewOption"
        track-by="id"
        allow-create
        multiple
      />
      <va-select
        v-model="allowCreateSelect.allowUniqueValueMultiple"
        label="'unique' mode and multi select"
        class="mb-6"
        :options="allowCreateSelect.options"
        @create-new="addNewOption"
        track-by="id"
        allow-create="unique"
        multiple
      />
      <va-select
        v-model="allowCreateSelect.valueMultipleMax"
        class="mb-6"
        label="'true' mode and multi select, Max 3 selections"
        :options="allowCreateSelect.options"
        @create-new="addNewOption"
        track-by="id"
        allow-create
        multiple
        :max-selections="3"
      />
    </VbCard>
    <VbCard
      title="With ajax"
      style="width: 400px;"
    >
      <va-select
        v-model="defaultSingleSelect.value"
        searchable
        :options="countriesList"
        :loading="isLoading"
        @updateSearch="updateSearch"
      />
    </VbCard>
    <VbCard
      title="scroll-bottom event"
      style="width: 400px;"
    >
      <va-select
        v-model="preloadable.value"
        :options="preloadable.options"
        @scroll-bottom="onLoadMore"
      />
    </VbCard>
    <VbCard
      title="Validation rules (on blur)"
      style="width: 400px;"
    >
      <va-select
        v-model="validationSelect.value"
        class="mb-6"
        label="At least 1 option should be selected"
        :options="validationSelect.options"
        :rules="validationSelect.rules.required"
        multiple
      />
      <va-select
        v-model="validationSelect.multipleValue"
        class="mb-6"
        label="Exactly 2 options should be selected"
        :options="validationSelect.options"
        :rules="validationSelect.rules.twoOptions"
        multiple
      />
    </VbCard>
    <VbCard :style="{ 'width': '100%' }">
      <p>{{ defaultSingleSelect.value }}</p>
      <p>{{ objectSingleSelect.value }}</p>
      <p>{{ multipleValue }}</p>
      <p>{{ longSelect.value }}</p>
      <p>{{ validationSelect.value }}</p>
    </VbCard>
  </VbDemo>
</template>

<script>
import { objectOptionsList, iconOptionsList, countriesList } from './demo/DemoData'

import { VaIcon } from '../va-icon'
import { VaCheckbox } from '../va-checkbox'
import { VaChip } from '../va-chip'
import { VaSelect } from './index'

const positions = ['top', 'bottom']

const random = () => Math.ceil(Math.random() * 10000) + ''

export default {
  components: { VaSelect, VaIcon, VaCheckbox, VaChip },
  data () {
    return {
      allowCreateValue: '',
      allowCreateValueMultiple: '',
      disabledValue: 'Selected option',
      defaultSingleSelect: {
        options: ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'],
        value: '',
      },
      withVirtualScroller: {
        options: new Array(1000).fill(null).map((_, index) => index),
        value: '',
      },
      defaultMultiSelect: {
        options: ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine'],
        value: [],
      },
      preloadable: {
        options: [random(), random(), random(), random(), random(), random(), random(), random(), random(), random()],
        value: '',
      },
      allowCreateSelect: {
        options: [
          { id: '0', text: 'one', value: 'one' },
          { id: '1', text: 'two', value: 'two' },
          { id: '2', text: 'three', value: 'three' },
          { id: '3', text: 'four', value: 'four' },
          { id: '4', text: 'five', value: 'five' },
        ],
        value: '',
        allowUniqueValue: '',
        valueMultiple: [],
        allowUniqueValueMultiple: [],
        valueMultipleMax: [],
      },
      disabledOptions: {
        options: [
          { id: '0', text: 'one', value: 'one', disabled: true },
          { id: '1', text: 'two', value: 'two' },
          { id: '2', text: 'three', value: 'three', disabled: true },
          { id: '3', text: 'four', value: 'four' },
          { id: '4', text: 'five', value: 'five' },
          { id: '5', text: 'six', value: 'six', disabled: true },
        ],
        value: '',
      },
      objectSingleSelect: {
        value: '',
        options: objectOptionsList,
      },
      objectGrouped: {
        options: [
          { id: '0', text: 'one', value: 'one', group: 'foo' },
          { id: '1', text: 'two', value: 'two', group: '' },
          { id: '2', text: 'three', value: 'three', group: 'bar' },
          { id: '3', text: 'four', value: 'four', group: 'bar' },
          { id: '4', text: 'five', value: 'five', group: 'foo' },
        ],
        value: '',
      },
      objectMultiSelect: {
        value: [],
        options: objectOptionsList,
      },
      objectMultiSelectByValue: {
        value: [],
        options: objectOptionsList,
      },
      objectSingleSelectWithIcons: {
        value: '',
        options: iconOptionsList,
      },
      objectMultiSelectWithIcons: {
        value: [],
        options: iconOptionsList,
      },
      longSelect: {
        value: '1st long long long long option sit amet, consectetur adipiscing elit,',
        options: [
          '1st long long long long option sit amet, consectetur adipiscing elit,',
          '2nd long  sit amet, consectetur adipiscing elit, long long long long long option',
        ],
      },
      validationSelect: {
        options: ['one', 'two', 'three', 'four'],
        value: '',
        multipleValue: [],
        rules: {
          required: [v => Array.isArray(v) ? v.length >= 1 : !!v || 'at least 1 option should be selected'],
          twoOptions: [v => (Array.isArray(v) && v.length === 2) || '2 options should be selected'],
        },
      },
      multipleValue: [],
      countriesList,
      positions,
      isLoading: false,
      isClearable: true,
    }
  },
  methods: {
    onLoadMore () {
      this.preloadable.options.push(random(), random(), random())
    },
    updateSearch (val) {
      this.isLoading = true
      setTimeout(() => {
        this.isLoading = false
      }, 2000)
    },
    alert (str) {
      window.alert(str)
    },
    addNewOption (newOption) {
      const option = { id: String(this.allowCreateSelect.options.length), text: newOption, value: newOption }
      this.allowCreateSelect.options = [...this.allowCreateSelect.options, option]
      this.allowCreateSelect.value = option
    },
  },
}
</script>
