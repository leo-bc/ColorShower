<template>
  <div id="main-box" v-bind:style="{ backgroundColor: toRGB() }">
    <div id="outer-box">
      <div id="inner-box">
        <div id="text-box" v-bind:style="{ backgroundColor: getFontColor(true) }">
          <span id="name-text" v-bind:style="{ color: toRGB() }">
            {{ namedColor.name }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "NamedColor",
  props: {
    namedColor: {},
  },
  methods: {
    toRGB() {
      var r = this.namedColor.color.r * 255;
      var g = this.namedColor.color.g * 255;
      var b = this.namedColor.color.b * 255;
      return `rgb(${r}, ${g}, ${b})`;
    },
    getFontColor(reverse = false) {
      var r = this.namedColor.color.r;
      var g = this.namedColor.color.g;
      var b = this.namedColor.color.b;
      var average = (r + g + b) / 3;
      if (reverse) {
        return average <= 0.5 ? "#FFFFFF" : "#000000";
      }
      return average > 0.5 ? "#FFFFFF" : "#000000";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#main-box {
  height: 15vh;
  width: 15vh;
  margin: 0.7vh;
  text-align: center;
  display: inherit;
  vertical-align: middle;
  padding: 3vh;
  border-radius: 1vh;
}

#outer-box {
  width: 100%;
  display: table;
  height: 14vh;
  overflow: hidden;
}

#inner-box {
  display: table-cell;
  vertical-align: middle;
}

#text-box {
  background: white;
  padding: 10px;
  padding-bottom: 15px;
  border-radius: 1vh;
}

#name-text {
  font-family: "RobotoSlab";
  font-size: 2vh;
}

@font-face {
  font-family: "RobotoSlab";
  src: local("RobotoSlab"),
    url(../fonts/RobotoSlab-Bold.ttf) format("truetype");
}
</style>
