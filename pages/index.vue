<template>
  <div>
    {{contents}}
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'

@Component
export default class PageIndex extends Vue {
  contents: any = 'これはコンテンツです'
}
</script>

<style lang="scss">

</style>
