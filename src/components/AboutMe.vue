<template>
  <div class="AboutMe">
     <p>作者邮箱：2516629927@qq.com</p>
     <p>项目地址：https://github.com/zengpang/cnodeLite</p>
  </div>
</template>
<script>
   export default {
    name: "AboutMe",
    data(){

    },
    mounted(){
        console.log("加载");
    }
   }
</script>
<style scoped>
.AboutMe {
    background: white;
    width: 75%;
    height: 98%;
    margin: 10px auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
</style>