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
          <div v-if="!list2.length">No players on the bench</div>
        </draggable>
      </div>
    </div>
    <div class="mt-3">
      <h3 class="text-center">Bench timer</h3>
      <bench-timer v-for="player of benchedPlayers" :key="player"></bench-timer>
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
        { name: "John", id: 1 },
        { name: "Joao", id: 2 },
        { name: "Jean", id: 3 },
        { name: "Gerard", id: 4 },
        { name: "Juan", id: 5 },
        { name: "Edgard", id: 6 },
        { name: "Johnson", id: 7 }
      ],
      list2: [],
      benchedPlayers: []
    };
  },
  methods: {
    benchLog: function(evt) {
      window.console.log("bench", evt);
      if ("added" in evt) {
        // add something to an array?
        // this.triggerTimer(evt);
        this.benchedPlayers.push(evt.added.element.id);
      }
    },
    fieldLog: function(evt) {
      window.console.log("field", evt);
    },
    triggerTimer: function(evt) {
      const user = evt.added.element.id;
      let playerTimer = setInterval(() => {
        if (this._data[user]) {
          this._data[user] = this._data[user] + 1;
        } else {
          this._data[user] = 1;
        }
        console.log(this._data);
      }, 1000);
      // this.timerTracker[user] = playerTimer;
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
.list-group-item {
  cursor: move;
}
.list-group-item i {
  cursor: pointer;
}
</style>
