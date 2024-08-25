<template>
<div class="copyright">
<div>
    <div class="title mb-6">
        <img src="/qualcomm-logo.svg" alt="qualcomm logo" style="transform: scale(1.8);">
        <h1>高通 {{model}} 系列处理器<br>参数大全</h1>
    </div>

    <div class="type-switch mb-6">
        <div @click="switchModels('A')" :class="['switch', {active: model === 'A'}]"><img :src="model === 'A'? 'imgs/icon/A/active.png': 'imgs/icon/A/default.png?v=2' " alt="A"></div>
    </div>
</div>

<div class="author">
    <p>
        <a class="link" target="_blank" href="https://en.wikipedia.org/wiki/Apple-designed_processors">wikipedia</a> ·
        <a class="link" target="_blank" href="https://github.com/KyleBing/apple-chip">github</a> ·
        <a class="link" href="http://kylebing.cn">kylebing</a>
    </p>
    <p>·</p>
<!--                <p>-->
<!--                    <a class="link" href="http://kylebing.cn/tools/apple-watch">Watch</a>-->
<!--                </p>-->
    <p>·</p>
    <p>
        <span>2020.06.05</span> ~
        <span>{{dateEnd}}</span>
    </p>
    <p>·</p>
    <p>Q群：<a class="link" target="_blank" href="https://jq.qq.com/?_wv=1027&k=Z8E0HrWA">920084833</a></p>
</div>
</div>
</template>
<script setup>
let dateEnd = '2024.08.25'
const model = '8'
</script>
<style scoped>

</style>