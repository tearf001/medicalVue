<template>
  <div class="center">
    <!-- 子路由展示 -->
    <router-view></router-view>
    <!-- 微信查询tab 两个选项卡 -->
    <div v-if="tabSearch">
      <div class="searchTab">
        <router-link tag="div" v-for="(item,index) in searchTabList" :to="{path: item.path}" :class="['searchTab-li chooseSearchTab']">
          <img :src="item.imgUrl">
          <span>{{item.msg}}</span>
        </router-link>
      </div>
      <!-- 其他信息 -->
      <otherMsg></otherMsg>
    </div>
  </div>
</template>

<script>
  import user from "@/components/user.vue"
  import otherMsg from "@/components/otherMsg.vue"
  export default {
    name: 'search',
    data () {
      return {
        searchTabList: [
          {
            path: "/search-my",
            imgUrl: require('../assets/search/search-my.png'),
            msg: "个人综合信息查询"
          },
          {
            path: "/search-other",
            imgUrl: require('../assets/search/search-other.png'),
            msg: "用户缴费信息查询"
          }
        ],
        currentIndex: 0,
        tabSearch: true
      }
    },
    mounted () {
      this.$nextTick(function (){
      });
    },
    watch: {
      "$route": "fetchDate"
    },
    methods: {
      touchPayBar (index) {
        this.currentIndex = index;
      },
      fetchDate(){
        if (this.$route.name == 'search-other' || this.$route.name == 'search-my') {
          this.tabSearch = false;
        }
        if (this.$route.name == 'search') {
          this.tabSearch = true;
        }
      }
    },
    components: {
      user,
      otherMsg
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.medical-title{
  color: red;
}
  .searchTab{
    width: 100%;
    height: 9rem;
    border-bottom: .7rem solid #EDF2F5;
    display: box;
    display: -webkit-box;
    display: -moz-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    justify-content: space-around;
    -ms-align-items: center;
    align-items: center;
  }
  .searchTab-li:first-child{
    margin-right: 2px;
  }
  .searchTab-li{
    width: 50%;
    height: 7rem;
    border-radius: .2rem;
    background: #EFEFEF;
    color: #9D9D9D;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: box;
    display: -webkit-box;
    display: -moz-box;
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
    -webkit-flex-direction: column;
    -moz-flex-direction: column;
    -ms-flex-direction: column;
    -o-flex-direction: column;
    flex-direction: column;
    justify-content: center;
    -ms-align-items: center;
    align-items: center;
  }
  .searchTab-li img{
    width: 2.5rem;
    margin-bottom: .5rem;
  }
  .searchTab-li span{
    font-size: .875rem;
  }
  .chooseSearchTab{
    background: #fff;
    border: 1px dashed #E5F7FF;
    -webkit-box-shadow: 1px 1px 10px 2px #CCEFFF;
    box-shadow: 1px 1px 10px 2px #CCEFFF;
    color: #31679C;
    -webkit-transition: all .2s;
    -o-transition: all .2s;
    transition: all .2s;
  }
</style>
