<template>
  <div class="userdetail">
    <div>
      <div class="user_img">
        <img :src="userInfo.user_img" alt="" v-if="userInfo.user_img">
        <img src="@/assets/default_img.jpg" alt v-else />
      </div>
      <div class="user_edit">
        <div>
          <p>
            <span>0</span>
            <span class="user_text">粉丝</span>
          </p>
          <p>
            <span>54</span>
            <span class="user_text">关注</span>
          </p>
          <p>
            <span>0</span>
            <span class="user_text">获赞</span>
          </p>
        </div>
        <div @click="$router.push('/edit')">
          <div class="user_editBtn" >编辑资料</div>
        </div>
      </div>
    </div>
    <div>
      <h2>{{userInfo.name}}</h2>
      <p v-if="userInfo.user_desc">{{userInfo.user_desc}}</p>
      <p v-else>这个人很神秘，什么都没有写</p>
    </div>
  </div>
</template>

<script>
export default {
    props:['userInfo']
};
</script>

<style lang="less">
.userdetail {
  background-color: white;
  padding: 0 12px;
  > div:nth-child(1) {
    display: flex;
    .user_img {
      margin-right: 20px;
      img {
        width: 85px;
        height: 85px;
        border-radius: 50%;
      }
    }
    .user_edit {
      margin-top: 10px;
      flex: 1;
      div:nth-child(1) {
        display: flex;
        p {
          flex: 1;
          display: flex;
          align-items: center;
          justify-content: center;
          flex-direction: column;
          font-size: 14px;
          .user_text {
            color: #aaa;
          }
        }
        p:nth-child(1),
        p:nth-child(2) {
          border-right: 1px solid #ccc;
        }
      }
      div:nth-child(2) {
        padding: 5px 10px;
        .user_editBtn {
          border: 1px solid #fb7a9f;
          padding: 3px;
          display: flex;
          justify-content: center;
          align-items: center;
          color: #fb7a9f;
          border-radius: 4px;
        }
      }
    }
  }
  >div:nth-child(2){
      h2{
          margin: 10px 0 3px 0;
          font-weight: 400;
      }
      p{
          padding:  0;
          margin: 10px 0;
          color: #999;
      }
      
  }
}
</style>