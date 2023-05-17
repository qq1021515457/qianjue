<template>
    <el-dialog v-model="state.visible" width="1000px" :before-close="handleClose">
        <video ref="videoPlayerRef" :src="state.videoUrl" style="width: 100%;" controls></video>
    </el-dialog>
    <div class="banner">
        <img class="banner-img" src="../assets/img/banner.png" alt="" />
        <div class="banner-content">
            <div class="banner-text">
                <span>全方位发掘</span>
                <span>您的交易优势</span>
            </div>
            <button class="banner-btn" @click="login">立即体验 ></button>
        </div>
    </div>
    <div class="cpjs">
        <div class="cpjs-left">
            <img src="../assets/img/cpjs.png" />
        </div>
        <div class="cpjs-content">
            <div class="cpjs-header">
                <img class="cpjs-bkg" src="../assets/img/cpjs-bkg.png" />
                <div class="cpjs-title">产品介绍</div>
            </div>
            <div class="cpjs-text">
                工欲善其事必先利其器，做交易最核心的在于拥有一套适合自己的交易体系，而建立体系最重要的一环就是在历史数据中去回测、验证证这个交易系统，并在这个过程中去调整，优化，使之成为自己的征战市场的“利器”。本网站将提供便捷、高效、可视化的回测工具，节省您宝贵的时间，助您早日达到稳定盈利。
            </div>
        </div>
    </div>

    <div class="vip">
        <img class="vip-img" src="../assets/img/vip.png" alt="" />
        <div class="vip-text">
            <div>数据回测服务有效期为7天</div>
            <span>到期后请联系您的专属客服开通正式会员</span>
            <!-- <button class="vip-btn" @click="reg()">立即注册 ></button> -->
        </div>
    </div>

    <div class="video">
        <div class="video-header">
            观看演示录像
        </div>
        <div class="video-container">
            <div class="video-content">
                <div class="video-v1">
                    <img class="video-play" src="../assets/img/play.png" @click="play(0)" />
                </div>

            </div>

            <div class="video-group">
                <div class="video-v2">
                    <img class="video-play" src="../assets/img/play.png" @click="play(0)" />
                </div>
                <div class="video-v3">
                    <img class="video-play" src="../assets/img/play.png" @click="play(0)" />
                </div>
            </div>
        </div>
    </div>

    <div class="about">
        <div class="about-header">
            关于我们
        </div>
        <div class="about-text">
            千掘数据是广州涡牛网络科技旗下的专业数据型网站，服务于广大交易爱好者及全职交易员。主打功能是数据回测于可视化，今后将推出交易日志，深度分析，模拟交易等更多功能。助力交易者全方位打造属于自己的交易系统，少走弯路。
        </div>
    </div>

    <div class="td">
        <div class="td-header">为什么选择我们</div>
        <div class="td-content">
            <div class="td-item">
                <div class="title">便捷
                    <img src="../assets/img/bj.png" />
                </div>
                <div class="text">
                    只需要输入初始金额，单笔盈亏等基础信息，便可自动生产分析结果。
                </div>
            </div>
            <div class="td-item">
                <div class="title">高效
                    <img src="../assets/img/gx.png" />
                </div>
                <div class="text">
                    回测效率比传统用电子表格的方式快3倍以上
                </div>
            </div>
            <div class="td-item">
                <div class="title">可视化
                    <img src="../assets/img/ksh.png" />
                </div>
                <div class="text">
                    对于每一次的回测数据，我们都会显示折线图，以及关键的分析数据，例如盈利因素，平均盈利与亏损，以及回测的数据评分，让您清楚掌握回测信息，并找到最佳的优化方向。
                </div>
            </div>
            <div class="td-item">
                <div class="title">便于存储
                    <img src="../assets/img/cc.png" />
                </div>
                <div class="text">每次回测的数据都能够一键储存，并能随时在策略库中调取，继续编辑。</div>
            </div>
        </div>
    </div>

    <div class="js">
        <div class="js-content">
            <div class="js-header">量化交易之父</div>
            <div>
                <img class="js-yh" src="../assets/img/yinhao.png" style="margin-bottom: 20px;" />
            </div>
            <div class="js-text">
                不管多么复杂的模型，没有一个能长期不变一直赚钱，人不是机器的奴隶，模型需要人去不断更新，需要人去寻找市场上的规律。
            </div>
            <div style="text-align: right;">
                <img class="js-yh" src="../assets/img/yinhao.png"
                    style="transform: rotate(180deg);margin-left: auto;margin-top: 20px;" />
            </div>
            <div class="person">
                <img class="person-avatar" src="../assets/img/avatar.png" alt="" />
                <div class="person-name">
                    <span class="person-t1">詹姆斯·西蒙斯</span>
                    <span class="person-t2">量化交易之父</span>
                </div>
            </div>
        </div>
    </div>
    <!-- <div class="sm">
        免责声明：本网站的所有数据仅用于教育与娱乐用途，不构成任何投资建议。历史数据并不一定保证将来业绩，由于测试手法，品种，交易时间段的不同，可能出现会出现不及预期的结果。任何投资决策均基于投资者本人，投资所造成的损失一概与本网站无关。
    </div> -->
    <div style="height: 200px;"></div>
</template>

<script setup>
import EventBus from '../utils/EventBus';
import { reactive, ref, watch } from "vue";

const videoPlayerRef = ref();
const state = reactive({
    visible: false,
    videoUrl: '/mp4/test.mp4'
})

function handleClose(done) {
    const videoPlayer = videoPlayerRef.value;
    console.log(videoPlayer)
    videoPlayer.pause();
    done();
}

function login() {
    EventBus.emit('login:open')
}

function reg() {
    EventBus.emit('register:open')
}

function play(i) {
    const videos = [];
    state.visible = true;

}
</script>

<style scoped lang="css">
.page {
    width: 100%;
    overflow-x: hidden;
    height: 100%;
}

.banner {
    margin: 30px;
    position: relative;
}

.banner-img {
    width: 100%;
}

.banner-content {
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    right: 0;
    padding-left: 30px;
    padding-top: 64px;
}

.banner-text {
    font-size: 48px;
    font-weight: 600;
    color: white;
    display: flex;
    flex-direction: column;
}

.banner-btn {
    border-radius: 30px;
    background-color: white;
    font-size: 20px;
    color: #0095E8;
    border: none;
    height: 48px;
    line-height: 48px;
    padding: 0 40px;
    margin-top: 30px;
}

.cpjs {
    position: relative;
    display: flex;
    justify-content: space-between;
}

.cpjs-left {
    position: absolute;
    left: 0;
    top: 50%;
    transform: translate(0, -50%);
    padding-left: 30px;
}

.cpjs-left>img {
    width: 390px;
    height: 400px;
}

.cpjs-content {
    background-color: #403C4A;
    width: 678px;
    /* height: 459px; */
    border-radius: 40px 0 0 40px;
    margin-left: auto;
    display: flex;
    flex-direction: column;
    padding-left: 373px;
    padding-top: 20px;
    padding-bottom: 20px;
}

.cpjs-header {
    height: 62px;
    position: relative;
    display: flex;
    align-items: end;
}

.cpjs-title {
    font-size: 40px;
    color: #0095E8;
    position: absolute;
    left: 0;
    top: 0;
}

.cpjs-bkg {
    position: absolute;
    left: 0;
    top: 0;
    width: 105px;
    height: 62px;
}

.cpjs-text {
    font-size: 18px;
    color: white;
    line-height: 32px;
    padding-right: 20px;
}

.vip {
    display: flex;
    background: #403C4A;
    border-radius: 20px;
    margin: 30px 30px;
    align-items: center;
}

.vip-img {
    width: 208px;
    height: 149px;
    margin: 30px;
}

.vip-text {
    display: flex;
    flex-direction: column;
    flex: 1;
}

.vip-text>div {
    font-size: 32px;
    color: #0095E8;
}

.vip-text>span {
    font-size: 20px;
    color: white;
    font-weight: 400;
    margin-top: 10px;
}

.vip-text>img {
    width: 557px;
    height: 45px;
}

.vip-btn {
    width: 120px;
    height: 36px;
    line-height: 36px;
    border-radius: 30px;
    border: 1px solid #FFFFFF;
    background-color: transparent;
    font-size: 16px;
    font-weight: 600;
    color: white;
    margin-top: 20px;
}

.video {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0 30px;
}

.video-container {
    position: relative;
    width: 100%;
}

.video-header {
    text-align: center;
    margin-bottom: 30px;
    font-size: 40px;
    color: #0095E8;
}

.video-bg {}

.bg-img {
    width: 176px;
    height: 176px;
}

.bg-left {
    position: absolute;
    left: 0;
    top: 0;
    margin-left: 90px;
    margin-top: 20px;

}

.bg-right {
    position: absolute;
    right: 0;
    bottom: 0;
    margin-right: 90px;
    margin-bottom: 0px;
}

.video-text {
    width: 429px;
    height: 67px;
}

.video-content {
    margin: 0 auto;
    z-index: 100;
}

.video-v1 {
    width: 690px;
    height: 388px;
    border-radius: 20px;
    background-image: url("../assets/img/v1.png");
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto;
}

.video-group {
    display: flex;
    gap: 30px;
    margin-top: 30px;
}

.video-v2 {
    border-radius: 20px;
    background-image: url("../assets/img/v2.png");
    background-size: cover;
    width: 100%;
    height: 188px;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
}

.video-v3 {
    border-radius: 20px;
    background-image: url("../assets/img/v3.png");
    background-size: cover;
    width: 100%;
    height: 188px;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
}

.video-play {
    width: 80px;
    height: 80px;
}

.about {
    margin-top: 30px;
    height: 320px;
    width: 100%;
    background-image: url("../assets/img/about.png");
    background-size: cover;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

}

.about-header {
    font-size: 40px;
    color: #0095E8;
}

.about-text {
    color: white;
    padding: 0 40px;
    font-size: 20px;
    line-height: 36px;
    margin-top: 20px;
    text-align: center;
}

.td {
    margin: 0 30px;
}

.td-header {
    font-size: 40px;
    color: #0095E8;
    text-align: center;
    margin-top: 30px;
    margin-bottom: 30px;
}

.td-content {
    display: flex;
    align-items: center;
    justify-content: center;
    align-content: stretch;
    flex-wrap: wrap;
    gap: 30px;
}

.td-item {
    width: calc(50% - 15px);
    min-height: 380px;
    border-radius: 20px;
    background-color: #403C4A;
    /* align-items: stretch;
    align-content: center; */
}

.td-item>.title {
    font-size: 32px;
    color: #0095E8;
    margin: 20px 40px 0;
    display: flex;
    align-items: center;
    align-content: stretch;
}

.td-item>.title>img {
    width: 30px;
    height: 30px;
    margin-left: 20px;
}

.td-item>.text {
    font-size: 18px;
    color: white;
    margin: 20px 40px 0;
    line-height: 32px;
}

.js {
    margin: 30px 30px 0;
}

.js-header {
    font-size: 40px;
    text-align: center;
    color: rgba(0, 149, 232, 1);
    margin-bottom: 20px;
}

.js-content {
    width: 100%;
    border-radius: 20px;
    background: rgba(64, 60, 74, 1);
    padding: 30px 60px;
}

.js-name {
    position: relative;
    margin-left: 80px;
}

.js-bg {
    position: absolute;
    left: 0;
    top: 0;
}

.js-bg>img {
    width: 176px;
    height: 128px;
}

.js-name-box {
    padding-top: 20px;
    position: relative;
    z-index: 100;
}

.js-text {
    font-size: 24px;
    color: white;
    line-height: 32px;
}

.js-yh {
    width: 72px;
    height: 54px;
}

.person {
    display: flex;
    align-items: end;
    margin-top: 30px;
}

.person-avatar {
    width: 120px;
    height: 120px;
}

.person-name {
    display: flex;
    flex-direction: column;
    padding-left: 30px;
}

.person-t1 {
    font-size: 24px;
    color: white;
}

.person-t2 {
    margin-top: 5px;
    font-size: 18px;
    color: rgba(255, 255, 255, 0.5);
    margin-bottom: 10px;

}

.js-name-box {
    display: flex;
    flex-direction: column;
}

.js-n1 {
    font-size: 72px;
    color: #0095E8;
}

.js-n2 {
    font-size: 60px;
    color: white;
}

.sm {
    display: flex;
    align-items: center;
    height: 216px;
    line-height: 44px;
    background-color: #403C4A;
    font-size: 24px;
    color: rgba(255, 255, 255, 0.5);
    padding: 0 30px;
    margin-top: 100px;
}
</style>
