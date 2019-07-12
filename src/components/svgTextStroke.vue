<template>
  <svg class="svgAnimation" xmlns="http://www.w3.org/2000/svg" :style="styles">
  </svg>
</template>

<script>
export default {
  name: 'svgTextStroke',
  props: {
    msg: String,
    fontSize: String,
    lineHeight: {
      type: [String, Number],
      default: 1
    },
    letterSpacing: {
      type: [String, Number],
      default: 1
    },
    dy: {
      type: [String, Number],
      default: 'String'
    },
    fontColor: {
      type: String,
      default: '#000'
    },
    strokeColor: {
      type: String,
      default: '#000'
    }
  },
  methods : {
    setText (targetText) {
      if(targetText.match(/<br>/) ) {
        let repTextArray = this.msg.split(/\r\n|\r|\n|<br>/g);

        for(let i = 0; i < repTextArray.length; i++) {
          let dText = document.createElementNS("http://www.w3.org/2000/svg", "text");
          dText.innerHTML = repTextArray[i];
          dText.setAttribute('x', 0);
          dText.setAttribute('y', 0);
          dText.setAttribute('font-size', this.fontSize);
          dText.setAttribute('dominant-baseline', 'text-after-edge');

          this.$el.appendChild(dText);
        }
      }

      else {
        let dText = document.createElementNS("http://www.w3.org/2000/svg", "text");
        dText.innerHTML = this.msg;
        dText.setAttribute('x', 0);
        dText.setAttribute('y', 0);
        dText.setAttribute('font-size', this.fontSize);
        dText.setAttribute('dominant-baseline', 'text-after-edge');

        this.$el.appendChild(dText);
      }
    },

    setSize() {
      let $parent = this.$el;
      const dText = $parent.querySelectorAll('text');

      Array.from(dText, (e, index) => {
        let num = index + 1;
        const bbox = e.getBBox();

        if(this.lineHeight != 1) {
          num = num * this.lineHeight;
        }

        if(this.letterSpacing != 1) {
          $parent.setAttribute('viewBox', '0 0 ' + (bbox.width * this.letterSpacing) + ' ' + bbox.height * num);
          e.setAttribute('textLength', bbox.width * this.letterSpacing);
          $parent.setAttribute('width', bbox.width * this.letterSpacing);
        }
        else {
          $parent.setAttribute('viewBox', '0 0 ' + bbox.width + ' ' + bbox.height * num);
          $parent.setAttribute('width', bbox.width);
        }

        $parent.setAttribute('height', bbox.height * num);

        e.setAttribute('width', bbox.width);
        e.setAttribute('height', bbox.height);
        // e.setAttribute('x', bbox.x);
        e.setAttribute('y', bbox.height * num);
        if(this.dy != 1) {
          e.setAttribute('dy', this.dy);
        }
      });
    }
  },

  computed: {
    // バインドするスタイルを生成
    styles () {
      return {
        '--fill': this.fontColor,
        '--stroke': this.strokeColor
      }
    }
  },

  mounted() {
    this.setText(this.msg);

    setTimeout(() => {
      this.setSize();
    }, 500);

    setTimeout(() => {
      this.$el.classList.add('start');
    }, 1000);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">


svg {
  stroke: transparent;
  stroke-dasharray: 220;
  stroke-width: 0.5px;
  // stroke-opacity: 0;
  fill: transparent;

  text {
    line-height: 1;
  }
}

.start {
  --stroke: #000;
  stroke: var(--stroke);
  --fill: #000;
  fill: var(--fill);
  // fill: transparent;
  fill-opacity: 0;
  animation: lineAndFill 3000ms cubic-bezier(0.250, 0.460, 0.450, 0.940) 1 forwards;
}
@keyframes lineAndFill {
  0% {
    stroke-dashoffset: 220;
  }
  90% {
    stroke-dashoffset: 0;
    fill: transparent;
    fill-opacity: 0;
    // stroke-opacity: 1;
  }
  100% {
    fill-opacity: 1;
  }
}
</style>
