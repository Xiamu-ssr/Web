<script lang="ts" setup>
import { ref, reactive, onMounted, computed } from "vue";
import type { TabsPaneContext } from 'element-plus'

const handleClick = (tab: TabsPaneContext, event: Event) => {
  console.log(tab, event)
}

var allteachers = require("../../json/team/brief.json")

allteachers.forEach((item, index, arr) => {
  // console.log(item.imageurl);
  item.imageurl = require("../../assets/" + item.imageurl)
  // console.log(item.imageurl);
});

const activeName = ref('first')

const handleSelect = () => {

}

onMounted(() => {

})
</script>

<template>
<el-space wrap size="large">
  <el-card style="margin: 10px;" v-for="teacher in allteachers" :key="teacher"  class="card-hover">
    <el-link :href="teacher.link"><el-image :src="teacher.imageurl" class="card-image"/></el-link>
      <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
        <el-tab-pane label="姓名" name="first" class="card-name-font">{{teacher.name}}</el-tab-pane>
        <el-tab-pane label="职位" name="second" class="card-title-font">{{teacher.qhu_title}}</el-tab-pane>
        <el-tab-pane label="联系方式" name="third" class="card-email-font">{{teacher.email}}</el-tab-pane>
      </el-tabs>
    <!-- <p><b class="card-name-font">{{teacher.name}}</b><span class="card-title-font">{{teacher.qhu_title}}</span></p>
    <br/>
    <p>{{teacher.email}}</p>-->
  </el-card>
</el-space>
</template>

<style scoped>
.card-image{
  height: 255px;
  width: 190px;
}
.card-name-font{
  font-weight: bold;
  font-size: 18px;
}
.card-title-font{
  font-weight: bold;
  font-size: 18px;
}
.card-email-font{
  font-weight: bold;
  font-size: 14px;
}
@keyframes example {
  0%   {transform: scale(1,1);}
  25%  {transform: scale(1.02,1.02);box-shadow: 0 0 2px 1px #0d6efd33;}
  50%  {transform: scale(1.04,1.04);box-shadow: 0 0 4px 2px #0d6efd66;}
  100% {transform: scale(1.06,1.06);box-shadow: 0 0 6px 3px #0d6efd99;}
}
.card-hover:hover{
    /* transition: transform 0.6s; */
    /* transform: scale(0.95,0.95); */
    animation-name: example;
    animation-duration: 0.3s;
    /* animation-iteration-count: 1; */
    animation-fill-mode: both;
}
</style>

