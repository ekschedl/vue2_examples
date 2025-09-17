<template>
  <div>
    <slot name="topSlot"></slot>
  </div>
</template>

<script>
export default {
  name: "SlotComponent",
};
</script>

<style scoped>
div {
  height: 50px;
  width: 50%;
  border: dotted black 1px;
  margin: 10px;
  padding: 10px;
  background-color: lightgreen;
  font-weight: bold;
}
</style>
