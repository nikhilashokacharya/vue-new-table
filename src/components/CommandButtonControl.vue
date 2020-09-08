<template>
  <div>
    <!-- <div class="btn-group">
      <button class="button" default>Alphabetic</button>
      <button class="button">Categorized</button>
    </div>
    <div v-for="data in commandButtonInfo" :key="data">
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
    </div> -->
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import { commandButtonData } from "../table/tableData/commandButtonData";
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
  components:{
    CustomInput,
    CustomDropDown,
    CustomColorTabs,
    CustomFontDialog
  }
})
export default class UserFormTable extends Vue {
  @Prop() selectedUserForm: any;
  commandButtonInfo = commandButtonData;

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
table {
  margin-right: 0%;
  width: 100%;
  border: 1px solid black;
  border-collapse: collapse;
  font-size: 11px;
  padding: none;
  color: black;
}

td {
  text-align: left;
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