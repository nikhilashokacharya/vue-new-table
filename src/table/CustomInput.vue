<template>
  <div class="custom-input-outer">
    <label class="custom-label-ele">{{data.labelName}}</label>
    <input
      class="custom-input-ele"
      :value="data.value"
      :type="data.subType"
      @input="input($event,data)"
      @change="change($event,data)"
      @keydown="keydown($event,data)"
      @keyup="keyup($event,data)"
      @keypress="keypress($event,data)"
      @focus="focus($event,data)"
      @blur="blur($event,data)"
      @mouseout="mouseout($event,data)"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";
@Component({
  components: {},
})
export default class CustomInput extends Vue {
  @Prop() data: any;

  input(e: any, data: any) {
    this.$emit("input", e, data);
  }
  change(e: any, data: any) {
    this.$emit("change", e, data);
  }
  keydown(e: any, data: any) {
    this.$emit("keydown",e, data);
  }
  keyup(e: any, data: any) {
    this.$emit("keyup",e, data);
  }
  keypress(e: any, data: any) {
    this.$emit("keypress",e, data);
  }
  focus(e: any, data: any) {
    this.$emit("focus",e, data);
  }
  blur(e: any, data: any) {
    this.$emit("blur",e, data);
  }
  mouseout(e: any, data: any) {
    this.$emit("mouseout",e, data);
  }
}
</script>

<style scoped>
.custom-input-outer {
  /* border: 1px solid lightgray; */
  position: relative;
  width: 100%;
  display: grid;
  grid-template-columns: 100px 1fr;
}
.custom-label-ele {
  outline: none;
  border: 0.1px solid lightgray;
  font-size: 12px;
  position: inherit;
}
.custom-input-ele {
  border: 0.1px solid lightgray;
  outline: none;
  font-size: 12px;
}
</style>