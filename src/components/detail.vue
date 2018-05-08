<template>
<div class="detail">
    <div class="nav">
        <router-link to="/">&laquo; 返回</router-link>
        <b @click="toggleCard">{{nextStatus}}</b>
    </div>

    <p class="img_wrap" v-show="showCover" :style="'height:' + contH + 'rem'"><img :src=" heroPath +index + '.jpg' "  /></p>

    <div class="hero_rare" v-show="!showCover" :style="'height:' + contH + 'rem'">
        <b class="name vt">{{hero.nick + '&bull;' + hero.name}}</b>

        <div class="attr vt">
            <p class="col">{{heroStar}}</p>
            <p class="col">职位 ：{{hero.pos}}</p>
            <p class="col col_pt" v-if="hero.posMore">{{hero.posMore}}</p>

            <p class="col">武器 ：{{hero.weapon}}</p>
            <p class="col col_pt" v-if="hero.weaponMore">{{hero.weaponMore}}</p>

            <p class="col">必杀技 ：{{hero.skill}}</p>
            <p class="col col_pt" v-if="hero.skillMore">{{hero.skillMore}}</p>
            <p class="col" v-if="hero.skillExt">特殊技 ：{{hero.skillExt}}</p>

            <div class="col">
                <b>防御力 ：</b>
                <span class="bg_def"> <i :style="'height:' + hero.defense + '%'"></i> </span>
            </div>
            <div class="col">
                <b>攻击范围 ：</b>
                <span class="bg_atkarea"> <i :style="'height:' + hero.attackArea + '%'"></i> </span>
            </div>
            <div class="col">
                <b>攻击力 ：</b>
                <span class="bg_atk"> <i :style="'height:' + hero.attack + '%'"></i> </span>
            </div>
        </div>

        <div class="info vt">
            <p v-for="(item,index) in heroInfo" :key="index">{{item}}</p>
        </div>

        <i class="order">{{hero.order}}</i>
    </div>
</div>
</template>

<script>
import HeroData from '../assets/hero_data'

export default {
    name: 'Detail',
    data () {
        return {
            heroData: []
            ,heroPath: '/static/hero_img/'
            ,index: 1
            ,hero: {}
            ,showCover: true
            ,nextStatus: '卡背'
            ,contH: '12.06'
            ,heroStar: ''
            ,heroInfo: []
        }
    }
    ,mounted(){
        //todo set data?
        this.heroData = HeroData
        this.index = this.$route.query.id

        var remRatio = document.documentElement.clientWidth/750*100
        var navH = 0.88*remRatio
        this.contH = (document.documentElement.clientHeight - navH)/remRatio

        this.hero = this.heroData[this.index-1]
        let D = this.hero

        let pos = D.pos.split('|')
        this.hero.pos = pos[0].replace('，', ' ， ')
        this.hero.posMore = pos[1] || ''

        let weapon = D.weapon.split('|')
        this.hero.weapon = weapon[0].replace('，', ' ， ')
        this.hero.weaponMore = weapon[1] || ''

        let skill = D.skill.split('|')
        this.hero.skill = skill[0].replace('，', ' ， ')
        this.hero.skillMore = skill[1] || ''

        let skillExt = D.skillExt.split('|')
        this.hero.skillExt = skillExt[0].replace('，', ' ， ')
        this.hero.skillExtMore = skillExt[1] || ''

        if (this.hero.order <37) {
            this.heroStar = '天罡 ： 天'+ this.hero.star +'星'
        }else{
            this.heroStar = '地煞 ： 地'+ this.hero.star +'星'
        }

        let len = D.detail.length
        let maxN = 15
        this.heroInfo.push('人物小传')
        for (let index = 0; index < len; index+=maxN) {
            let s = D.detail.substr(index, maxN)
            s = s.replace(/([，。“”])/gi, ' $1 ')
            this.heroInfo.push(s)
        }
    }
    ,methods:{
        toggleCard(){
            if (this.showCover) {
                this.showCover = false
                this.nextStatus = '卡面'
            }else {
                this.showCover = true
                this.nextStatus = '卡背'
            }
        }
    }
}
</script>

<style scoped>
@import url('detail.css');
</style>
