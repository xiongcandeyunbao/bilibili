<template>
  <div @click="bannerClick">
      <div class="editbanner">
          <span>{{left}}</span>
          <span> <slot name="right"></slot></span>
      </div>
  </div>
</template>

<script>
export default {
    props:['left'],
    methods:{
        bannerClick(){
            this.$emit('bannerClick')
        }
    }
}
</script>

<style>
.editbanner{
    padding: 4.167vw ;
    background-color: white;
    border: 0.278vw solid #eee;
    font-size: 3.889vw;
    display: flex;
    color: #333;
    justify-content: space-between;
    align-items: center;
}
</style>