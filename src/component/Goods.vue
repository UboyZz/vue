<template>
  <div>
    <div class="header">
        <div class="content-wrapper">
          <div class="avatar">
            <img width="64" height="64" src="http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg">
          </div>
          <div class="content">
            <div class="title">
              <span class="brand"></span>
                <span class="name">{{shopdes.shop_name}}</span>
            </div>
            <div class="description">
              <span class="buluetiger">{{shopdes.shop_delivery}}</span>38分钟送达|配送费￥{{shopdes.shop_uptosend}}
            </div>
            <div class="support">
              <span class="text">在线支付满28减5</span>
            </div>
          </div>
          <Vactivity :shopid="shopid"></Vactivity>
        </div>

        <div class="background">
          <img width="100%" height="100%" src="http://static.galileo.xiaojukeji.com/static/tms/seller_avatar_256px.jpg">
        </div>
    </div>
    <div class="navtab">
      <ul>
        <li @click="selectactive(0)" :class="{'active':active==0}">商品</li>
        <li @click="selectactive(1)" :class="{'active':active==1}">评价（4.7分）</li>
        <div class="cf"></div>
      </ul>
    </div>
    <div  class="good" v-show="active==0">
      <div class="menu-wrapper" ref="menuWrapper">
        <ul>
          <li v-for="(item, index) in goods" class="menu-item"  :class="{'current':currentIndex === index}"
              @click="selectMenu(index, $event)">
          <span class="text">
           {{item.SaleType}}
          </span>
          </li>
        </ul>
      </div>
      <div class="foods-wrapper" ref="foodWrapper">
        <ul>
          <li v-for="item in goods" class="food-list food-list-hook">
            <h1 class="title">{{item.SaleType}}</h1>
            <ul>
              <li v-for="food in item.item" class="food-item" @click="selectFood(food, $event)">
                <div class="icon">
                  <img src="../../static/temp/4.jpg">
                </div>
                <div class="content">
                  <h2 class="name">{{food.name}}</h2>
                  <p class="desc">{{food.description}}</p>
                  <div class="extra">
                    <span class="count">月售52份</span>
                  </div>
                  <div class="price">
                    <span class="now">￥{{food.price}}</span>
                    <span class="fr">
                     <div class="caroption">
                        <a @click="add(-1,food.SaleID)"><i>-</i></a>
                        <span>{{food.conts}}</span>
                        <a @click="add(1,food.SaleID)"><i>+</i></a>
                    </div>
                    </span>
                  </div>
                </div>
              </li>
            </ul>
          </li>
        </ul>
      </div>
      <div>

      </div>
    </div>
    <div v-show="active==1">
      <div class="discuss row" >
        <div class="score">
          <span class="name">4.7</span><br/>
          <span class="text">综合评分</span><br/>
          <span class="percent">高于周边商家79.7%</span>
        </div>
        <div class="starscontent">
          <div class="starsitem">
            <span>服务态度</span>
            <span><Vstars :score="3.8"></Vstars></span>
            <span class="text-yellow">3.8分</span>
          </div>
          <div class="starsitem">
            <span>服务态度</span>
            <span><Vstars :score="5"></Vstars></span>
            <span class="text-yellow">5分</span>
          </div>
          <div class="starsitem">
            <span>送达时间</span>
            <span class="text-title">45分钟</span>
          </div>
        </div>
      </div>
      <div class="hr"></div>
      <div class="targete">
        <span  class="active">全部（252）</span>
        <span>满意（123）</span>
        <span >不满意（52）</span>
        <span>有图（22）</span>
        <span >味道好（33）</span>
        <span>送货快（183）</span>
        <span >分量足（252）</span>
      </div>
      <div class="estimate">
        <div class="title">只看有内容的评价</div>
        <div class="content">
          <div class="imgcontent"><img src="../../static/temp/4.jpg"/> </div>
          <div class="des">
            <div class="item">
              <span class="name">小****手术</span><span class="data">2017-02-03</span>
            </div>
            <div class="item">
              <span class="headline">商家服务：</span>
              <span><i class="iconfont icon-xingxing "></i>非常满意|</span>
              <span class="headline">商品：</span>
              <span><i class="iconfont icon-xingxing "></i>非常满意</span>
            </div>
            <div class="item">
              <span class="text-bulue">阿萨德看了看:</span><span>非常好吃</span>
            </div>
            <div class="item">
              <span class="text-bulue">阿萨德看了看:</span><span>非常好吃</span>
            </div>
          </div>
        </div>
        <div class="content">
          <div class="imgcontent"><img src="../../static/temp/4.jpg"/> </div>
          <div class="des">
            <div class="item">
              <span class="name">小****手术</span><span class="data">2017-02-03</span>
            </div>
            <div class="item">
              <span class="headline">商家服务：</span>
              <span><i class="iconfont icon-xingxing "></i>非常满意|</span>
              <span class="headline">商品：</span>
              <span><i class="iconfont icon-xingxing "></i>非常满意</span>
            </div>
            <div class="item">
              <span class="text-bulue">阿萨德看了看:</span><span>非常好吃</span>
            </div>
            <div class="item">
              <span class="text-bulue">阿萨德看了看:</span><span>非常好吃</span>
            </div>
          </div>
        </div>
      </div>
    </div>
   <Vshopcart :cartfoods="goods" :upsend="shopdes.SendPrice"></Vshopcart>
  </div>

</template>

<script type="text/ecmascript-6">
  import BScroll from 'better-scroll';
  import Vactivity from "./Activity.vue"
  import Vstars from "./Stars.vue"
  import Vshopcart from "./ShopCart.vue"
  import Vcaroption from "./CartOption.vue"
  export default {
    name:"goods",
    props: {

    },
    data () {
      return {
        shopdes:[],
        active:0,
        goods: [],
        listHeight: [],
        scrolly: 0,
        foods:[],
      };
    },
    created() {
      this.$store.state.neednav = false;
      this.shopid=this.$route.params.orgid;
      this.loadshopdes()
      this._index=1;
      this.$http.post(this.$store.state.IP+"/api/goods/getlist",{id:this.shopid}).then(function (res) {
        this.goods=res.body.Rows;
        console.log(this.goods)
        this.$nextTick(() => {
          this._initScroll();
          this._calculateHeight();
        });
      })

    },
    computed: {
      currentIndex() {
        for (let i = 0; i < this.listHeight.length; i++) {
          let height = this.listHeight[i];
          let height2 = this.listHeight[i + 1];
          if (!height2 || (this.scrolly >= height && this.scrolly < height2)) {
            return i;
          }
        }
        return 0;
      },
      selectFoods() {
        let foods = [];
        this.goods.forEach((good) => {
          good.foods.forEach((food) => {
            if (food.count) {
              foods.push(food);
            }
          });
        });
        return foods;
      }
    },
    methods: {
      add(cont,id){
          for(var i=0;i<this.goods.length;i++) {
            for (var j = 0; j < this.goods[i].item.length; j++) {
              if (id == this.goods[i].item[j].SaleID) {
                if(this.goods[i].item[j].conts==0&&cont<0){
                  this.goods[i].item[j].conts=0
                }else {
                  this.goods[i].item[j].conts+=cont
                }
              }
            }
          }
      },
      //获取头部商家信息
      loadshopdes(){
        this.$http.post(this.$store.state.IP+"/api/shop/getoneshop",{id:this.shopid}).then((res)=>{
         this.shopdes=res.body[0]
        })
      },
      _initScroll() {
        this.menuScroll = new BScroll(this.$refs.menuWrapper, {
          click: true
        });
        this.foodScroll = new BScroll(this.$refs.foodWrapper, {
          probeType: 3,
          click: true
        });
        this.foodScroll.on('scroll', (pos) => {
          this.scrolly = Math.abs(Math.round(pos.y));
        });
      },
      _calculateHeight() {
        let foodList = this.$refs.foodWrapper.getElementsByClassName('food-list-hook');
        let height = 0;
        this.listHeight.push(height);
        for (let i = 0; i < foodList.length; i++) {
          let item = foodList[i];
          height += item.clientHeight;
          this.listHeight.push(height);
        }
      },
      selectMenu(index, event) {
        if (!event._constructed) {
          // 去掉自带click事件的点击
          return;
        }
        let foodList = this.$refs.foodWrapper.getElementsByClassName('food-list-hook');
        let el = foodList[index];
        this.foodScroll.scrollToElement(el, 300);
      },
      selectFood(food, event) {
        if (!event._constructed) {
          return;
        }
       /* this.selectedFood = food;
        this.$refs.food.show();*/
      },
      incrementTotal(target) {

        this.$refs.shopCart.drop(target);
      },
      selectactive(index){
       this.active=index
      }
    },
    components: {
      Vactivity:Vactivity,
      Vstars:Vstars,
      Vshopcart:Vshopcart,
      Vcaroption:Vcaroption
    }
  };
</script>
<style>

</style>
