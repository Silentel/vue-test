<template>
  <div id="app">
    <h1>Первый инвентарь</h1>
    <inventory :items="items"></inventory>
    <h1>Второй инвентарь</h1>
    <inventory :items="items2"></inventory>
  </div>
</template>

<script>
import Inventory from '@/components/Inventory'
import { items, items2 } from '@/data'

export default {
  name: 'App',
  components: {
    Inventory
  },
  data () {
    return {
      items,
      items2
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
