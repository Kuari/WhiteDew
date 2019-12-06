<template>
  <div class="toListPanel">
    <!-- 输入框 -->
    <div class="pushList" @keyup.enter="addTask">
      <input type="text" placeholder="To Do" class="toDoInput" v-model="task" />
    </div>
    <!-- 输入框 结束-->
    <div v-for="(item, index) in lists" :key="index">
      <div v-if="item.show">
        <el-row class="listitem">
          <!-- 任务完成的选择框 -->
          <el-col :span="4">
            <div @click="finishTask(item.task)">
              <div v-if="item.finish">
                <svg-icon icon-class="checkmark-circle-out" />
              </div>
              <div v-else>
                <svg-icon icon-class="clock-circle-o" />
              </div>
            </div>
          </el-col>
          <!-- 任务完成的选择框 结束-->

          <!-- 任务名 -->
          <el-col :span="16">
            <!-- 双击时候可以编辑 -->
            <div v-if="item.edit">
              <el-input class="editInput" v-model="item.task">
                <el-button slot="append" icon="el-icon-check" @click="editTask(item.task)"></el-button>
              </el-input>
            </div>
            <div v-else>
              <span
                :class="{ taskFinishText : item.finish }"
                @dblclick="editTask(item.task)"
              >{{ item.task | taskNameLength }}</span>
            </div>
          </el-col>
          <!-- 删除键 -->
          <el-col :span="4">
            <div class="delete">
              <a>
                <svg-icon icon-class="delete" @click="deleteTask(item.task)" />
              </a>
            </div>
          </el-col>
        </el-row>
        <hr style="color: #f2f2f2;" />
      </div>
    </div>
    <!-- 面板尾部 todo信息 -->
    <div class="toDoFooter">
      <p>共 {{ taskNumber }} 个任务</p>
    </div>
    <!-- 面板尾部 todo信息 结束 -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: "",
      taskNumber: 0,
      lists: [
        {
          task: "白露接口文档",
          finish: true,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发1",
          finish: true,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发2",
          finish: false,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发3",
          finish: false,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发4",
          finish: false,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发5",
          finish: false,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发6",
          finish: false,
          show: true,
          edit: false
        },
        {
          task: "后台页面开发7",
          finish: false,
          show: true,
          edit: false
        }
      ]
    };
  },
  methods: {
    fetchData() {
      this.taskNumber = this.lists.length;
    },
    addTask() {
      // 添加todo任务
      if (this.task) {
        this.lists.push({
          task: this.task,
          finish: false,
          show: true
        });
        this.task = "";
        this.taskNumber += 1;
      } else {
        this.$message("任务不能为空");
      }
    },
    deleteTask(task) {
      // 删除task任务
      this.lists.forEach((item, index) => {
        if (item.task == task) {
          this.lists[index].show = false;
          this.taskNumber -= 1;
        }
      });
    },
    finishTask(task) {
      // 完成任务
      this.lists.forEach((item, index) => {
        if (item.task == task) {
          this.lists[index].finish = !this.lists[index].finish;
        }
      });
    },
    editTask(task) {
      // 开启编辑任务
      this.lists.forEach((item, index) => {
        if (item.task == task) {
          this.lists[index].edit = !this.lists[index].edit;
        }
      });
    }
  },
  filters: {
    taskNameLength(value) {
      if (value.length > 20) return value.substring(0, 20) + "...";
      return value;
    }
  },
  mounted() {
    this.fetchData()
  }
};
</script>

<style scoped>
div.toListPanel {
  border-radius: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
  padding: 20px;
  background-color: white;
  width: 100%;
  color: #606266;
}
div.delete {
  display: none;
  text-align: right;
  padding-right: 10px;
}
div.listitem {
  padding: 13px 10px;
}
div.listitem:hover div.delete {
  display: block;
}
input.toDoInput {
  padding: 15px 10px;
  width: 100%;
  border: none;
  border-bottom: 1px solid #f2f2f2;
}
input.toDoInput:hover {
  border-bottom: 1px solid black;
}
div.toDoFooter {
  font-size: 12px;
}
.taskFinishText {
  color: #d9d9d9;
  text-decoration-line: line-through;
}
.editInput {
  /* padding: 15px 10px; */
  width: 100%;
}
</style>