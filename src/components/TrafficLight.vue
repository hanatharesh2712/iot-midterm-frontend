<template>
  <div id="traffic-light">
    <input
      type="radio"
      :name="`traffic-light-color-${index}-${$parent.$vnode.tag}`"
      id="color1"
      value="RED"
      v-model="currentLight"
      :disabled="!allowChangeLight"
    />
    <input
      type="radio"
      :name="`traffic-light-color-${index}-${$parent.$vnode.tag}`"
      id="color2"
      value="YELLOW"
      v-model="currentLight"
      :disabled="!allowChangeLight"
    />
    <input
      type="radio"
      :name="`traffic-light-color-${index}-${$parent.$vnode.tag}`"
      id="color3"
      value="GREEN"
      v-model="currentLight"
      :disabled="!allowChangeLight"
    />
  </div>
</template>

<style lang="scss" scoped>
$whole: #333;
$color1: #ff0000;
$color2: #ffff00;
$color3: #00ff00;

#traffic-light {
  display: flex;
  flex-direction: column;
  left: 50%;
  top: 50%;
  background-color: $whole;
  width: 120px;
  height: 320px;
  border-radius: 30px;
}

input {
  appearance: none;
  position: relative;
  left: 50%;
  width: 80px;
  height: 80px;
  margin-top: 20px;
  margin-left: -40px;
  background-color: grey;
  border-radius: 100%;
  display: block;
  &#color1 {
    background-color: darken($color1, 15%);
    &:checked {
      background-color: $color1;
      box-shadow: 0 0 6em lighten($color1, 10%);
    }
  }
  &#color2 {
    background-color: darken($color2, 15%);
    &:checked {
      background-color: $color2;
      box-shadow: 0 0 6em lighten($color2, 10%);
    }
  }
  &#color3 {
    background-color: darken($color3, 15%);
    &:checked {
      background-color: $color3;
      box-shadow: 0 0 6em lighten($color3, 10%);
    }
  }
}
</style>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
import { mapGetters } from "vuex";
import { TrafficLightColor } from "@/store";

@Component({
  computed: {
    ...mapGetters({
      trafficLights: "trafficLights"
    })
  }
})
export default class TrafficLight extends Vue {
  @Prop() private index!: number;
  @Prop({ required: false, default: false }) private allowChangeLight!: boolean;
  private trafficLights!: TrafficLightColor[];

  private get currentLight(): TrafficLightColor {
    return this.trafficLights[this.index];
  }

  private set currentLight(newValue: TrafficLightColor) {
    this.axios.post(`traffic-light/change-light/${this.index}`, {
      color: newValue
    });
  }
}
</script>