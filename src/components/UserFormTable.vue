<template>
  <div>
    <div class="btn-group">
      <button class="button" default>Alphabetic</button>
      <button class="button">Categorized</button>
    </div>
    <div v-for="data in userFormInfo" :key="data.labelName">
      <CustomInput
        v-if="data.type==='input'"
        :data="data"
        @input="input"
        @change="change"
        @keydown="keydown"
        @keyup="keydown"
        @keypress="keypress"
        @focus="focus"
        @blur="blur"
        @mouseout="mouseout"
      />
      <CustomDropDown
        v-if="data.type==='dropdown'"
        :data="data"
        @change="change"
        @focus="focus"
        @blur="blur"
      />
      <CustomColorTabs v-if="data.type==='color'" :data="data" @blur="blur" />
      <CustomFontDialog v-if="data.type==='font'" :data="data" />
    </div>
  </div>
</template>

<script lang="ts">
import { userFormData } from "../table/tableData/userFormData";
import { Component, Prop, Vue } from "vue-property-decorator";
import backColor from "../models/backColor.json";
import borderColor from "../models/borderColor.json";
import borderStyle from "../models/borderStyle.json";
import cycle from "../models/cycle.json";
import font from "../models/font.json";
import foreColor from "../models/foreColor.json";
import keepScrollsBarsVisible from "../models/keepScrollsBarsVisible.json";
import mousePointer from "../models/mousePointer.json";
import pictureAlignment from "../models/pictureAlignment.json";
import scrollBars from "../models/scrollBars.json";
import specialEffect from "../models/specialEffect.json";
import startUpPosition from "../models/startUpPosition.json";
import pictureSizeMode from "../models/pictureSizeMode.json";
/* import { validators } from "@/validators/validator.js"; */
import { Getter, Mutation } from "vuex-class";
import ColorPallate from "../views/table-design/ColorPallate.vue";
import FontDialog from "../views/table-design/FontDialog.vue";
import DropDown from "../views/table-design/DropDown.vue";
import CustomInput from "../table/CustomInput.vue";
import CustomDropDown from "../table/CustomDropDown.vue";
import CustomColorTabs from "../table/CustomColorTabs.vue";
import CustomFontDialog from "../table/CustomFontDialog.vue";

@Component({
  components: {
    ColorPallate,
    FontDialog,
    DropDown,
    CustomInput,
    CustomDropDown,
    CustomColorTabs,
    CustomFontDialog,
  },
  filters: {
    sizeFilter(value: any) {
      return parseInt(value, 10);
    },
  },
})
export default class UserFormTable extends Vue {
  @Prop() selectedUserForm: any;
  /*  validators: object = validators; */
  pictureSizeMode: object = pictureSizeMode;
  backColor: object = backColor;
  borderColor: object = borderColor;
  borderStyle: object = borderStyle;
  cycle: object = cycle;
  font: object = font;
  foreColor: object = foreColor;
  keepScrollsBarsVisible: object = keepScrollsBarsVisible;
  mousePointer: object = mousePointer;
  pictureAlignment: object = pictureAlignment;
  scrollBars: object = scrollBars;
  specialEffect: object = specialEffect;
  startUpPosition: object = startUpPosition;
  previousDrawBuffer = this.selectedUserForm.drawBuffer;
  previoushelpContextId = this.selectedUserForm.helpContextId;

  userFormInfo = userFormData;

  mounted() {}

  /*  @Getter selectedUserForm!: any */
  @Mutation updateStyle!: Function;
  @Mutation updatedInnerWindowStyle!: Function;

  handleChangeInput(e: any, styleName: string) {
    this.updateStyle({ styleValue: e.target.value, styleName: styleName });
  }
  /* ChangeInput(e: any, styleName: string)
{
  this.updatedInnerWindowStyle({styleValue:e.target.value,styleName:styleName})
  
} */

  drawBufferValidate(data: any) {
    if (data > 16000 && data <= 1048576) {
      this.selectedUserForm.drawBuffer = data;
    } else {
      this.selectedUserForm.drawBuffer = this.previousDrawBuffer;
    }
  }

  helpContextIdValidate(data: any): void {
    if (data > 2147000000) {
      this.selectedUserForm.helpContextId = this.previoushelpContextId;
    }
  }
  input(e: any, data: any) {
    console.log("@input Event value", e.target.value);
    data.value = e.target.value;
  }
  change(e: any, data: any) {
    console.log("@change Event value", e.target.value);
    data.value = e.target.value;
  }
  keydown(e: any, data: any) {
    console.log("@keydown Event value", e.target.value);
    data.value = e.target.value;
  }
  keyup(e: any, data: any) {
    console.log("@keyup Event value", e.target.value);
    data.value = e.target.value;
  }
  keypress(e: any, data: any) {
    console.log("@keypress Event value", e.target.value);
    data.value = e.target.value;
  }
  focus(e: any, data: any) {
    console.log("@focus Event value", e.target.value);
    data.value = e.target.value;
  }
  blur(e: any, data: any) {
    console.log("@blur Event value", e.target.value);
    data.value = e.target.value;
  }
  mouseout(e: any, data: any) {
    console.log("@mouseout Event value", e.target.value);
    data.value = e.target.value;
  }
}
</script>

<style scoped>
.node {
  text-align: left;
}
table {
  margin-right: 0%;
  /* width: 100%; */
  border: 1px solid black;
  border-collapse: collapse;
  font-size: 11px;
  font-display: initial;
  color: black;
}
th,
td {
  text-align: left;
  width: fit-content;
  position: relative;
}
th {
  width: 120%;
  font-size: 12px;
}

.form-control {
  float: left;
  width: 280px;
  cursor: pointer;
  background-color: rgb(190, 185, 185);
  /* border: 6px solid grey; */
}
label {
  float: left;
}
select {
  /* width: 166px; */
  width: 100%;
  padding: 1px 2px;
}
input {
  /* width: 158px; */
  width: 100%;
}

/* Must be added as style for the new data */
.btn-group .button {
  border: none;
  color: black;

  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  cursor: pointer;
  /* float: left; */
}
.btn-group .button {
  border: none;
  color: black;

  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 12px;
  cursor: pointer;
  /* float: left; */
}
.lefttd {
  width: 130px;
}
</style>