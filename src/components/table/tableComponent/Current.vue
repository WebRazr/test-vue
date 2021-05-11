<template>
  <div class="center-data-block">
    <p :style="total.cur ? 'color: green' : 'color: red'">{{ total.value }}</p>
  </div>
</template>
<script>
export default {
  name: "Current",
  props: ["total"],
};
</script>
