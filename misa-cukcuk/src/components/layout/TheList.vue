<template>
  <div id="list">
    <the-top-of-list />
    <the-table />
    <the-footer />
  </div>
</template>

<script>
import TheTopOfList from "./TheTopOfList.vue"
import TheFooter from "./TheFooter.vue"
import TheTable from './TheTable.vue'

export default {
  components: { TheTopOfList, TheFooter, TheTable},
};
</script>

<style>
</style>