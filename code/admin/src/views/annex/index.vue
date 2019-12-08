<template>
  <div>
    <el-upload
      ref="upload"
      action="/"
      accept=".md"
      :before-upload="beforeUpload"
      :disabled="fileList.length !== 0"
      :default-file-list="fileList"
    >
      <el-button type="primary" :disabled="fileList.length !== 0">上传文件</el-button>
    </el-upload>

    {{ fileData }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      fileList: [],
      fileData: ''
    }
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
        const formerData = this.fileData
        // 将读取的结果赋值给fileData
        this.fileData = formerData + '\n' + cont
      }
      rd.readAsBinaryString(f)
    }
  }
}
</script>
