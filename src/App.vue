<template>
  <div id="app"> 
    <keep-alive>
          <router-view v-if="$route.meta.keepalive "/>
    </keep-alive>
      <router-view v-if="!$route.meta.keepalive"></router-view>
  </div>

</template>

<style>
body{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  background-color: #f4f4f4;
}
p{
  margin: 0;
  
}
</style>
