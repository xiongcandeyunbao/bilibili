<template>
  <div class="commentitems">
    <div class="commentItem" v-for="(item ,index) in commentChild" :key="index">
      <div class="userImg">
        <img v-if="item.userinfo.user_img" :src="item.userinfo.user_img" alt />
          <img v-else src="@/assets/default_img.jpg" alt="">
           <p>
            <span v-if="item.userinfo">{{item.userinfo.name}}</span>
            <span v-else>此用户无姓名</span>
            <span>{{item.comment_date}}</span>
        </p>
      </div>
      <div class="commentContent">
       
        <div v-if="!temp">
          {{item.comment_content}} 
          <span class="publish"  @click="PostItemcomment(item.comment_id)">
            回复
          </span>
        </div>
        <div v-else>
         回复<span style="color:#478ef0">{{item.parent_user_info.name}}</span>: {{item.comment_content}}
         <span class="publish"  @click="PostItemcomment(item.comment_id)">回复</span>
        </div>
      </div>
      <commentchild-item :commentChild="item.child" @postchild="postchild" :temp="true"></commentchild-item>
    </div>
  </div>
</template>

<script>
export default {
  name:'commentchildItem',
  props: ["commentChild",'temp'],
  methods:{
    PostItemcomment(id){
      this.$emit('postchild',id)
      this.$emit('PostPublish',id)
    },
    postchild(id){
      this.PostItemcomment(id)
      this.$emit('PostPublish',id)
    }
  }
};
</script>

<style lang="less">
.commentitems {

  .commentItem{
    display: flex;
    flex-direction: column;
    .userImg{
      display: flex;
      img{
        margin: 0 5px 10px ;
      }
      p{
        display: flex;
        color: #555;
        justify-content: space-between;
        font-size: 3.611vw;
        margin-bottom: 1.389vw;
        flex: 1;
        align-items: center;
      }
    }
  }
}
.commentContent{
  position: relative;
  margin-bottom: 1.778vw;
  .publish{
    color: red;
    position: absolute;
    right: 4.167vw;
  }
}
</style>