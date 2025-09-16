<template>
  <div class="field">
    <input
      :value="value"
      :placeholder="placeholder"
      @input="$emit('input', $event.target.value)"
    />
  </div>
</template>

<script>
export default {
  name: "ComponentInput",
  props: {
    value: { type: String, default: "" }, // v-model erwartet Prop "value"
    placeholder: { type: String, default: "" },
  },
};
</script>

<style scoped>
.field {
  margin: 10px 0;
}
input {
  padding: 6px 10px;
  border: 1px solid #aaa;
  border-radius: 4px;
}
</style>
