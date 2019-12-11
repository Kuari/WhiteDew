<template>
  <div class="container">
    <div class="btnGroup">
      <el-form :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="菜单名称">
          <el-input v-model="formInline.name" placeholder="菜单名" />
        </el-form-item>
        <el-form-item label="菜单类型">
          <el-select v-model="formInline.menuType" placeholder="菜单类型">
            <el-option label="页面" value="page" />
            <el-option label="分类" value="classification" />
            <el-option label="链接" value="link" />
          </el-select>
        </el-form-item>

        <span v-if="formInline.menuType === 'page'">
          <el-form-item label="页面选择">
            <el-select v-model="formInline.value" placeholder="请选择页面">
              <el-option label="首页" value="home" />
              <el-option label="关于" value="about" />
            </el-select>
          </el-form-item>
        </span>
        <span v-else-if="formInline.menuType === 'link'">

          <el-form-item label="链接">
            <el-input v-model="formInline.value" placeholder="链接" />
          </el-form-item>
        </span>
        <span v-else-if="formInline.menuType === 'classification'">

          <el-form-item label="分类">
            <el-select v-model="formInline.value" placeholder="请选择分类">
              <span v-for="item in classification" :key="item">
                <el-option :label="item" :value="item" />
              </span>
            </el-select>
          </el-form-item>
        </span>

        <el-form-item>
          <el-button type="primary" :disabled="disableAddMenuBtn" @click="addMenu">添加</el-button>
        </el-form-item>
      </el-form>
    </div>

    <div class="menuGrapGroup">

      <div v-if="lists.length > 0">
        <draggable v-model="lists">
          <transition-group>
            <div v-for="(item, index) in lists" :key="item.name">
              <el-card shadow="never" class="card">
                <span class="cardOption"><i class="el-icon-rank" /></span>
                {{ item.name }} <span class="menuSubInfo">{{ item.menuType }} - {{ item.value.length>10? item.value.slice(0, 10) + '...' : item.value }}</span>
                <span class="cardDelete"><i class="el-icon-delete" @click="deleteMenu(index)" /></span>
              </el-card>
            </div>
          </transition-group>
        </draggable>
      </div>
      <div v-else>
        <div class="noDataInfo">你还没有创建菜单。</div>
      </div>
    </div>

    <el-button type="primary" :disabled="lists.length===0">保 存</el-button>

  </div>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  components: {
    draggable
  },
  data() {
    return {
      lists: [
        {
          name: 'Home',
          menuType: 'page',
          value: 'home'
        },
        {
          name: 'menu1',
          menuType: 'page',
          value: 'about'
        },
        {
          name: 'menu2',
          menuType: 'page',
          value: 'home'
        }
      ],
      formInline: {
        name: '',
        menuType: '',
        value: ''
      },
      classification: [
        '宋词1', '宋词2', '宋词3'
      ]
    }
  },
  computed: {
    disableAddMenuBtn() {
      if (this.formInline.name && this.formInline.menuType && this.formInline.value) return false
      return true
    }
  },
  methods: {
    deleteMenu(menuId) {
      this.lists.splice(menuId, 1)
    },
    onSubmit() {
      console.log('submit')
    },
    addMenu() {
      var formData = {}
      formData['name'] = this.formInline.name
      formData['menuType'] = this.formInline.menuType
      formData['value'] = this.formInline.value
      this.lists.push(formData)
      this.formInline.name = ''
      this.formInline.menuType = ''
      this.formInline.value = ''
    }
  }
}
</script>

<style scoped>
.cardOption {
    float: left;
    margin-right: 10px;
}
.cardDelete {
  float: right;
  margin-right: 10px;
}
.cardDelete:hover {
  color: rgb(223, 70, 70);
}
div.btnGroup {
  margin-bottom: 20px;
}
div.menuGrapGroup {
  margin-bottom: 20px;
  padding-right: 50%;
}
.menuSubInfo {
  color: #c4c2c2;
  margin-left: 20px;
}
.noDataInfo {
  padding: 20px;
    color: #c4c2c2;
  margin-left: 20px;
}
</style>
