<template>
  <va-alert
    center
    class="mb-6"
  >
    {{ $t("alert.misc.centered") }}
  </va-alert>
  <va-alert
    color="warning"
    closeable
    :title="$t('alert.misc.title')"
    icon="favorite"
    center
    class="mb-6"
  >
    {{ $t('alert.misc.centered') }}
  </va-alert>
</template>
