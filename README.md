# vue-svg-textstroke

テキストのラインアニメーションをSVGで。  

[DEMO](https://mattune.github.io/vue-svg-textstroke/)

## 導入方法
1. /src/components/svgTextStroke.vue を任意の場所に追加。


## 使用方法
詳しくはApp.vueを参照  
```html
<svgTextStroke msg="表示する文字列"/>
```

## オプション
・font-size  
フォントサイズを指定
```html
<svgTextStroke msg="表示する文字列" font-size="30"/>
```

・stroke-color  
線の色を指定
```html
<svgTextStroke msg="表示する文字列" stroke-color="#f0f"/>
```

・font-color  
文字色を指定
```html
<svgTextStroke msg="表示する文字列" font-color="#f0f"/>
```

・letter-spacing  
字間を指定
```html
<svgTextStroke msg="表示する文字列" letter-spacing="1.5"/>
```

・line-height  
行間を指定
```html
<svgTextStroke msg="表示する文字列" line-height="1.5"/>
```

・dy  
文字の縦位置を指定  
フォントによって上下が切れたりするのを調整する時に使用する  
```html
<svgTextStroke msg="表示する文字列" dy="1.5"/>
```

・複数行  
brで改行させると複数行表示になる  
```html
<svgTextStroke msg="メロスは激怒した。<br>必ず、かの邪智暴虐（じゃちぼうぎゃく）の王を除かなければならぬと決意した。<br>メロスには政治がわからぬ。<br>メロスは、村の牧人である。<br>笛を吹き、羊と遊んで暮して来た。<br>けれども邪悪に対しては、人一倍に敏感であった。"/>
```

・delay  
delayを指定すると表示が徐々に表示される  
複数行の時も同様
```html
<svgTextStroke msg="時間差で徐々に表示するサンプルです。" delay="0.04"/>
```

```html
<svgTextStroke msg="メロスは激怒した。<br>必ず、かの邪智暴虐（じゃちぼうぎゃく）の王を除かなければならぬと決意した。<br>メロスには政治がわからぬ。<br>メロスは、村の牧人である。<br>笛を吹き、羊と遊んで暮して来た。<br>けれども邪悪に対しては、人一倍に敏感であった。" delay="0.04"/>
```