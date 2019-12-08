<template>
  <div class="container">
    <el-form ref="ruleForm" :model="form" label-width="80px" :rules="rules">

      <el-form-item>
        <el-button type="primary" @click="onSubmit('ruleForm', 1)">发布</el-button>
        <el-button type="info" @click="onSubmit('ruleForm', 0)">保存为草稿</el-button>
      </el-form-item>

      <el-form-item label="文章名" prop="title" required>
        <el-input
          v-model="form.title"
          type="text"
          placeholder="文章名，最大为50字"
          maxlength="50"
          show-word-limit
        />
      </el-form-item>

      <span v-show="headerStatus">

        <el-form-item label="副标题" label-width="80px">
          <el-input v-model="form.subtitle" placeholder="若为空则自动截取文章首部文字生成" />
        </el-form-item>

        <el-row>
          <el-col :span="8">
            <el-form-item label="发布时间" prop="time" required>
              <el-date-picker
                v-model="form.time"
                type="datetime"
                placeholder="选择发布时间"
                align="right"
                :picker-options="pickerOptions"
              />
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="允许评论">
              <el-switch v-model="form.comment" />
            </el-form-item>
          </el-col>
          <el-col :span="8">
            <el-form-item label="列表图片">
              <el-button>选择图片</el-button>
            </el-form-item>
          </el-col>
        </el-row>

        <el-form-item label="标签">
          <el-tag
            v-for="tag in dynamicTags"
            :key="tag"
            closable
            :disable-transitions="false"
            @close="handleClose(tag)"
          >{{ tag }}</el-tag>
          <el-input
            v-if="inputVisible"
            ref="saveTagInput"
            v-model="inputValue"
            class="input-new-tag"
            size="small"
            @keyup.enter.native="handleInputConfirm"
            @blur="handleInputConfirm"
          />
          <el-button v-else class="button-new-tag" size="small" @click="showInput">+ 新的标签</el-button>
        </el-form-item>
      </span>

      <el-form-item>
        <div class="hideHeader" @click="headerStatus = !headerStatus">
          <i :class="headerStatus ? 'el-icon-arrow-up':'el-icon-arrow-down'" />
          {{ headerStatus? '隐藏详细设置' : '展开详细设置' }}
        </div>
      </el-form-item>
    </el-form>

    <!-- 富文本编辑器 -->
    <div class="markdownEdit">
      <el-row :gutter="20">
        <el-col :span="12">
          <el-input v-model="input" type="textarea" :rows="50" placeholder="请使用markdown语法编写~" />
        </el-col>
        <el-col :span="12">
          <vue-markdown :source="input" />
        </el-col>
      </el-row>
    </div>
    <!-- 富文本编辑器 结束 -->
  </div>
</template>

<script>
import VueMarkdown from 'vue-markdown'
import Prism from 'prismjs'
import '../../../node_modules/prismjs/themes/prism.css'

export default {
  components: {
    VueMarkdown
  },
  data() {
    return {
      input: '### 请使用markdown语法编写~ 8-)',
      headerStatus: false,
      form: {
        title: '',
        subtitle: '',
        time: '',
        comment: true
      },
      rules: {
        title: [{ required: true, message: '请输入文章名', trigger: 'blur' }],
        time: [
          {
            type: 'date',
            required: true,
            message: '请选择发布时间',
            trigger: 'change'
          }
        ]
      },
      pickerOptions: {
        shortcuts: [
          {
            text: '今天',
            onClick(picker) {
              picker.$emit('pick', new Date())
            }
          },
          {
            text: '昨天',
            onClick(picker) {
              const date = new Date()
              date.setTime(date.getTime() - 3600 * 1000 * 24)
              picker.$emit('pick', date)
            }
          },
          {
            text: '一周前',
            onClick(picker) {
              const date = new Date()
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7)
              picker.$emit('pick', date)
            }
          }
        ]
      },
      dynamicTags: [],
      inputVisible: false,
      inputValue: ''
    }
  },
  updated() {
    Prism.highlightAll()
  },
  methods: {
    onSubmit(formName, status) {
      // 提交和保存 status: 0-保存为草稿 1-提交并发布
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert('submit!')
        } else {
          console.log('error submit!!')
          this.headerStatus = true
          return false
        }
      })
    },
    handleClose(tag) {
      this.dynamicTags.splice(this.dynamicTags.indexOf(tag), 1)
    },

    showInput() {
      this.inputVisible = true
      this.$nextTick(_ => {
        this.$refs.saveTagInput.$refs.input.focus()
      })
    },

    handleInputConfirm() {
      const inputValue = this.inputValue
      if (inputValue) {
        this.dynamicTags.push(inputValue)
      }
      this.inputVisible = false
      this.inputValue = ''
    }
  }
}
</script>

<style scoped>
div.markdownEdit {
  margin: 30px 10px;
}
div.hideHeader {
  text-align: right;
  margin-right: 20px;
}
.el-tag + .el-tag {
  margin-left: 10px;
}
.button-new-tag {
  margin-left: 10px;
  height: 32px;
  line-height: 30px;
  padding-top: 0;
  padding-bottom: 0;
}
.input-new-tag {
  width: 90px;
  margin-left: 10px;
  vertical-align: bottom;
}
</style>
