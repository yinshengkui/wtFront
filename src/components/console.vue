<template>
    <div class="choose-type">
        <slot name="headerTop">
            <HeaderTop :navList="navList" :funName="funName" :teamName="user.teamName"></HeaderTop>
        </slot>

        <q-alert
            v-if="visibleTopInfoAlert"
            color="positive"
            icon="access_alarm"
            appear
            :actions="[
                { label: '知道了', handler: () => { visibleTopInfoAlert = false } }, 
                { label: '不再提示', handler: () => { this.notShow() } }
            ]"
            class="q-mb-sm top-info"
        >
            更新日志 v2.0.1<br>
            <br>
            ● 月报OKR优化:<br>
              <br>
              ○ 新增『复制』功能,可以从当月的目标复制到绩效<br>
              ○ 展示板新增以下展示: 自我评分、自我评价、组长评价<br>
              ○ 新增流程组长评价,小组成员通过或者驳回需要写评价,组长本身的评价由TL填写
        </q-alert>
        <a class="good relative-position" v-ripple="true" @click="goOkr">
            <img src="statics/types/okr.jpg" alt="">
            <p>月报OKR</p>
        </a>
        <a class="good relative-position" v-ripple="true" @click="$router.push('/')">
            <img src="statics/types/week.jpg" alt="">
            <p>周报</p>
        </a>
        <a v-if="user.pRole === 1" class="good relative-position" v-ripple="true" @click="$router.push('/pm')">
            <img src="statics/types/pm.jpg" alt="">
            <p>PM周报</p>
        </a>
        <a class="good relative-position" v-ripple="true" @click="$router.push('/userEnergy')">
            <img src="statics/types/energy.jpg" alt="">
            <p>能量图</p>
        </a>
        <a class="good relative-position" v-ripple="true" @click="$router.push('/userShow')">
            <img src="statics/types/boy-avatar.jpg" alt="">
            <p>成员秀</p>
        </a>
        <slot name="footerTop">
            <FooterTop></FooterTop>
        </slot>
    </div>
</template>

<script>
    import HeaderTop from '../layouts/common/header';
    import FooterTop from '../layouts/common/footer';
    export default {
        name: 'Console',
        data () {
            return {
                navList: [],
                funName: '',
                user: {},
                visibleTopInfoAlert: true,
                
            }
        },
        validations: {},
        components: {HeaderTop, FooterTop},
        created () {
            this.init();
        },
        methods: {
            init () {
                const _this = this;
                _this.user = JSON.parse(localStorage.getItem('user'));
                _this.visibleTopInfoAlert = localStorage.getItem('notshow_console') === 'v2.0.1' ? false : true;
            },
            notShow () {
                window.localStorage.setItem('notshow_console', 'v2.0.1');
                this.visibleTopInfoAlert = false;
            },
            goOkr () {
                window.location.href = 'https://luolinjia.com/tt/okr'
            }
        }
    }
</script>

<style scoped lang="less">
    .choose-type {
        // position:absolute;
        // width:60%;
        // height:50%;
        // top:50%;
        // left:50%;
        // transform:translate(-50%,-50%);
        margin: 0 auto;
        width: 76%;
        position: relative;
        margin-top: 300px;
        .bread {
            position: absolute;
            left:-8px;
            top: -60px;
            margin: 0;
        }
    }
    .team-title {
        position: absolute;
        top: -88px;
        font-style: normal;
        font-size: 20px;
        font-weight: bold;
    }
    .btn-create {
        /*margin-top: 10px;*/
        position: relative;
        top: -15px;
        // left: 15px;
    }

    .q-table-container {
        -webkit-box-shadow: none;
        -moz-box-shadow: none;
        box-shadow: none;
    }

    .form-field {
        margin: 12px 0;
    }

    .task-table {
        border: none;
    }
    .good {
        width: 200px;
        height: 200px;
        // background: red;
        display: inline-block;
        margin-right: 20px;
        margin-bottom: 20px;
        border: 5px solid #333;
        overflow: hidden;
        cursor: pointer;
        transition: all ease-in .1s;
        &:hover {
            box-shadow: 3px 3px 10px #999;
            transform: translateX(-2px);
            transform: translateY(-2px);
        }
        
        p {
            margin-left: 10px;
            position: relative;
            top: -4rem;
            color: white;
            font-size: 2rem;
        }
    }
    .top-info {
        margin-bottom: 3rem;
        width: 80%;
    }
</style>
<style lang="less">
    // .q-table-top {
    //     position: absolute;
    //     top: -45px;
    //     right: 50px;
    //     min-height: 0;
    //     padding: 0;
    // }
</style>
