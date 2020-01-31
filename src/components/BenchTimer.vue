<template>
  <div class="col-11 col-md-4 text-center d-flex justify-content-between list-group-item">
    <span>{{data.name}}</span>
    <span>Time on bench: {{pad(Math.floor(parseInt(counter/60)))}}:{{pad(Math.floor(counter % 60))}}</span>
  </div>
</template>

<script>
export default {
  name: "BenchTimer",
  data() {
    return {
      counter: 0,
      startTime: null
    };
  },
  props: {
    data: Object
  },
  created: function() {
    this.startTime = new Date();
    setInterval(() => {
      this.counter = (new Date().getTime() - this.startTime.getTime()) / 1000;
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
