<template>
  <div class="col-11 col-md-4 text-center d-flex justify-content-between list-group-item">
    <span>{{data.name}}</span>
    <span>Time on bench: {{pad(parseInt(counter/60))}}:{{pad(counter % 60)}}</span>
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
  props: {
    data: Object
  },
  created: function() {
    setInterval(() => {
      this.counter++;
    }, 1000);
  },
  methods: {
    pad: function(val) {
      var valString = val + "";
      if (valString.length < 2) {
        return "0" + valString;
      } else {
        return valString;
      }
    }
  }
};
</script>
