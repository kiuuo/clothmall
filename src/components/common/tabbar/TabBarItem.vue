<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
  export default {
    name: "TabBarItem",
    props: {
      path: String,
      //可以将颜色分离出来,传入什么颜色每个TabBarItem就是什么颜色
      color: {
        type: String,
        default: "#FF6666"
      }
    },
    data() {
      return {
        // isActive: false
      }
    },
    computed: {
      isActive() {
        //使用indexOf也可以检测到/home/xx之类的路径.
        return this.$route.path.indexOf(this.path) !== -1
      },
      activeStyle() {
        return this.isActive? {color: this.color} : {}
      }
    },
    methods: {
      itemClick() {
        this.$router.replace(this.path);
      }
    }
  }
</script>

<style scoped>
  .tab-bar-item{
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }

  .tab-bar-item img{
    margin-top: 4px;
    vertical-align: middle;
    color: red;
  }
</style>
