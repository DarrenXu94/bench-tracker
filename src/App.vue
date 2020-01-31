<template>
  <div>
    <h1 style="font-size:5vw;" class="text-center mb-3">Bench Tracker</h1>
    <div class="d-flex justify-content-center">
      <div class="col-6 col-sm-4">
        <h3>Field</h3>
        <draggable class="list-group" :list="list1" group="people" @change="fieldLog">
          <!-- <transition-group type="transition" name="flip-list"> -->
          <div
            class="drag list-group-item"
            v-for="element in list1"
            :key="element.name"
          >{{ element.name }}</div>
          <!-- </transition-group> -->
        </draggable>
      </div>

      <div class="col-6 col-sm-4">
        <h3>Bench</h3>
        <draggable class="list-group" :list="list2" group="people" @change="benchLog">
          <!-- <transition-group type="transition" name="flip-list"> -->
          <div
            class="drag list-group-item"
            v-for="element in list2"
            :key="element.name"
          >{{ element.name }}</div>
          <!-- </transition-group> -->
          <div v-if="!list2.length">No players on the bench</div>
        </draggable>
      </div>
    </div>
    <div class="mt-3 mb-3">
      <h3 class="text-center">Bench timer</h3>
      <div class="d-flex justify-content-center flex-column align-items-center">
        <bench-timer v-for="player of benchedPlayers" :key="player.id" :data="player"></bench-timer>
      </div>
    </div>
  </div>
</template>

<script>
import draggable from "vuedraggable";
import BenchTimer from "./components/BenchTimer";

export default {
  name: "app",
  components: {
    draggable,
    BenchTimer
  },
  data() {
    return {
      list1: [
        { name: "Daz", id: 1 },
        { name: "Van", id: 2 },
        { name: "Ed", id: 3 },
        { name: "Caleb", id: 4 },
        { name: "Luca", id: 5 },
        { name: "Arnie", id: 6 },
        { name: "Adrian", id: 7 }
      ],
      list2: [],
      benchedPlayers: []
    };
  },
  methods: {
    benchLog: function(evt) {
      window.console.log("bench", evt);
      if ("added" in evt) {
        this.benchedPlayers.push(evt.added.element);
      }
      if ("removed" in evt) {
        this.benchedPlayers = this.benchedPlayers.filter(player => {
          return player.id !== evt.removed.element.id;
        });
      }
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
  min-height: 50vh;
}
.drag.list-group-item {
  cursor: move;
  :hover {
    background: red !important;
  }
}
.drag.list-group-item i {
  cursor: pointer;
}
</style>
