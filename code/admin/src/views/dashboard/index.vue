<template>
  <div class="bg">
    <div class="dashBoardContainer">
      <div class="line">
        <panelGroup></panelGroup>
      </div>
      <div class="line panel">
        <lineChart />
      </div>
      <div class="line">
        <el-row :gutter="20">
          <el-col :span="8">
            <div class="panel">
              <pieChart />
            </div>
          </el-col>
          <el-col :span="8">
            <div class="panel">
              <histogram />
            </div>
          </el-col>
          <el-col :span="8">
            <div class="panel">
              <line-chart2 />
            </div>
          </el-col>
        </el-row>
      </div>
      <div class="line">
        <el-row :gutter="20">
          <el-col :span="12">
            <to-do-list />
          </el-col>
          <el-col :span="6">
            <recentComment />
          </el-col>
          <el-col :span="6">
            <optionlog />
          </el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
import panelGroup from "./components/panelGruop";
import pieChart from "./components/pieChart";
import lineChart from "./components/lineChart";
import histogram from "./components/Histogram";
import lineChart2 from "./components/lineChart2";

import recentComment from "../../components/PagePlugin/recentComment";
import toDoList from "./components/toDoList";
import optionlog from "./components/optionLog";

export default {
  name: "Dashboard",
  components: {
    panelGroup,
    pieChart,
    lineChart,
    histogram,
    lineChart2,
    recentComment,
    toDoList,
    optionlog
  }
};
</script>

<style scoped>
.panel {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  padding: 20px;
  background-color: white;
  height: 400px;
}
.line {
  margin-bottom: 20px;
}
div.bg {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  background-color: #f2f2f2;
}
.dashBoardContainer {
  padding: 30px;
}
</style>
