<template>
  <div>
    <slot v-bind:dataFromMySlot="data"></slot>
  </div>
</template>
<script>
export default {
  name: "DataSlotComponent",
  data() {
    return {
      data: "This is local data from DataSlotComponent",
    };
  },
};
</script>

<style scoped>
div {
  height: 70px;
  width: 70%;
  border: dotted black 1px;
  margin: 10px;
  padding: 10px;
  background-color: lightgreen;
  font-weight: bold;
}
</style>
