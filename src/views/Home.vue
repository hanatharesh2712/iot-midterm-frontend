<template>
  <div class="tab_container">
    <input id="tab1" type="radio" name="tabs" checked @click="changeMode('MANUAL')" />
    <label for="tab1">
      <i class="fa fa-wrench"></i>
      <span>Mannual Mode</span>
    </label>

    <input id="tab2" type="radio" name="tabs" @click="changeMode('AUTO')" />
    <label for="tab2">
      <i class="fa fa-pencil-square-o"></i>
      <span>Auto Mode</span>
    </label>

    <input id="tab3" type="radio" name="tabs" @click="changeMode('SENSOR')" />
    <label for="tab3">
      <i class="fa fa-bar-chart-o"></i>
      <span>Sensor Mode</span>
    </label>

    <input id="tab4" type="radio" name="tabs" />
    <label for="tab4">
      <i class="fa fa-code"></i>
      <span>Debug Mode</span>
    </label>

    <input id="tab5" type="radio" name="tabs" />
    <label for="tab5">
      <i class="fa fa-users"></i>
      <span>Group Members</span>
    </label>

    <section id="content1" class="tab-content">
      <MannualModeControlSet />
    </section>

    <section id="content2" class="tab-content">
      <AutoModeControlSet />
    </section>

    <section id="content3" class="tab-content">
      <SensorModeControlSet />
    </section>

    <section id="content4" class="tab-content">
      <DebugModeControlSet />
    </section>

    <section id="content5" class="tab-content">
      <h1>
        Chutipon Hirankanokkul
        <i>5931239021</i>
        ICE 4
        <sup>th</sup>
      </h1>
      <h1>
        Worradorn Putraserani
        <i>5931338521</i>
        ADME 4
        <sup>th</sup>
      </h1>
    </section>
  </div>
</template>

<style lang="scss" scoped>
@import url("https://maxcdn.bootstrapcdn.com/font-awesome/4.4.0/css/font-awesome.min.css");

*,
*:after,
*:before {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

.clearfix:before,
.clearfix:after {
  content: " ";
  display: table;
}

.clearfix:after {
  clear: both;
}

body {
  font-family: sans-serif;
  background: #f6f9fa;
}

/*Fun begins*/
.tab_container {
  width: 100%;
  margin: 0 auto;
  position: relative;
}

input,
section {
  clear: both;
  padding-top: 10px;
  display: none;
}

label {
  font-weight: 700;
  font-size: 18px;
  display: block;
  float: left;
  width: 20%;
  padding: 1.5em;
  color: #757575;
  cursor: pointer;
  text-decoration: none;
  text-align: center;
  background: #f0f0f0;
}

#tab1:checked ~ #content1,
#tab2:checked ~ #content2,
#tab3:checked ~ #content3,
#tab4:checked ~ #content4,
#tab5:checked ~ #content5 {
  display: block;
  padding: 20px;
  background: #fff;
  color: #999;
  border-bottom: 2px solid #f0f0f0;
}

.tab_container .tab-content * {
  -webkit-animation: fadeInScale 0.7s ease-in-out;
  -moz-animation: fadeInScale 0.7s ease-in-out;
  animation: fadeInScale 0.7s ease-in-out;
}
.tab_container .tab-content h3 {
  text-align: center;
}

.tab_container [id^="tab"]:checked + label {
  background: #fff;
  box-shadow: inset 0 3px #0ce;
}

.tab_container [id^="tab"]:checked + label .fa {
  color: #0ce;
}

label .fa {
  font-size: 1.3em;
  margin: 0 0.4em 0 0;
}

/*Media query*/
@media only screen and (max-width: 900px) {
  label span {
    display: none;
  }

  .tab_container {
    width: 98%;
  }
}

/*Content Animation*/
@keyframes fadeInScale {
  0% {
    transform: scale(0.9);
    opacity: 0;
  }

  100% {
    transform: scale(1);
    opacity: 1;
  }
}
</style>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import MannualModeControlSet from "@/components/ManualModeControlSet.vue";
import AutoModeControlSet from "@/components/AutoModeControlSet.vue";
import SensorModeControlSet from "@/components/SensorModeControlSet.vue";
import DebugModeControlSet from "@/components/DebugModeControlSet.vue";
import { TrafficLightSystemMode } from "@/store";

@Component({
  components: {
    MannualModeControlSet,
    AutoModeControlSet,
    SensorModeControlSet,
    DebugModeControlSet
  }
})
export default class Home extends Vue {
  private changeMode(mode: TrafficLightSystemMode) {
    this.axios.post(`traffic-light/mode`, { mode });
  }
}
</script>
