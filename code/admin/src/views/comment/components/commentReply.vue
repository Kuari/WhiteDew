<template>
  <div>
    <el-dialog title="回复评论" :visible.sync="dialogVisibleData">
      <div class="comment">
        <h3>{{ username }} :</h3>
        <p>{{ comment }}</p>
      </div>
      <div class="replay">
        <el-input
          type="textarea"
          :autosize="{ minRows: 2, maxRows: 4}"
          placeholder="回复"
          v-model="replay"
        ></el-input>
      </div>
      <div slot="footer" class="dialog-footer">
        <el-button @click="cancelReply">取 消</el-button>
        <el-button type="primary" @click="submitReply">回 复</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  props: {
    dialogVisible: {
      type: Boolean,
      default: false
    },
    username: {
      type: String
    },
    comment: {
      type: String
    }
  },
  data() {
    return {
      replay: "",
      formLabelWidth: "120px",
      dialogVisibleData: this.dialogVisible
    };
  },
  methods: {
    cancelReply() {
      this.replay = "";
      this.dialogVisibleData = false;
    },
    submitReply() {
      this.dialogVisibleData = false;
      console.log("heihei");
      this.replay = "";
    }
  },
};
</script>

<style scoped>
</style>