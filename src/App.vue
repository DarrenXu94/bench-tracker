<template>
  <div>
    <h1 class="text-center mb-3">Bench Tracker</h1>
    <div class="d-flex justify-content-center">
      <div class="col-4">
        <h3>Field</h3>
        <draggable class="list-group" :list="list1" group="people" @change="fieldLog">
          <transition-group type="transition" name="flip-list">
            <div
              class="list-group-item"
              v-for="(element, index) in list1"
              :key="element.name"
            >{{ element.name }} {{ index }}</div>
          </transition-group>
        </draggable>
      </div>

      <div class="col-4">
        <h3>Bench</h3>
        <draggable class="list-group" :list="list2" group="people" @change="benchLog">
          <transition-group type="transition" name="flip-list">
            <div
              class="list-group-item"
              v-for="(element, index) in list2"
              :key="element.name"
            >{{ element.name }} {{ index }}</div>
          </transition-group>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "app",
  components: {
    draggable
  },
  created: () => {},
  data() {
    return {
      list1: [
        { name: "John", id: 1 },
        { name: "Joao", id: 2 },
        { name: "Jean", id: 3 },
        { name: "Gerard", id: 4 }
      ],
      list2: [
        { name: "Juan", id: 5 },
        { name: "Edgard", id: 6 },
        { name: "Johnson", id: 7 }
      ]
    };
  },
  methods: {
    benchLog: function(evt) {
      window.console.log("bench", evt);
    },
    fieldLog: function(evt) {
      window.console.log("field", evt);
    }
  }
};
</script>

<style lang="scss">
.button {
  margin-top: 35px;
}
.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0s;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group {
  min-height: 20px;
}
.list-group-item {
  cursor: move;
}
.list-group-item i {
  cursor: pointer;
}
</style>
