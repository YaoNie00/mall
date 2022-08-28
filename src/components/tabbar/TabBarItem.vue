<template>
  <div class="tab-bar-item" @click="Click">
    <div v-if="!isActive">
        <slot name="item-icon"></slot>
    </div>
    <div v-else>
        <slot name="item-icon-active"></slot>
    </div>
    <!-- 这样写样式不起效果  -->
    <!-- <slot :class="{ active: isActive }" name="item-text"></slot> -->
    <!-- 渲染的时候会直接把它这个替换成  <div slot="item-text">首页</div> -->
    <!-- 一般不会直接在插槽上绑定动态属性，因为渲染时会把它替换掉
     外面套一个div这样不会把原来的替换掉，上面两个最好也这样写  -->
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>

<script>
export default {
     props:{
        path:String,
        activeColor:{
          type:String,
          default:'red'
        }
    },
    data() {
        return {
            // isActive: true,
        }
    },
    computed:{
      isActive () {
        // 动态获取活跃的
        return this.$route.path.indexOf(this.path) !== -1
      },
      activeStyle () {
        // 动态的获取颜色
        return this.isActive ? { color: this.activeColor } : {}
      }
    },
   
    methods:{
        Click(){
          // 点击跳转页面
            console.log('Click');
            // this.$router.replace(this.path)
            this.$router.replace(this.path).catch(err => {})
        }
    }

}
</script>

<style>
.tab-bar-item{
  /* 设置导航栏样式 */
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}
.tab-bar-item img{
  width: 24px;
  height: 24px;
  margin-top: 3px;
  vertical-align: middle;
  margin-bottom: 2px;
}
</style>