<template>
  <div id="app">
    <div id="settings-box">
      <div class="settings-item">
        <div class="setting-half">
          <span class="text" style="float: right;">filter colors:</span>
        </div>
        <div class="setting-half">
          <input type="text" v-model="filter" class="text" style="float: left; width: 20vh;"/>
        </div>
      </div>
      <div class="settings-item">
        <div class="setting-half">
          <span class="text" style="float: right;">limit amount of colors shown:</span>
        </div>
        <div class="setting-half">
          <input type="checkbox" v-model="limit" style="float: left; width: 2vh; height: 2vh; margin-top: 0.4vh"/>
        </div>
      </div>
      <br>
      <span class="text" style="font-family: RobotoSlabLight">{{ getFilterText() }}</span>
    </div>
    <div id="card-list">
      <NamedColor
        v-for="(namedColor, index) in getFiltered(limit)"
        :key="index"
        :namedColor="namedColor"
      ></NamedColor>
    </div>
  </div>
</template>

<script>
import ncJSON from "./assets/colors.json";
import NamedColor from "./components/NamedColor.vue";

export default {
  name: "App",
  data() {
    return {
      namedColors: [],
      filter: "",
      limit: true,
    };
  },
  components: {
    NamedColor,
  },
  methods: {
    getFiltered(limit) {
      var filter = this.filter.toLowerCase();
      var filtered = this.namedColors;
      if (filter.length > 1) {
        filtered = this.namedColors.filter(function (v) {
          return v.name.includes(filter);
        });
      }
      return limit ? filtered.slice(0, 100) : filtered;
    },
    getFilterText() {
      var filtered = this.getFiltered();
      if (filtered.length == 0)
        return `found no colors with filter "${this.filter}"`;
      if (this.filter.length > 1)
        return `found ${filtered.length} colors with filter "${this.filter}"`;
      return `loaded ${filtered.length} colors`;
    },
  },
  mounted() {
    for (let i = ncJSON.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [ncJSON[i], ncJSON[j]] = [ncJSON[j], ncJSON[i]];
    }
    // var res = ncJSON.slice(0, 1000);
    var res = ncJSON;
    this.namedColors = res;
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 5vh;
}

#card-list {
  width: 90vw;
  display: inline-block;
}

#settings-box {
  margin-bottom: 3vh;
}

.setting-half {
  width: 50%;
  margin: 1vh;
}

.settings-item {
  height: 5vh;
  display: flex;
}

.text {
  font-family: "RobotoSlab";
  font-size: 2vh;
}

@font-face {
  font-family: "RobotoSlab";
  src: local("RobotoSlab"),
    url(./fonts/RobotoSlab-Regular.ttf) format("truetype");
}

@font-face {
  font-family: "RobotoSlabLight";
  src: local("RobotoSlab"),
    url(./fonts/RobotoSlab-Light.ttf) format("truetype");
}
</style>
