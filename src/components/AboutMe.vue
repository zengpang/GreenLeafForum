<template>
  <div class="AboutMe">
     <p></p>
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