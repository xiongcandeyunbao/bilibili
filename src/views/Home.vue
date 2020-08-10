<template>
  <div class="home" v-if="category">
    <nav-bar></nav-bar>
    <div class="categorytab">
      <div class="category-ico" @click="$router.push('/editcategory')"><van-icon name="setting-o" /></div>
    <van-tabs v-model="active" swipeable sticky>
      <van-tab v-for="(item,index) in category" :title="item.title" :key="index">
        <van-list v-model="item.loading" :finished="item.finished" finished-text="我也是有底线的" :immediate-check="false" @load="onLoad">
          <div class="detailparent">
            <cover
              class="detailitem"
              :detailitem="categoryitem"
              v-for="(categoryitem,categoryindex) in item.list"
              :key="categoryindex"
            />
          </div>
        </van-list>
      </van-tab>
    </van-tabs>
    </div>
  </div>
</template>

<script>
import NavBar from "@/components/common/Navbar.vue";
import cover from "./cover";
export default {
  data() {
    return {
      category: [],
      active: 0
    };
  },
  components: {
    NavBar,
    cover
  },
  activated(){
    //页面活跃调用
    if(localStorage.getItem('newCat')){
      let newCat =JSON.parse(localStorage.getItem('newCat'))
        this.category = this.changeCategory(newCat)
        this.selectArticle()
    }
  },
  methods: {
    async selectCategory() {
      if(localStorage.getItem('newCat')){
        
        return
      }
      const res = await this.$http.get("/category");
      this.changeCategory(res.data);
    },
    changeCategory(data) {
      //改造数据
      const category1 = data.map(item => {
        item.list = [];
        item.page = 0,
        item.finisned= false,
        item.loading=false,
        item.pagesize = 10;
        return item;
      });
      // this.category = category1;
      // this.selectArticle();
      return category1
    },
    async selectArticle() {
      //获取数据  页面刷新
      const categoryitem = this.categoryItem();
      const res = await this.$http.get("/detail/" + categoryitem._id, {
        params: {
          page: categoryitem.page,
          pagesize: categoryitem.pagesize
        }
      });
      categoryitem.list.push(...res.data);
      categoryitem.loading= false
      if(res.data.length<categoryitem.pagesize){
          categoryitem.finisned=true
      }
    },
    categoryItem() {
      //返回点击之后改变的值
      const categoryitem = this.category[this.active];
      return categoryitem;
    },
    onLoad(){
        const categoryitem=this.categoryItem()
        setTimeout(() => {
            categoryitem.page +=1
            this.selectArticle()
        }, 1000);
        
    }
  },

  watch: {
    active() {
      // this.categoryItem()
      this.selectArticle();
    }
  },
  created() {
    this.selectCategory();
  }
};
</script>

<style lang="less">
.home {
  background-color: white;
}
.detailparent {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  .detailitem {
    margin: 1.389vw 0;
    width: 45%;
  }
}
.categorytab{
  position: relative;
  .category-ico{
    position: absolute;
    z-index: 5;
    right: 0;
    top: 1.944vw;
    padding: 1.389vw 2.778vw;
    background-color: white;
  }
}
</style>