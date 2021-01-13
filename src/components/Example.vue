<template>
  <div>
    <vue-p5
        @preload="preload"
        @setup="setup"
        @draw="draw"
        @keypressed="keyPressed"
        @mousemoved="mouseMoved"
        @mousedragged="mouseDragged">
    </vue-p5>
    <p>
      Red: {{ red }} <br/>
      Green: {{ green }} <br/>
      Blue: {{ blue }} <br/>
    </p>
    <p>
      Press <button @click="toggleRed()">button</button> to toggle red color <br/>
      Press <code>g</code> to toggle green color <br/>
      Use mouse to draw lines <br/>
    </p>
  </div>
</template>
<script>
import VueP5 from "vue-p5";

export default {
  name: "p5-example",
  components: {
    "vue-p5": VueP5
  },
  data: () => ({
    red: 0,
    green: 255,
    // blue color is a computed property that changes over time
    lines: [],
    p5LogoImage: null,
    startTime: Date.now(),
    // store current time in data to force computed properties to update
    currentTime: Date.now(),
  }),
  computed: {
    msSinceStart() {
      return this.currentTime - this.startTime;
    },
    blue() {
      return Math.floor(this.msSinceStart * 0.03) % 255;
    },
    p5LogoRotationAngle() {
      return this.msSinceStart * 0.0001 % Math.PI * 2;
    }
  },
  methods: {
    // preload(sketch) {
    //   this.p5LogoImage = sketch.loadImage("static/p5js.png");
    // },
    setup(sketch) {
      let d = 70;
      let p1 = d;
      let p2 = p1 + d;
      let p3 = p2 + d;
      let p4 = p3 + d;
      sketch.createCanvas(720, 400);
      sketch.background(0);
      sketch.noSmooth();

      sketch.translate(140, 0);

      // 绘制灰色的方块
      sketch.stroke(153);
      sketch.line(p3, p3, p2, p3);
      sketch.line(p2, p3, p2, p2);
      sketch.line(p2, p2, p3, p2);
      sketch.line(p3, p2, p3, p3);

      // 绘制白色的点
      sketch.stroke(255);
      sketch.point(p1, p1);
      sketch.point(p1, p3);
      sketch.point(p2, p4);
      sketch.point(p3, p1);
      sketch.point(p4, p2);
      sketch.point(p4, p4);
    },
    // draw(sketch) {
    //   this.currentTime = Date.now();

    //   const { red, green, blue } = this;
    //   sketch.background(red, green, blue);

    //   const logoWidth = sketch.width / 3;
    //   const logoHeight = sketch.height / 3;

    //   // logo should be in the middle of the screen and rotated
    //   sketch.translate(sketch.width / 2, sketch.height / 2);
    //   sketch.rotate(this.p5LogoRotationAngle);
    //   sketch.image(this.p5LogoImage, -logoWidth / 2, -logoHeight/2, logoWidth, logoHeight);
    //   sketch.resetMatrix();

    //   for (let line of this.lines) {
    //     sketch.stroke(line.color);
    //     sketch.line(line.pmouseX, line.pmouseY, line.mouseX, line.mouseY);
    //   }
    // },
    // keyPressed({ keyCode }) {
    //   // 'g' key
    //   if (keyCode === 71) {
    //     this.toggleGreen();
    //   }
    // },
    // mouseMoved({ mouseX, mouseY, pmouseX, pmouseY }) {
    //   this.pushLine({ mouseX, mouseY, pmouseX, pmouseY, color: 0 });
    // },
    // mouseDragged({ mouseX, mouseY, pmouseX, pmouseY }) {
    //   this.pushLine({ mouseX, mouseY, pmouseX, pmouseY, color: 255 });
    // },
    // toggleRed() {
    //   this.red = 255 - this.red;
    // },
    // toggleGreen() {
    //   this.green = 255 - this.green;
    // },
    // pushLine(line) {
    //   let lines = this.lines;
    //   lines.push(line);
    //   this.lines = lines.slice(-100);
    // }
  }
};
</script>
