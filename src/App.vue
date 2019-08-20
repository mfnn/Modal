<template>
  <div id="app">
    <button @click="open">打开模态框</button>
    <!-- 自定义模态框组件 -->
    <my-modal :dialogOption="dialogOption" v-show="isShow" ref="dialog" width="80%">
      <div slot="content">
        <label>用户名</label>
        <input type="text" placeholder="请输入用户名" v-model="username">
        <br>
        <label>密码</label>
        <input type="password" placeholder="请输入密码" v-model="password">
      </div>
    </my-modal>
  </div>
</template>

<script>
/* eslint-disable */
import MyModal from "./components/MyModal.vue";

export default {
  name: "app",
  components: {
    MyModal
  },
  data() {
    return {
      isShow: false,
      dialogOption: {
        title: "查看详情"
      },
      username: "",
      password: ""
    };
  },
  methods: {
    open() {
      this.isShow = true;
      this.$refs.dialog
        .confirm()
        .then(() => {
          this.isShow = false;
        })
        .catch(() => {
          this.isShow = false;
        });
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
