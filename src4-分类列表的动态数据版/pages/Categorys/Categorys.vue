<template>
  <div class="categorys_brand">
    <div class="categorys_header bottom-border-1px">
      <div class="categorys_list" @click="selected(1)">
        <a href="javascript:;" class="categorys_text" :class="{on:selectType===1}">分类</a>
      </div>
      <div class="pinpai" @click="selected(2)">
        <a href="javascript:;" class="pinpai_text" :class="{on:selectType===2}">品牌</a>
        <a> <i class="iconfont icon-search"></i> </a>
      </div>
    </div>
    <div class="categorys_content" v-show="selectType===1">
      <div id="categorys_list">
        <ul>
          <li class="list" :class="{on: currentCateIndex===index}" v-for="(classify,index) in categorys"
              :key="index" @click="clickCurrentCategory(index)">{{classify.name}}</li>
        </ul>
      </div>
      <div id="pinpai_container">
        <div class="pinpai_list">
          <div class="zhuliang">
            <div class="title">
              <span>狗狗主粮</span>
              <a class="link_to">
                <span>全部商品<i class="iconfont icon-quanbu"></i></span>
              </a>
            </div>
            <ul class="zhuliang_ul">
              <li class="zhuliang_list">
                <img src="./imags/1-1.jpg" alt="">
                <span>进口狗粮</span>
              </li>
              <li class="zhuliang_list">
                <img src="./imags/1-2.jpg" alt="">
                <span>国产狗粮</span>
              </li>
              <li class="zhuliang_list">
                <img src="./imags/1-3.jpg" alt="">
                <span>处方狗粮</span>
              </li>
              <li class="zhuliang_list">
                <img src="./imags/1-1.jpg" alt="">
                <span>冻干狗粮</span>
              </li>
            </ul>
          </div>
          <div class="remen">
            <p class="remen_title">热门品牌</p>
            <ul class="remen_ul">
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>
              <li class="remen_li">
                <img src="./imags/2-1.jpg" alt="">
                <span>天衡宝（原雪山）</span>
              </li>

            </ul>
          </div>
        </div>
      </div>
    </div>
    <div class="brand_container" v-show="selectType===2">
      <div class="brand_content">
        <div class="brand_item">
          <div class="brand_list_title">
            <span>—— 推荐品牌 ——</span>
          </div>
          <div class="brand_list">
            <ul class="list_ul">
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai1.jpg" alt="">
                </div>
                <p class="name">冠能</p>
                <p class=" name country">美国</p>
              </li>
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai2.jpg" alt="">
                </div>
                <p class="name">ZIWI Peek</p>
                <p class=" name country">新西兰</p>
              </li>
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai3.jpg" alt="">
                </div>
                <p class="name">原始猎食渴望</p>
                <p class=" name country">加拿大</p>
              </li>
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai1.jpg" alt="">
                </div>
                <p class="name">冠能</p>
                <p class=" name country">美国</p>
              </li>
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai2.jpg" alt="">
                </div>
                <p class="name">ZIWI Peek</p>
                <p class=" name country">新西兰</p>
              </li>
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai3.jpg" alt="">
                </div>
                <p class="name">原始猎食渴望</p>
                <p class=" name country">加拿大</p>
              </li>
              <li class="list_li">
                <div class="img_container">
                  <img src="./imags/3-pinpai2.jpg" alt="">
                </div>
                <p class="name">ZIWI Peek</p>
                <p class=" name country">新西兰</p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  import {mapState} from 'vuex'

  export default{
    data(){
      return {
        selectType: 1, // 默认选中分类
        currentCateIndex: 0  // 默认选中分类列表的第一个为您推荐
      }
    },
    mounted(){
      this.$store.dispatch('getCategorys',() => {
        this.$nextTick(() => {
          // 左边分类列表滑动效果
          if(!this.scrollCategorys){
            this.scrollCategorys = new BScroll('#categorys_list',{
              click: true
            })
          }else{
            this.scrollCategorys.refresh()
          }
        })
      })

      // 右侧热门品牌
      if(!this.scrollRemen){
        this.scrollRemen = new BScroll('#pinpai_container',{
          click: true
        })
      }else{
        this.scrollRemen.refresh()
      }
    },
    computed: {
      ...mapState(['categorys'])
    },
    methods: {
      // 头部选择分类还是品牌
      selected(selectType){
          this.selectType = selectType
      },
      //选分类列表的内容
      clickCurrentCategory(index){
        this.currentCateIndex = index
      }
    }
  }

</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixins.styl"
  .categorys_brand
    width 100%
    height 100%
    position relative
    background #f5f5f5
    .categorys_header
      bottom-border-1px(#999)
      position fixed
      top 0
      left 0
      right 0
      height 50px
      z-index 100
      display flex
      justify-content space-between
      align-items center
      background #fff
      .categorys_list
        width 50%
        text-align right
        padding-right 10px
        line-height 50px
        padding-bottom 10px
        .categorys_text
          color black
          font-size 14px
          padding-bottom 5px
          &.on
            color red
            border-bottom 1px solid red
      .pinpai
        display flex
        justify-content space-between
        align-items flex-end
        padding 0 15px
        width 50%
        .pinpai_text
          color black
          font-size 14px
          padding-bottom 5px
          &.on
            color red
            border-bottom 1px solid red


    .categorys_content
      width 100%
      height 100%
      box-sizing border-box
      padding-top 50px
      font-size 14px
      display flex
      #categorys_list
        height 100%
        width 20%
        >ul
          width 100%
          display flex
          text-align center
          flex-direction column
          background #fff
          margin-right 5px
          padding-bottom 50px
          .list
            padding 20px 0
            height 100%
            width 100%
            border-bottom 1px solid #f5f5f5
            &.on
              background  #f5f5f5
              color red




      #pinpai_container
        width 80%
        height 100%
        margin 5px 0 0 6px
        .pinpai_list
          background #fff
          width 100%
          padding 10px 10px
          box-sizing border-box
          .zhuliang
            bottom-border-1px(#f5f5f5)
            width 100%
            margin  10px 0
            .title
              width 100%
              display flex
              justify-content space-between
              .link_to
                display block
                margin-left 140px
                font-size 10px


            .zhuliang_ul
              width 100%
              display flex
              justify-content flex-start
              text-align center
              flex-wrap wrap
              padding-bottom 20px
              .zhuliang_list
                margin 10px 0px
                width 33.3333333%
                >img
                  width 87px
                  height 87px
                  display block
                  margin-bottom 10px



          .remen
            width 100%
            margin 30px 0
            .remen_title
              color #999
              text-align left

            .remen_ul
              margin-top 10px
              width 100%
              display flex
              flex-wrap wrap
              justify-content space-between
              .remen_li
                width 48%
                height 100px
                text-align center
                font-size 12px
                >img
                  padding 5px 10px
                  width 80%
                  display block
                  border 1px solid #ddd
                  margin-bottom 10px





    .brand_container
      width 100%
      height 100%
      padding-top 55px
      box-sizing border-box
      .brand_content
        width 100%
        background #ffffff
        .brand_item
          width 100%
          padding 20px 10px 0
          text-align center
          color #999
          font-size 12px
          box-sizing border-box
          margin-bottom 10px
          .brand_list
            margin-top 20px
            width 100%
            .list_ul
              width 100%
              display flex
              flex-wrap wrap
              justify-content space-between
              .list_li
                width 32%
                margin-bottom 15px
                .img_container
                  width 100%
                  height 60px
                  border 1px solid #e2e2e2
                  box-sizing border-box
                  padding 20px 10px
                  margin-bottom 5px
                  >img
                    margin-top -15px
                    width 100%
                    display block
                .name
                  width 100%
                  height 20px
                  line-height 20px
                  color black
                  &.country
                    color #999

</style>
