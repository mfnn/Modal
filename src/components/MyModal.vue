<template>
  <div class="dialog">
    <div class="mask"></div>
    <div class="dialog-content">
      <!-- 标题 -->
      <h3 class="title">{{ modal.title }}</h3>
      <!-- 自定义内容 -->
      <slot name="content"></slot>
      <!-- 按钮组 -->
      <div class="btn-group">
        <div class="btn" @click="cancel">{{ modal.cancelButtonText }}</div>
        <div class="btn" @click="submit">{{ modal.confirmButtonText }}</div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: "MyModal",
  props: {
    dialogOption: Object
  },
  data() {
    return {
      resolve: "",
      reject: "",
      promise: "" //保存promise对象
    };
  },
  computed: {
    modal() {
      let option = this.dialogOption;
      return {
        title: option.title || "提示",
        text: option.text,
        cancelButtonText: option.cancelButtonText
          ? option.cancelButtonText
          : "取消",
        confirmButtonText: option.confirmButtonText
          ? option.confirmButtonText
          : "确定"
      };
    }
  },
  methods: {
    //确定,将promise断定为完成态
    submit() {
      this.resolve();
    },
    // 取消,将promise断定为reject状态
    cancel() {
      this.reject();
    },
    //显示confirm弹出,并创建promise对象，给父组件调用
    confirm() {
      this.promise = new Promise((resolve, reject) => {
        console.log(resolve, reject);
        this.resolve = resolve;
        this.reject = reject;
      });
      return this.promise; //返回promise对象,给父级组件调用
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.dialog {
  position: relative;
  .dialog-content {
    position: fixed;
    z-index: 2;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    box-sizing: border-box;
    background: white;
    border-radius: 5px;
    padding: 20px;
    min-height: 140px;
    .title {
      font-size: 16px;
      font-weight: 600;
      line-height: 30px;
    }
    .text {
      font-size: 14px;
      line-height: 30px;
      color: #555;
    }
    .btn-group {
      display: flex;
      position: absolute;
      right: 0;
      bottom: 10px;
      .btn {
        padding: 10px 20px;
        font-size: 14px;
        &:last-child {
          color: #76d49b;
        }
      }
    }
  }
  .mask {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    z-index: 1;
  }
}
</style>
