<template>
  <div class="center-data-block">
    <p :style="'color: blue'">{{ start }}</p>
  </div>
</template>
<script>
export default {
  name: "Start",
  props: ["start"],
};
</script>
