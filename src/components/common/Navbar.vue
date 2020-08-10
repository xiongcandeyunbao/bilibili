<template>
  <div class="navbar" >
      <div class="logo" @click="$router.push('/')">
          <img src="@/assets/logo.png" alt="">
      </div>
      <div>
          <p>
              请输入内容
              <van-icon class="ipt-icon" name="search" />
          </p>
      </div>
      <div>
            <img :src="imgUrl" alt="" @click="$router.push('/userinfo')" v-if="imgUrl">
            <img src="@/assets/default_img.jpg"  @click="$router.push('/login')" alt="" v-else >
            <p>下载App</p>
      </div>
  </div>
</template>

<script>
export default {
    data(){
        return {
            imgUrl:''
        }
    },
    async mounted(){
        if(localStorage.getItem('token')){
            const res=await this.$http.get('/user/' +localStorage.getItem('id'))    //发送请求
            this.imgUrl=res.data[0].user_img
        }
    }
}
</script>

<style lang="less">
.navbar{
    height: 12.5vw;
    background-color: white;
    display: flex;
    .logo{
        width: 30.556vw;
        display: flex;
        align-items: center;
        justify-content: center;
        img{
            width: 90%;
        }
    }
    div:nth-child(2){
        flex: 1;
        display: flex;
        align-items: center;
        margin: 0 1.389vw;
        p{
            font-size: 3.333vw;
            line-height: 7.222vw;
            position: relative;
            background-color: #f4f4f4;
            height: 6.389vw;
            width: 100%;
            border-radius: 3.611vw;
            padding-left: 6.944vw ;
            color: #aaa;
            .ipt-icon{
                position: absolute;
                left: 2.778vw;
                top: 50%;
                transform: translate(0,-40%);
                color: #aaa;
            }
        }
    }
    div:nth-child(3){
        display: flex;
        justify-content: center;
        align-items: center;
        img{
            width: 6.667vw;
            height: 6.667vw;
            border-radius: 50%;
        }
        p{
            padding: 1.389vw 2.778vw;
            margin: 0 2.222vw;
            background-color: #fb7299;
            color: white;
            border-radius: 0.833vw;
            font-size: 3.611vw;
        }
    }
}
</style>