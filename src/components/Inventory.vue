<template>
  <div class="grid">
    <div
      draggable="true"
      v-for="cell in cells"
      :key="cell.id"
      :id="`div-${cell-1}-${id}`"
      @dragstart="drag"
      @dragover.prevent
      @drop.stop="drop"
    >
    </div>
  </div>
</template>

<script>
export default {
  props: ['id', 'items'],
  data () {
    return {
      cells: 9,
      currentTarget: ''
    }
  },
  methods: {
    drag (cell) {
      this.currentTarget = cell.target.id
    },
    drop (cell) {
      const oldEl = document.getElementById(this.currentTarget).firstChild
      const newEl = document.getElementById(cell.target.id).firstChild

      if (oldEl) {

        const parentDivOld = oldEl.parentNode

        if (!newEl) {
          const oldElClone = parentDivOld.cloneNode(true).firstChild
          const parentDivNew = document.getElementById(cell.target.id)
          parentDivNew.appendChild(oldElClone)

          parentDivOld.removeChild(oldEl)


          console.debug('old position: ', parentDivOld.id.slice(4))
          console.debug('new position: ', parentDivNew.id.slice(4))
        } else {
          const parentDivNew = newEl.parentNode

          const oldElClone = parentDivOld.cloneNode(true).firstChild
          const newElClone = parentDivNew.cloneNode(true).firstChild

          parentDivNew.appendChild(oldElClone)
          parentDivOld.appendChild(newElClone)

          parentDivNew.removeChild(newEl)
          parentDivOld.removeChild(oldEl)


          console.debug('old position: ', parentDivOld.id.slice(4))
          console.debug('new position: ', parentDivNew.id.slice(4))
        }
      }
    }
  },
  mounted () {
    for (let j = 0; j < this.cells; j++) {
      const divId = document.getElementById(`div-${j}-${this.id}`)

      const item = this.items.find(i => {
        let n = Math.sqrt(this.cells)*i.y + i.x
        return n === j
      })

      if (item && Math.sqrt(this.cells)*item.y + item.x === j) {
        let p = document.createElement("span");
        let p1_content = document.createTextNode(`${item.icon}`);
        p.appendChild(p1_content)
        divId.appendChild(p1_content)
      }
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
