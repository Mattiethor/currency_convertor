<template>
  <div>
    <div>
      <b>{{ currency }}</b> 
    </div>
    <div> <u>Conversion rate: {{ rate }}</u> </div>
  </div>
</template>

<script>
export default {
  name: "CurrencyInfo",
  props: ["currency", "rate"],
};
</script>

<style>
</style>