<template>
  <div class="home">
    <Nav-Bar class="home-nav"><div slot="center">购物街</div></Nav-Bar>
    <Home-Swiper :banners="banners"/>
    <Recomend-View :recommends="recommends"/>
    <Feature-View/>
    <Tab-control class="tab-control" :titles="['流行','新款','精选']"/>

    <!-- 虚拟数据 -->
    <div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    <div>劝君惜取少年时</div>
    </div>
  </div>
</template>  

<script>
import NavBar from 'components/common/navbar/NavBar'
import TabControl from 'components/content/tabControl/TabControl'

import HomeSwiper from './childComps/HomeSwiper'
import RecomendView from './childComps/RecomendView'
import FeatureView from './childComps/FeatureView'

import { getHomeMultidata, getHomeGoods } from 'network/home'

export default {
  name: "Home",
  components: {
    NavBar,
    TabControl,
    HomeSwiper,
    RecomendView,
    FeatureView
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'news': {page: 0, list: []},
        'sell': {page: 0, list: []}
      }
    }
  },
  created() {
    // 1. 请求多个数据
    this.getHomeMultidata()

    // 2. 请求商品数据
    this.getHomeGoods('pop')
  },
  methods: {
    getHomeMultidata(){
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      })
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      })
    }
  },
}

</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }

  .tab-control {
    position: sticky;
    top: 44px;
  }
</style>