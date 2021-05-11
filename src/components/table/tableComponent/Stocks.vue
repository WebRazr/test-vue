<template>
  <div class="center-data-block">
    <p :style="'color: blue'">{{ stock }}</p>
  </div>
</template>
<script>
export default {
  name: "Stocks",
  props: ["stock"],
};
</script>
