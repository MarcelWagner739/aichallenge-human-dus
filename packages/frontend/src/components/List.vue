<template>
  <li>
    {{ title }}
    <button @click="$emit('remove')">Remove</button>
  </li>
</template>

<script>
export default {
  name: "List",
  props: ["title"],
  emits: ["remove"],
};
</script>
