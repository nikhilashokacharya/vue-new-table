<template>
  <div>
    <div class="btn-group">
      <button class="button" default>Alphabetic</button>
      <button class="button">Categorized</button>
    </div>
    <div v-for="data in labelInfo" :key="data.labelName">
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
import { EventBus } from "../components/event-bus";
import { Component, Prop, Vue } from "vue-property-decorator";
import { LabelData } from "../table/tableData/labelData";
import { CommandButtonData } from "../table/tableData/commandButtonData";
import { userFormData } from "../models/UserFormData";
import { Mutation, Getter } from "vuex-class";
import CustomInput from "../table/CustomInput.vue";
import CustomDropDown from "../table/CustomDropDown.vue";
import CustomColorTabs from "../table/CustomColorTabs.vue";
import CustomFontDialog from "../table/CustomFontDialog.vue";
@Component({
  filters: {
    sizeFilter(value: any) {
      return parseInt(value, 10);
    },
  },
  components: {
    CustomInput,
    CustomDropDown,
    CustomColorTabs,
    CustomFontDialog,
  },
})
export default class UserFormTable extends Vue {
  @Prop() selectedUserForm: any;
  selectedOption: any;

  labelInfo: any = [];

  mounted() {
    const that = this;
    EventBus.$on("CallControl", (userForm: object, control: object) => {
      debugger
      that.selectedUserForm = userForm;
      that.selectedOption = control;
      if (that.selectedOption.type === "Label") {
        const labelObject = new LabelData();
        that.labelInfo = labelObject.data
      }
      if (that.selectedOption.type === "CommandButton") {
        debugger;
        const commandButtonObject = new CommandButtonData();
        that.labelInfo = commandButtonObject.data;
      }
      for (const key1 in userFormData.ID_USERFORM1.controls[0].properties) {
        for (let i = 0; i < that.labelInfo.length; i++) {
          if (that.labelInfo[i].labelName === key1) {
            userFormData.ID_USERFORM1.controls[0].properties[
              key1
            ] = that.labelInfo[i].value;
          }
        }
      }

      console.log("this is selected option", that.selectedOption);
      console.log(
        "this is Label Info",
        userFormData.ID_USERFORM1.controls[0].properties
      );
    });

    console.log("testing", userFormData.ID_USERFORM1.controls[0].properties);
    const data: any = {};
    console.log("bating", this.labelInfo);
  }
  input(e: any, data: any) {
    console.log("@input Event value", e.target.value);
    data.value = e.target.value;
    console.log("ID checker outside", this.selectedOption.id);
    if (
      userFormData.ID_USERFORM1.controls[0].properties.ID ===
      this.selectedOption.id
    ) {
      console.log("ID checker", this.selectedOption.id);
      userFormData.ID_USERFORM1.controls[0].properties[data.labelName] =
        data.value;
    }
    console.log("main data", userFormData.ID_USERFORM1.controls[0].properties);
  }
  change(e: any, data: any) {
    console.log("@change Event value", e.target.value);
    data.value = e.target.value;
    if (
      userFormData.ID_USERFORM1.controls[0].properties.ID ===
      this.selectedOption.id
    ) {
      console.log("ID checker", this.selectedOption.id);
      userFormData.ID_USERFORM1.controls[0].properties[data.labelName] =
        data.value;
    }
    console.log("main data", userFormData.ID_USERFORM1.controls[0].properties);
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
    if (
      userFormData.ID_USERFORM1.controls[0].properties.ID ===
      this.selectedOption.id
    ) {
      console.log("ID checker", this.selectedOption.id);
      userFormData.ID_USERFORM1.controls[0].properties[data.labelName] =
        data.value;
    }
    console.log("main data", userFormData.ID_USERFORM1.controls[0].properties);
  }
  mouseout(e: any, data: any) {
    console.log("@mouseout Event value", e.target.value);
    data.value = e.target.value;
    if (
      userFormData.ID_USERFORM1.controls[0].properties.ID ===
      this.selectedOption.id
    ) {
      console.log("ID checker", this.selectedOption.id);
      userFormData.ID_USERFORM1.controls[0].properties[data.labelName] =
        data.value;
    }
    console.log("main data", userFormData.ID_USERFORM1.controls[0].properties);
  }
}
</script>




<style scoped>
.node {
  text-align: left;
}
table {
  /* table-layout: fixed; */
  margin-right: 0%;
  width: 100%;
  border: 1px solid black;
  border-collapse: collapse;
  color: black;
}
th,
td {
  text-align: left;
  font-size: 11px;
  margin-right: 0%;
  width: fit-content;
  border: 1px solid black;
  border-collapse: collapse;
  color: black;
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
  width: 100%;
  /* width: 166px; */
  padding: 1px 2px;
}
input {
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
  width: 120px;
}
</style>