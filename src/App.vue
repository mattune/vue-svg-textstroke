<template>
  <div id="app">
    <svgTextStroke class="wf-noto" msg="日常的に使うための飽きのこない、それでいてちょっと気になるデザイン。" font-size="30"/>
    <hr>
    <svgTextStroke class="wf-hannari" msg="あかるく、やさしく、ふんわり。" font-size="30" stroke-color="#f0f"/>
    <hr>
    <svgTextStroke class="wf-kokoro" msg="わたしのふたつのじんかくにはきょうつうのきおくがある。" font-size="30"/>
    <hr>
    <svgTextStroke class="wf-nikukyu" msg="ピョンピョン" font-size="30" dy="-5" font-color="#f0f"/>
    <hr>
    <svgTextStroke class="wf-nicomoji" msg="いらっしゃいませ" font-size="40" letter-spacing="1.5"/>
    <hr>
    <svgTextStroke msg="メロスは激怒した。<br>必ず、かの邪智暴虐（じゃちぼうぎゃく）の王を除かなければならぬと決意した。<br>メロスには政治がわからぬ。<br>メロスは、村の牧人である。<br>笛を吹き、羊と遊んで暮して来た。<br>けれども邪悪に対しては、人一倍に敏感であった。" font-size="20" line-height="1.5"/>
  </div>
</template>

<script>
import svgTextStroke from './components/svgTextStroke.vue'

export default {
  name: 'app',
  components: {
    svgTextStroke
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Noto+Sans+JP&display=swap');
@import url('https://fonts.googleapis.com/earlyaccess/hannari.css');
@import url('https://fonts.googleapis.com/css?family=Sawarabi+Mincho');
@import url('https://fonts.googleapis.com/earlyaccess/kokoro.css');
@import url('https://fonts.googleapis.com/earlyaccess/nikukyu.css');
@import url('https://fonts.googleapis.com/earlyaccess/nicomoji.css');

#app {
  padding: 50px;

  hr {
    border-bottom: 2px solid #000;
    margin: 50px 0;
  }
}

.wf-hannari { font-family: "Hannari"; }
.wf-noto { font-family: 'Noto Sans JP'; }
.wf-sawarabimincho { font-family: "Sawarabi Mincho"; }
.wf-kokoro { font-family: "Kokoro"; }
.wf-nikukyu { font-family: "Nikukyu"; }
.wf-nicomoji { font-family: "Nico Moji"; }

</style>
