<template>
  <section class="admin">
    <div class="admin__wrapper">
      <div class="admin__inner">
        <h2 class="admin__title">
          {{ $t('landing.admin.title') }}
        </h2>
        <div class="admin__subtitle">
          {{ $t('landing.admin.text') }}
        </div>
        <div class="admin__buttons">
          <va-button
            class="admin__buttons--button"
            href="https://github.com/epicmaxco/vuestic-admin"
            target="blank"
          >
            <template #prepend>
              <va-icon
                class="fa fa-github"
                style="margin-right: 0.5rem;"
              />
            </template>
            {{ $t('landing.admin.buttons.github') }}
          </va-button>
          <va-button
            class="admin__buttons--button"
            href="https://vuestic.epicmax.co/admin/dashboard"
            target="blank"
            preset="secondary"
          >
            {{ $t('landing.admin.buttons.demo') }}
          </va-button>

          <div class="admin__buttons--button">
            <landing-stars-button repo="epicmaxco/vuestic-admin" />
          </div>
        </div>
        <div class="admin__content">
          <div class="admin__content__item admin__content__item--first">
            <img
              src="/landing/admin/admin.png"
              alt="Vuestic Admin"
              height="555px"
              width="875px"
            >
          </div>
          <div class="admin__content__item admin__content__item--second">
            <!-- items -->
            <div class="items">
              <div class="item item--first">
                <div class="item__frame">
                  <img
                    src="/landing/admin/open-source.svg"
                    alt="Open source"
                    height="32px"
                    width="32px"
                  >
                </div>
                <h2 class="item__title">
                  {{ $t('landing.admin.features.opensource') }}
                </h2>
              </div>

              <div class="item">
                <div class="item__frame">
                  <img
                    src="/landing/admin/themes.svg"
                    alt="Themes"
                    height="32px"
                    width="32px"
                  >
                </div>
                <h2 class="item__title">
                  {{ $t('landing.admin.features.themes') }}
                </h2>
              </div>

              <div class="item">
                <div class="item__frame">
                  <img
                    src="/landing/admin/responsive.svg"
                    alt="Responsive"
                    height="32px"
                    width="32px"
                  >
                </div>
                <h2 class="item__title">
                  {{ $t('landing.admin.features.responsive') }}
                </h2>
              </div>

              <div class="item">
                <div class="item__frame">
                  <img
                    src="/landing/admin/i18n.svg"
                    alt="i18n"
                    height="32px"
                    width="32px"
                  >
                </div>
                <h2 class="item__title">
                  {{ $t('landing.admin.features.i18n') }}
                </h2>
              </div>
            </div>
            <!-- /items -->
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts" setup>
import LandingStarsButton from './StarsButton.vue'
</script>

<style lang="scss" scoped>
@import '@/assets';

.admin {
  width: 100%;
  position: relative;
  padding-top: 4.5rem;
  padding-bottom: 8.5rem;
  background-color: var(--va-background-landing);
  color: var(--va-on-background-landing);

  // sm
  @include sm(padding-top, 3rem);
  @include sm(padding-bottom, 5rem);

  &__wrapper {
    @include wrapper();
  }

  &__inner {
    @include row-flex();

    align-items: center;
  }

  &__title {
    @include col();
    @include size(12);
    @include title-font();

    padding-top: 3.5rem;
    text-align: center;
  }

  &__subtitle {
    @include col();
    @include size(12);
    @include text-font();

    padding-top: 1rem;
    line-height: 1.5;
    text-align: center;
  }

  &__buttons {
    @include row-flex();

    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    padding-top: 1.5rem;

    &--button {
      --va-button-content-px: 1.5rem;

      @include button-font();
      @include md(margin-bottom, 1rem);
      @include md(justify-content, center);
      @include xs(width, 100%);
      @include xs(margin, 0 1rem 1rem 1rem);

      height: 3rem;
      margin-right: 1rem;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  }

  &__content {
    @include row-flex();
    @include col();
    @include size(12);

    padding-top: 4rem;
    justify-content: center;

    &__item {
      &--first {
        @include col();
        @include size(8);
        @include shift-right(1);

        // md
        @include size-md(12);
        @include shift-md-right(0);

        img {
          object-fit: contain;
          max-width: 100%;
          max-height: 100%;
        }
      }

      &--second {
        @include col();
        @include size(3);

        display: flex;
        flex-direction: column;
        justify-content: center;

        // md
        @include size-md(12);
      }
    }
  }
}

.items {
  @include row-flex();

  .item {
    $color: #6c7898;

    @include col();
    @include size(12);

    display: flex;
    align-items: center;
    padding-top: 2.2rem;

    // md
    @include size-md(6);
    // xs
    @include size-xs(12);

    &--first {
      padding-top: 0;

      // md
      @include md(padding-top, 2.2rem);
    }

    &__frame {
      display: inline-block;
      padding: 0.75rem;
      border: 1px dashed $color;
      border-radius: 1rem;
    }

    &__title {
      @include text-font();

      padding-left: 1rem;
      line-height: 1.5;
    }
  }
}

.stars-button {
  @include code-font();

  padding: 0 !important;
  color: #ffffff !important;
  height: 1.75rem;
}
</style>
