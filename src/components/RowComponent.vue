<script lang="ts">
import { defineComponent } from 'vue'
import BoxComponent from './BoxComponent.vue'

export default defineComponent({
  name: 'RowComponent',
  components: { BoxComponent },
  props: ['rowState', 'handleClick', 'rowIndex']
})
</script>

<template>
  <div id="row">
    <div v-for="(box, index) in rowState" v-bind:key="'box-'+index">
      <BoxComponent
        :rowIndex="rowIndex"
        :boxIndex="index"
        :boxState="box"
        :handleClick="handleClick"
      />
    </div>
  </div>
</template>

<style>
#row {
  display: flex;
  background-color: blue;
  width: 9rem;
  height: 3rem;
}
</style>
