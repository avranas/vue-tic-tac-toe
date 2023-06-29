<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'BoxComponent',
  components: {},
  props: ['boxState', 'handleClick', 'rowIndex', 'boxIndex'],
  methods: {
    handleBoxClick() {
      this.handleClick(this.rowIndex, this.boxIndex)
    }
  }
})
</script>

<template>
  <div id="box">
    <!-- Different syntax for button clicks for some reason -->
    <button @click="handleBoxClick">
      {{ boxState }}
    </button>
  </div>
</template>

<style>
#box {
  background-color: green;
  width: 3rem;
  height: 3rem;
}
</style>
