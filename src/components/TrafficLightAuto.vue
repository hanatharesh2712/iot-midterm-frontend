<template>
  <div class="traffic-light-container">
    <h2>Light {{index + 1}}</h2>
    <p>Countdown: {{counterString}}</p>
    <TrafficLight :index="index"></TrafficLight>
    <!-- <div class="input-container">
      <div class="group">
        <input type="text" required />
        <span class="highlight"></span>
        <span class="bar"></span>
        <label>Countdown</label>
      </div>
    </div> -->
  </div>
</template>

<style lang="scss" scoped>
.traffic-light-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}
* {
  box-sizing: border-box;
}

.input-container {
  font-family: "Roboto";
  margin: 30px auto 0;
  display: block;
  background: #fff;
}
h2 {
  text-align: center;
  margin-bottom: 50px;
}
h2 small {
  font-weight: normal;
  color: #888;
  display: block;
}
.footer {
  text-align: center;
}
.footer a {
  color: #53b2c8;
}

/* form starting stylings ------------------------------- */
.group {
  position: relative;
  margin-bottom: 45px;
}
input {
  font-size: 18px;
  padding: 10px 10px 10px 5px;
  display: block;
  width: 300px;
  border: none;
  border-bottom: 1px solid #757575;
}
input:focus {
  outline: none;
}

/* LABEL ======================================= */
label {
  color: #999;
  font-size: 18px;
  font-weight: normal;
  position: absolute;
  pointer-events: none;
  left: 5px;
  top: 10px;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}

/* active state */
input:focus ~ label,
input:valid ~ label {
  top: -20px;
  font-size: 14px;
  color: #5264ae;
}

/* BOTTOM BARS ================================= */
.bar {
  position: relative;
  display: block;
  width: 300px;
}
.bar:before,
.bar:after {
  content: "";
  height: 2px;
  width: 0;
  bottom: 1px;
  position: absolute;
  background: #5264ae;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}
.bar:before {
  left: 50%;
}
.bar:after {
  right: 50%;
}

/* active state */
input:focus ~ .bar:before,
input:focus ~ .bar:after {
  width: 50%;
}

/* HIGHLIGHTER ================================== */
.highlight {
  position: absolute;
  height: 60%;
  width: 100px;
  top: 25%;
  left: 0;
  pointer-events: none;
  opacity: 0.5;
}

/* active state */
input:focus ~ .highlight {
  -webkit-animation: inputHighlighter 0.3s ease;
  -moz-animation: inputHighlighter 0.3s ease;
  animation: inputHighlighter 0.3s ease;
}

/* ANIMATIONS ================ */
@-webkit-keyframes inputHighlighter {
  from {
    background: #5264ae;
  }
  to {
    width: 0;
    background: transparent;
  }
}
@-moz-keyframes inputHighlighter {
  from {
    background: #5264ae;
  }
  to {
    width: 0;
    background: transparent;
  }
}
@keyframes inputHighlighter {
  from {
    background: #5264ae;
  }
  to {
    width: 0;
    background: transparent;
  }
}
</style>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
import TrafficLight from "@/components/TrafficLight.vue";
import { mapGetters } from "vuex";

@Component({
  components: {
    TrafficLight
  },
  computed: {
    ...mapGetters({
      trafficLightCounter: "trafficLightCounter"
    })
  }
})
export default class TrafficLightAuto extends Vue {
  @Prop() private index!: number;
  private trafficLightCounter!: number[];

  private get counterString(): string {
    if (this.trafficLightCounter[this.index] === -1) {
      return "-";
    } else {
      return `${this.trafficLightCounter[this.index]}`;
    }
  }
}
</script>