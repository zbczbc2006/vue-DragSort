<template>
  <div class="drag-sort">
    <div v-for="(item, index) of list" draggable="true" @dragstart="dragstartHandler($event,index)" @dragover.prevent @drop.prevent="dropHandler($event,index)" :key="item">
      <slot :item="item" :index="index"></slot>
    </div>
  </div>
</template>
<script>
export default {
  name: 'drag-sort',
  props: {
    list: {
      required: true,
      type: Array,
    },
  },
  methods: {
    dragstartHandler(event, index) {
      event.dataTransfer.setData('indexOld', index);
    },
    dropHandler(event, index) {
      let indexOld = event.dataTransfer.getData('indexOld');
      let itemMove = this.list.splice(indexOld, 1)[0];
      this.list.splice(index, 0, itemMove);
      this.$emit('change', this.list);
    },
  },
}
</script>
