<template>
    <div class="list" ref="wrapper">
       <div>
           <div class="area">
           <div class="title border-topbottom">当前城市</div>
           <div class="btn-list">
               <div class="btn-wrap" >
                   <div class="btn">{{this.currentCity}}</div>
               </div>
           </div>
       </div>
       <div class="area">
           <div class="title border-topbottom">热门城市</div>
           <div class="btn-list">
               <div class="btn-wrap" @click="handleCity(item.name)" v-for="item of hot" :key="item.id">
                   <div class="btn">{{item.name}}</div>
               </div>
           </div>
       </div>
       <div class="area"  v-for="(item,key) of cities" :key="key" :ref="key">
           <div class="title border-topbottom">{{key}}</div>
           <div class="item-list"  @click="handleCity(items.name)" v-for="(items,key) of item" :key="key">
               <div class="item border-bottom">{{items.name}}</div>
           </div>
       </div>
       </div>
    </div>
</template>

<script>
import BScroll from 'better-scroll'
import {mapState, mapMutations} from 'vuex'
export default {
    props: {
        hot:Array,
        cities:Object,
        letter:String
    },
    computed: {
        ...mapState({
            currentCity:'city'
        })
        
    },
    methods: {
      handleCity(city){
          this.handleCityBtn(city)
          this.$router.push('/')
      },
        ...mapMutations(['handleCityBtn'])
        
    },
    mounted () {
        // bs引入
       this.scroll = new BScroll(this.$refs.wrapper)
    },
    watch: {
        letter(){
            if(this.letter){
                const element=this.$refs[this.letter][0]
                // 滚动到指定dom元素
                this.scroll.scrollToElement(element)
            }
        }
    }
}
</script>

<style lang="stylus" scoped>
@import "~styles/varibies.styl"
    .border-topbottom
        &:before
            border-color #cccccc
        &:after
            border-color #ccc  
    .border-bottom
        &:before
            border-color #cccccc
.list
    overflow hidden
    position absolute
    top 1.58rem
    left 0
    right 0
    bottom 0

    .title
        line-height .54rem
        background #eeeeee
        padding-left .2rem
        color #666666
        font-size .26rem
    .btn-list
        padding .1rem
        overflow hidden
        padding .1rem .6rem .1rem .1rem
        .btn-wrap
            float left
            width 33.33%
            .btn
                margin .1rem
                text-align center
                border .02rem solid #ccc
                padding .1rem 0
                border-radius .1rem
    .item-list
        .item
            line-height .76rem
            padding-left .2rem
</style>
