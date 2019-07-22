<template>
  <svg class="svgAnimation" xmlns="http://www.w3.org/2000/svg">
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
      default: 0
    },
    delay: {
      type: [String, Number],
      default: 0
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
          let sText = document.createElementNS("http://www.w3.org/2000/svg", "text");

          if(this.delay != 0) {
            const splitTxtArray = repTextArray[i].split('');

            for(let i = 0; i < splitTxtArray.length; i++) {
              let tSpan = document.createElementNS("http://www.w3.org/2000/svg", "tspan");
              tSpan.innerHTML = splitTxtArray[i];
              tSpan.style.setProperty('animation-delay', i*this.delay+'s');
              tSpan.style.setProperty('fill', this.fontColor);
              tSpan.style.setProperty('stroke', this.strokeColor);
              sText.appendChild(tSpan);
            }
          }
          else {
            let tSpan = document.createElementNS("http://www.w3.org/2000/svg", "tspan");
            tSpan.innerHTML = repTextArray[i];
            tSpan.style.setProperty('fill', this.fontColor);
            tSpan.style.setProperty('stroke', this.strokeColor);
            sText.appendChild(tSpan);
          }

          sText.setAttribute('x', 0);
          sText.setAttribute('y', 0);
          sText.setAttribute('font-size', this.fontSize);
          sText.setAttribute('dominant-baseline', 'text-after-edge');

          this.$el.appendChild(sText);
        }
      }

      else {
        let sText = document.createElementNS("http://www.w3.org/2000/svg", "text");

        if(this.delay != 0) {
          const splitTxtArray = targetText.split('');

          for(let i = 0; i < splitTxtArray.length; i++) {
            let tSpan = document.createElementNS("http://www.w3.org/2000/svg", "tspan");
            tSpan.innerHTML = splitTxtArray[i];
            tSpan.style.setProperty('animation-delay', i*this.delay+'s');
            tSpan.style.setProperty('fill', this.fontColor);
            tSpan.style.setProperty('stroke', this.strokeColor);
            sText.appendChild(tSpan);
          }

        }
        else {
          let tSpan = document.createElementNS("http://www.w3.org/2000/svg", "tspan");
          tSpan.innerHTML = targetText;
          tSpan.style.setProperty('fill', this.fontColor);
          tSpan.style.setProperty('stroke', this.strokeColor);
          sText.appendChild(tSpan);
        }

        sText.setAttribute('x', 0);
        sText.setAttribute('y', 0);
        sText.setAttribute('font-size', this.fontSize);
        sText.setAttribute('dominant-baseline', 'text-after-edge');

        this.$el.appendChild(sText);
      }
    },

    setSize() {
      let $parent = this.$el;
      const sText = $parent.querySelectorAll('text');
      let maxWidthArry = [];

      Array.from(sText, (e, index) => {
        let num = index + 1;
        const bbox = e.getBBox();

        if(this.lineHeight != 1) {
          num = num * this.lineHeight;
        }

        if(this.letterSpacing != 1) {
          maxWidthArry.push(bbox.width * this.letterSpacing);
          e.setAttribute('textLength', bbox.width * this.letterSpacing);
        }
        else {
          maxWidthArry.push(bbox.width);
        }
        $parent.setAttribute('viewBox', '0 0 ' + Math.max(...maxWidthArry) + ' ' + bbox.height * num);
        $parent.setAttribute('width', Math.max(...maxWidthArry));
        $parent.setAttribute('height', bbox.height * num);

        e.setAttribute('width', bbox.width);
        e.setAttribute('height', bbox.height);
        e.setAttribute('y', bbox.height * num);
        if(this.dy != 1) {
          e.setAttribute('dy', this.dy);
        }
      });
    }
  },

  mounted() {
    this.setText(this.msg);

    setTimeout(() => {
      this.setSize();
    }, 500);
  }
}
</script>


<style lang="scss">
.svgAnimation {
stroke: transparent;
stroke-opacity: 0;

  tspan {
    stroke: transparent;
    stroke-dasharray: 220;
    stroke-width: 0.5px;
    // stroke-opacity: 0;
    fill: transparent;
    fill-opacity: 0;
  }

  text {
    stroke: transparent;
    stroke-opacity: 0;
  }

  &.start {
    tspan {
      stroke: var(--stroke);
      fill: var(--fill);
      fill-opacity: 0;
      animation: lineAndFill 3000ms cubic-bezier(0.250, 0.460, 0.450, 0.940) 1 forwards;
    }
  }
}


@keyframes lineAndFill {
  0% {
    stroke-dashoffset: 220;
    stroke-opacity: 1;
  }
  90% {
    stroke-dashoffset: 0;
    fill: transparent;
    fill-opacity: 0;
    stroke-opacity: 1;
  }
  100% {
    fill-opacity: 1;
    stroke-opacity: 1;
  }
}
</style>
