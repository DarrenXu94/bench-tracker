<template>
  <div>
    Benched
    {{counter}}
  </div>
</template>

<script>
export default {
  name: "BenchTimer",
  data() {
    return {
      counter: 0
    };
  },
  created: function() {
    setInterval(() => {
      this.counter++;
    }, 1000);
  }
};
</script>