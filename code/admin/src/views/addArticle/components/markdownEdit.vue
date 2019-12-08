<template>
  <div>
    <div id="markdownEdit" class="markdownEdit">
      <div class="editHeader">

        <el-row :gutter="10">
          <el-col :span="1">
            <el-tooltip content="全屏" placement="top">
              <a @click="screenFull">
                <svg-icon icon-class="fullscreen" />
              </a>
            </el-tooltip>
          </el-col>
          <el-col :span="1">
            <el-tooltip content="导入md文件" placement="top">
              <el-upload
                ref="upload"
                action="/"
                accept=".md"
                :before-upload="beforeUpload"
                :disabled="fileList.length !== 0"
                :default-file-list="fileList"
              >
                <a>
                  <svg-icon icon-class="upload" />
                </a>
              </el-upload>
            </el-tooltip>
          </el-col>
          <el-col :span="1">
            <el-tooltip content="预览" placement="top">
              <a @click="previewStatus = !previewStatus">
                <span v-if="previewStatus">
                  <svg-icon icon-class="eye-open" style="fill: #2c2c2c;" />
                </span>
                <span v-else>
                  <svg-icon icon-class="eye" style="fill: #2c2c2c;" />
                </span>
              </a>
            </el-tooltip>
          </el-col>
          <el-col :span="1">
            <el-tooltip content="markdown语法提示" placement="top">
              <a>
                <svg-icon icon-class="tip" />
              </a>
            </el-tooltip>
          </el-col>
        </el-row>

      </div>
      <el-row>
        <el-col :span="previewStatus ? 12 : 24">
          <!-- markdown编辑处 -->
          <div class="input">
            <el-input
              v-model="input"
              type="textarea"
              :rows="50"
              placeholder="请使用markdown语法在此处编写正文~"
            />
          </div>
          <!-- markdown编辑处 结束 -->
        </el-col>
        <el-col v-if="previewStatus" :span="12">
          <!-- 输出 -->
          <div class="output">
            <vue-markdown :source="input" />
          </div>
          <!-- 输出 结束 -->
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
import VueMarkdown from 'vue-markdown'
import Prism from 'prismjs'
import '../../../../node_modules/prismjs/themes/prism.css'
import screenfull from 'screenfull'

export default {
  components: {
    VueMarkdown
  },
  data() {
    return {
      input: '### 请使用markdown语法在此处编写正文~ 8-)',
      isFullscreen: false,
      fileList: [],
      previewStatus: true
    }
  },
  updated() {
    Prism.highlightAll()
  },
  beforeCreate() {
    // 读取文件
    FileReader.prototype.reading = function({ encode }) {
      const bytes = new Uint8Array(this.result) // 无符号整型数组
      const text = new TextDecoder(encode || 'UTF-8').decode(bytes)
      return text
    }
    /* 重写readAsBinaryString函数 */
    FileReader.prototype.readAsBinaryString = function(f) {
      if (!this.onload) {
        // 如果this未重写onload函数，则创建一个公共处理方式
        this.onload = e => {
          // 在this.onload函数中，完成公共处理
          const rs = this.reading()
          console.log(rs)
        }
      }
      this.readAsArrayBuffer(f) // 内部会回调this.onload方法
    }
  },
  methods: {
    screenFull() {
      const element = document.getElementById('markdownEdit')
      if (screenfull.isEnabled) screenfull.toggle(element)
    },
    beforeUpload(file) {
      this.fileList = [file]
      // 读取数据
      this.read(file)
      return false
    },
    read(f) {
      const rd = new FileReader()
      rd.onload = e => {
        // this.readAsArrayBuffer函数内，会回调this.onload函数。在这里处理结果
        const cont = rd.reading({ encode: 'GBK' })
        console.log(cont)
        const formerData = this.input
        // 将读取的结果赋值给fileData
        this.input = formerData + '\n' + cont
      }
      rd.readAsBinaryString(f)
    }
  }
}
</script>

<style>
div.input textarea.el-textarea__inner {
    border: none;
    background-color: #f2f2f2;
}
</style>

<style scoped>
div.markdownEdit {
    background-color: white;
}
div.editHeader {
  height: 30px;
  width: 100%;
  padding: 5px 10px;
  margin-bottom: 5px;
}
div.editHeader a {
  padding: 5px 12px;
  display: block;
  text-align: center;
}
div.editHeader a:hover {
  background-color: #DCDFE6;
}
div.input,
div.output {
    border-top: 1px solid #DCDFE6;
    padding: 10px 20px;
}
div.input {
  background-color: #f2f2f2;
}
</style>
