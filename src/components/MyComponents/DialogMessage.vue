<template>
  <div class="dialog">
    <div class="dialog_box">
      <p class="dialog_title"  :class="classNext">{{ title }}</p>
      <div class="dialog_content" :class="classScroll">
        <div class="text_rule"><div v-html="content"></div></div>
        <div v-if="showBtn" class="dialog_btn flex_evenly">
          <div class="applyBtn cancelbtn" @click="backToHome">残忍拒绝</div>
          <div class="applyBtn comfirmbtn" @click="remainApply">继续申请</div>
        </div>
      </div>
    </div>
    <div class="dialog_icon" @click="dialogHide">
      <svg-icon iconClass="cancelDialog"></svg-icon>
    </div>
  </div>
</template>

<script>
import SvgIcon from '../SvgIcon.vue';
import router from '../../router/index';

export default {
  components: { SvgIcon },
  name: 'DialogMessage',
  props: ['classAno', 'show', 'paClassScroll'],
  data() {
    return {
      title: '',
      content: '',
      classNext: '',
      showBtn: false,
      classScroll: '',
    };
  },
  methods: {
    dialogHide() {
      this.remove();
    },
    backToHome() {
      this.remove();
      router.push({ name: 'ApplyHome' });
    },
    remainApply() {
      this.remove();
    },

  },
  watch: {
    classAno() {
      this.classNext = this.classAno;
      this.classScroll = this.paClassScroll;
      this.showBtn = this.show;
    },
  },

};
</script>

<style lang="less" scoped>
.warnText{
  color: #F44336;
}
.flex_center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.dialog {
  width: 100vw;
  height: 100vh;
  position: fixed;
  flex-direction:column;
  top: 0;
  left: 0;
  z-index: 11;
  background: rgba(0, 0, 0, 0.6);
  .flex_center;
  .dialog_box {
    width: 560px;
    padding: 40px 32px;
    background: #fff;
    border-radius: 10px;
    overflow-y: hidden;
    .dialog_title {
      height: 36px;
      //padding-bottom: 25px;
      max-height: 100%;
      font-size: 1rem;
      font-weight: bold;
      color: #f72539;
      .flex_center;
    }
    .dialogScroll{
      height: 800px !important;
    }
    .dialog_content {
      min-height: 30px;
      // margin-top: 30px;
      overflow-y: scroll;
      /*这里学到了一个解决弹框滚动的问题，父级元素设置一个高度，
      并设置-webkit-overflow-scrolling:touch;设置overflow；scroll，给子元素设置overflow；auto*/
      height: 90%;
      -webkit-overflow-scrolling:touch;  //解决滑动不顺畅
      &::-webkit-scrollbar {   //隐藏滚动条
        display: none;
      }

      font-size: .8rem;
      word-break: break-all;
      display: inline-block;
      width: 100%;
      .text_rule{
        height: auto;
        white-space: -moz-pre-wrap; /*Mozilla,since1999*/
        white-space: -pre-wrap; /*Opera4-6*/
        white-space: -o-pre-wrap; /*Opera7*/
        word-wrap: break-word; /*InternetExplorer5.5+*/
        line-height: 1.6em;
        font-family: inherit;
      }
      .dialog_btn{
        height: 75px;
        font-size: .875rem;
        line-height: 75px;
        margin-top:2em;
        .applyBtn{
          width: 35%;
          text-align: center;
          border-radius: 2rem;
        }
        .cancelbtn{
            background: #c9c7c7ad;
            color: inherit;
        }
        .comfirmbtn{
          background: #0c0808a1;
          color: #fff;
        }
      }
    }

    .dialog_btn_group {
      height: 90px;
      margin-top: 50px;
      border-top: 1px solid #e5e5e5;
      .flex_center;
      .cancel_btn,
      .confirm_btn {
        .flex_center;
        flex: 1 1 50%;
        height: 100%;
        font-size: 16px;
      }
      .cancel_btn{
        border-right: 1px solid #e5e5e5;
      }
      .confirm_btn {
        color: #f72539;
        // border-left: 1px solid #e5e5e5;
      }
    }
  }
  .dialog_icon{
    font-size: 1.2rem;
    margin: 1rem;
  }
}
</style>
