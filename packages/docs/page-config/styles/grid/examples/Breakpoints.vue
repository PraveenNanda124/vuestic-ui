<template>
  <va-card
    color="background-element"
    style="padding: 0.75rem;"
  >
    <div class="row">
      <div class="flex flex-col md12">
        <div class="item">
          md12
        </div>
      </div>
      <div class="flex flex-col md6">
        <div class="item">
          md6
        </div>
      </div>
      <div class="flex flex-col md6">
        <div class="item">
          md6
        </div>
      </div>
    </div>
    <br>
    <div class="row">
      <div class="flex flex-col md12">
        <div class="item">
          md12
        </div>
      </div>
      <div class="flex flex-col md9">
        <div class="item">
          md9
        </div>
      </div>
      <div class="flex flex-col md3">
        <div class="item">
          md3
        </div>
      </div>
    </div>
  </va-card>
</template>

<style lang="scss" scoped>
@import "vuestic-ui/src/styles/resources";
@import "vuestic-ui/src/styles/grid/grid.scss";

.item {
  border: 1px solid var(--va-background-border);
  background-color: var(--va-background-primary);
  text-align: center;
}
</style>
