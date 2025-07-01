<template>
  <div>
    <input type="text" placeholder="Anzahl Gewinner default (2)" />
    <button @click="$emit('calculate')">Ermittle Gewinner</button>
  </div>
</template>

<script>
export default {
  name: "List",
  emits: ["calculate"],
};
</script>
