<template>
<div class="hero">
    <ul class="hero_list">
        <li v-for="(item, index) in heroData" >
            <router-link :to=" '/detail?id=' + (index+1) ">
            <p class="img_wrap"><img :src=" heroPath + (index+1) + '.jpg' "  /></p>
            <b>{{item.nick + '&bull;' + item.name}}</b>
            </router-link>
        </li>
        
    </ul>
</div>
</template>

<script>
import HeroData from '../assets/hero_data'

export default {
    name: 'HelloWorld',
    data () {
        return {
            msg: 'shuihu list'
            ,heroData: []
            ,heroPath: '/static/hero_img/'
        }
    }
    ,mounted(){
        //todo set data?
        this.heroData = HeroData
    }
    ,methods:{
        goDetail(){
            console.log('go detail') ;

        }
    }
}
</script>

<style scoped>
a { color: #42b983; }
.hero_list {overflow:hidden;}
.hero_list li {position:relative;float:left;width:32.6%;height:4rem;background-color:#eee;margin:.5% 0 0 .5%;overflow:hidden;}
.hero_list b {position:absolute;top:0;right:0;width:.26rem;line-height:.3rem;font-size:.24rem;text-align:center;background-color:rgba(0,0,0,0.3);color:#ccc;padding:2px 2px;border-radius:0 0 0px 2px;  
    word-break:break-all;white-space:normal;word-wrap:break-word;}
.hero_list img {position:absolute;left:50%;top:0px;height:100%;transform:translateX(-50%)}
</style>
