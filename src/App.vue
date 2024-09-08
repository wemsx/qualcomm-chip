<script setup>
import { computed, ref } from "vue";
import { qualcomm8 } from "./static/8.json"
import { qualcomm6 } from "./static/6.json"
import { contributors } from "./static/contributors.json"
let series = ['8', '6']
const model = ref('8')
let dateEnd = '2024.08.25'

const platforms = {
  "8": qualcomm8.reverse(),
  "6": qualcomm6.reverse()
}

/*const portraitMode = computed(() => { return window.innerWidth > window.innerHeight })
const isInMobileMode = computed(() => { return /Mobile/i.test(navigator.userAgent) })
const isInChromeCore = computed(() => { return /Chrome/i.test(navigator.userAgent) })
const isShowFullScreenBtn = computed(() => { return this.isInChromeCore && !this.isInMobileMode })*/
</script>

<template>
  <div class="card-container" :style="heightApp === 0 ? '' : `height: ${heightApp}px`">
    <div class="copyright">
      <div>
        <div class="title mb-6">
          <img src="/qualcomm-logo.svg" alt="qualcomm logo" style="transform: scale(1.8);">
          <h1>高通 {{ model }} 系列处理器<br>参数大全</h1>
        </div>

        <div class="type-switch mb-6">
          <div v-for="item in series">
          <div @click="model = item" :class="['switch', { active: model === item }]"><img
              src="/qualcomm-placeholder.svg" :alt="item"></div>
        </div></div>
      </div>

      <div class="contributors" style="text-align: center;">
        感谢以下的贡献者：
        <p v-for="item in contributors" class="author">{{ item }}<br/></p>
      </div><br/>

      <div class="author">
        <p>
          <a class="link" target="_blank" href="https://en.wikipedia.org/wiki/Apple-designed_processors">wikipedia</a> ·
          <a class="link" target="_blank" href="https://github.com/KyleBing/apple-chip">Github</a> ·
          <a class="link" href="http://kylebing.cn">@kylebing</a> · Origin Project
          <br/>
          <a class="link" target="_blank" href="https://github.com/wemsx/qualcomm-chip">Github</a> ·
          <a class="link" href="http://kylebing.cn">@wemsx</a> · Modified
        </p>
        <p>·</p>
        <!--                <p>-->
        <!--                    <a class="link" href="http://kylebing.cn/tools/apple-watch">Watch</a>-->
        <!--                </p>-->
        <p>
          <span>2020.06.05</span> ~
          <span>{{ dateEnd }}</span>
        </p>
        <!--<p>·</p>
        <p>Q群：<a class="link" target="_blank" href="https://jq.qq.com/?_wv=1027&k=Z8E0HrWA">920084833</a></p>-->
      </div>
    </div>
    <!-- CHIP LIST -->
    <div class="chip" v-for="(item, index) in platforms[model]" :key="`item.name-${index}`">
      <div class="chip-img">
        <img :src="item.img == '' ? item.img : '/qualcomm-placeholder.svg'" :alt="item.name">
      </div>

      <div class="chip-name">
        <h2>{{ item.name }}</h2>
        <p>{{ item.model || '-' }}</p>
        <p>{{ item.release }}</p>
      </div>


      <div class="cpu-gpu-group">
        <div class="cpu-list">
          <div class="cpu" v-for="(cpu, index) in item.cpu" :key="index">
            <div class="tag">CPU</div>
            <div class="fire">
              {{ cpu.name }}
            </div>
            <div class="freq">{{ cpu.rate }} </div>
            <div class="num info">x {{ cpu.core }} </div>
          </div>
        </div>

        <div class="gpu-list">
          <div class="gpu" v-for="(gpu, index) in item.gpu.reverse()" :key="index">
            <div class="tag">GPU</div>
            <div class="brand"><span>{{ gpu.brand || '-' }}</span><span v-if="gpu.freq"> x {{ gpu.freq }} MHz</span></div>
            <div class="info" v-if="gpu.info">{{ gpu.info }}</div>
          </div>
        </div>

      </div>

      <div class="info-list-group">
        <div class="info-list">
          <div :class="['info-item', { 'invalid': !item.ai.rate }]">
            <div class="key">AI</div>
            <div class="value" v-if="item.ai.rate">× {{ item.ai.core }} {{ item.ai.rate }}</div>
          </div>
          <div :class="['info-item', { 'invalid': !item.baseband }]">
            <div class="key">基带</div>
            <div class="value" v-if="item.baseband">{{ item.baseband }}</div>
          </div>
        </div>

        <div class="info-list">
          <div :class="['info-item', { 'invalid': !item.isa }]">
            <div class="key">内核架构</div>
            <div class="value">{{ item.isa }}</div>
          </div>
          <div :class="['info-item', { 'invalid': !item.dieSize }]">
            <div class="key">内核大小</div>
            <div class="value">{{ item.dieSize }} <span class="unit">mm<sup>2</sup></span></div>
          </div>
          <div :class="['info-item', { 'invalid': !item.tech }]">
            <div class="key">技术工艺</div>
            <div class="value"><span v-if="item.techCompany">{{ item.techCompany }} - </span>{{ item.tech }} 纳米</div>
          </div>
          <div :class="['info-item', { 'invalid': !item.transistorCount }]">
            <div class="key">晶体管数</div>
            <div class="value" v-if="item.transistorCount">{{ item.transistorCount }}<span class="unit">亿</span></div>
          </div>
        </div>


        <div class="info-list">
          <div :class="['info-item', { 'invalid': !item.os.init }]">
            <div class="key">初始系统</div>
            <div class="value">{{ item.os.init }}</div>
          </div>
          <div :class="['info-item', { 'invalid': !item.os.latest }]">
            <div class="key">最终系统</div>
            <div class="value">{{ item.os.latest }}</div>
          </div>
        </div>
      </div>


      <!--设备列表-->
      <div class="device">
        <div class="device-title">运行设备</div>
        <div class="device-list">
          <div class="device-item" v-for="(device, index) in item.devices" :key="'device' + index">{{ device }}</div>
        </div>
      </div>
    </div>

    <div class="gap"></div>
  </div>
</template>

<style scoped></style>
