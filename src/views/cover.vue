<template>
  <!-- <div @click="$router.push('/detail/' +detailitem.id+'')"> -->
    <div  @click="pathPush">
        <div class="detailItem">
          <div class="imgparent">
            <img :src="detailitem.img" alt="" style="width:100%;height:100%">
            <div class="bottom">
              <div class="icon-play2"><span class="video">1233</span></div>
              <div class="icon-file-text"><span class="comment">{{!detailitem.commentlen?66:detailitem.commentlen}}</span></div>
            </div>
            <p>{{detailitem.name}}</p>
          </div>
        </div>
    </div>
  <!-- </div> -->
</template>

<script>
export default {
    props:['detailitem'],
    methods:{
      pathPush(){
        if(this.$route.path != `/article/${this.detailitem.id}`){
          this.$router.push(`/article/${this.detailitem.id}`)
        }
      }
    }
}
</script>

<style lang="less">
.detailItem{
  p{
    font-size: 3.333vw;
    padding: 0.833vw 0;
  }
  .imgparent{
    position: relative;
    .bottom{
        padding:  0 1.389vw;
        margin-bottom: 0.278vw;
        display: flex;
        left: 0;
        right: 0;
        justify-content: space-between;
        color: white;
        position: absolute;
        bottom: 6.944vw;
        background: linear-gradient(0deg,rgba(0,0,0,.85),transparent);
  }
  
}
}

</style>