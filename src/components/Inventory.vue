<template>
  <div class="grid">
    <div
      draggable="true"
      v-for="slot of slots"
      :key="slot.index"
      :data-index="slot.index"
      @dragstart="drag"
      @dragover.prevent
      @drop.stop="drop"
    >
      <span v-if="slot.content">
        {{ slot.content.icon }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: ['id', 'items'],
  data () {
    return {
      cells: 9,
      currentTarget: '',
      slots: [],
    }
  },
  methods: {
    drag (cell) {
      console.log(cell.target.dataset.index)
      this.currentTarget = cell.target.dataset.index
    },
    drop (cell) {
      if (cell.target.dataset.index === undefined) {
        const parentDiv = cell.target.parentNode

        console.log(parentDiv.dataset.index)

        const oldVal = this.slots[this.currentTarget].content
        const newVal = this.slots[parentDiv.dataset.index].content

        this.slots[parentDiv.dataset.index].content = oldVal
        this.slots[this.currentTarget].content = newVal
      } else {
        console.log(cell.target.dataset.index)

        const oldVal = this.slots[this.currentTarget].content        
        const newVal = this.slots[cell.target.dataset.index].content
        
        this.slots[cell.target.dataset.index].content = oldVal
        this.slots[this.currentTarget].content = newVal
      }
    }
  },
  mounted () {
    for (let i = 0; i < this.cells; i++) {
      this.slots.push({content: null, index: i})
    }
    for (let item of this.items) {
      this.slots[item.y * 3 + item.x].content = item
    }
  }
}
</script>

<style scoped>
.grid { 
  display: grid;
  grid-template-rows: 1fr 1fr 1fr;
  grid-template-columns: 1fr 1fr 1fr;
  grid-gap: 2vw;
}
.grid > div {
  font-size: 5vw;
  padding: .5em;
  background: rgb(80, 80, 80);
  text-align: center;
}
</style>