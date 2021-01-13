<template>
  <div class="container">
    <div class="p5Canvas"></div>
  </div>
</template>

<script>
import P5 from 'p5';

export default {
  data() {
    return {
      p5Canvas: null,
    }
  },
  created() {
    const sketch = p5 => {
        let w = 2000;
        let h = 1500;
        p5.setup = () => {
            p5.createCanvas(w, h);
            p5.background(102);
        },

        p5.draw = () => {
            p5.changeBG(p5.mouseX, p5.mouseY);
            p5.variableEllipse(p5.mouseX, p5.mouseY, p5.pmouseX, p5.pmouseY);
            
        },

        p5.variableEllipse = (x, y, px, py) =>{
            let speed = p5.abs(x - px) + p5.abs(y - py);
            p5.stroke(speed);
            p5.ellipse(x, y, speed, speed);
        }
        p5.changeBG = (x, y) => {
          let _x = p5.map(x, 0, w, 0, 255);
          let _y = p5.map(y, 0, h, 0, 255);
          p5.background(_x, _y, 1);
        }
    };

    this.p5Canvas = new P5(sketch, 'p5Canvas');
  },
  unmounted () {
    this.p5Canvas = null;
  },
}
</script>

<style>
#p5Canvas {
  width: 100vw;
  position: relative;
}

main {
  margin: 0 auto;
  width: 90vw;
}
</style>