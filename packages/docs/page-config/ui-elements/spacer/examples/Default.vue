<template>
  <va-card>
    <va-card-content>
      <div class="flex">
        <va-button>Button</va-button>
        <va-spacer class="spacer" />
        <va-button>Button</va-button>
      </div>
    </va-card-content>
  </va-card>
</template>

<style lang="scss">
.spacer {
  text-align: center;
  border: 2px dashed var(--va-secondary);

  &::after {
    content: "VaSpacer is here!";
  }
}
</style>
