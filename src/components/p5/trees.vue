<template>
  <vue-P5
    class="planter"
    @setup="setup"
    @draw="draw"
    @mousedragged="mouseDragged"
    @mousemoved="mouseMoved"
  />
</template>

<script>
import VueP5 from "vue-p5";
export default {
  name: "Tree",
  components: {
    VueP5
  },
  data: () => {
    return {
      p5: {},
      plants: [],
      mouse: {x: 0, y: 0},
      pmouse: {x: 0, y: 0},
      Plant: class{
        constructor(p5, pos, angle) {
          this.pos = pos;
          this.angle = angle + p5.PI * 0.5;
          this.lifespan = 1;
          this.branches = [];
          this.up = -this.angle + p5.PI;
          this.makeBranch(p5, p5.createVector(), p5.random(20, 30), 0);
        }
        display(p5) {
          if (this.branches.length > 1) {
            if (this.lifespan > 0.01) {
              this.lifespan *= 0.9;
            }

            p5.push();
            //p5.translate(this.pos.x, this.pos.y);
            p5.translate(this.pos.x, this.pos.y);
            p5.rotate(this.angle);

            for (let i = this.branches.length - 1; i >= 0; i--) {
              //p5.stroke('#3CC787');
              //p5.stroke('#F2F2F2');
              //p5.stroke('#5C6975');
              p5.stroke(232);
              p5.fill("#3CC787");
              //p5.fill('#5C6975');
              p5.strokeWeight((this.branches.length - i) * 0.3);
              let b = this.branches[i];
              let base = b.base.copy();
              base.mult(1 - this.lifespan);
              let tip = b.tip.copy();
              tip.mult(1 - this.lifespan);

              p5.line(base.x, base.y, tip.x, tip.y);
              // leafs
              p5.noStroke();
              if (i > this.branches.length - 20) {
                let size = b.leaf.size * 6 - this.lifespan * 50;
                size = p5.max(0, size);
                p5.push();
                p5.translate(tip.x, tip.y);
                p5.rotate(b.leaf.angle + p5.PI * 1.5);
                p5.ellipse(0, size, size, size * 2);
                p5.pop();
              }
              // if(i == 0){
              // 	for (let i = 1; i >= 0; i-= 0.1) {
              // 		p5.strokeWeight(1);
              // 		p5.push();
              // 		p5.translate(base.x+i, base.y);
              // 		p5.rotate(p5.PI*i);
              // 		p5.line(i*5, 0, i*10, 5);
              // 		p5.pop();
              // 	}
              // }
            }
            p5.pop();
          }
        }
        shrinkBranch() {
          this.lifespan += 0.2;
        }
        makeBranch(p5, base, h, theta) {
          h *= p5.random(0.8, 0.9);
          // let theta = p5.random(p5.PI*0.5);
          let r = p5.PI * 0.4;
          theta += p5.random(-r, r);
          let desired = (this.up - theta) * 0.3; // force
          theta += desired;
          if (h > 15) {
            // ToDo make branch objects
            let tip = p5.createVector(0, h);
            tip.rotate(theta);
            tip.add(base);
            let leafSize = p5.random(0.5, 1);
            let leafAngle = theta + p5.random(-r, r);
            //p5.line(base.x, base.y, tip.x, tip.y);
            this.branches.push({
              base: base,
              tip: tip,
              leaf: { size: leafSize, angle: leafAngle }
            });
            this.makeBranch(p5, tip, h, theta);
            this.makeBranch(p5, tip, h, theta);
          }
        }
      }
    }
  },
  methods: {
    setup(p5) {
      this.p5 = p5;
      p5.createCanvas(800, 400);
      let pos = p5.createVector(200, 200);
      let plant = new this.Plant(p5, pos, 1);
      this.plants.push(plant);
    },
    draw(p5) {
      //p5.background(255);
      p5.clear();
      p5.strokeWeight(0.5);
      p5.stroke("#3CC787");
      //p5.stroke(0,232);
      p5.fill("#3CC787");

      p5.point(this.mouse.x, this.mouse.y);
      for (let i = this.plants.length - 1; i >= 0; i--) {
        this.plants[i].display(p5);
      }
      let numOfPlants = 30;
      if (this.plants.length > numOfPlants) {
        for (let i = 0; i <= this.plants.length - numOfPlants; i++) {
          this.plants[i].shrinkBranch();
          if (this.plants[i].lifespan > 1) {
            this.plants.splice(i, 1);
          }
        }
      }
    },
    mouseMoved({ mouseX, mouseY, pmouseX, pmouseY }) {
      this.mouse.x = mouseX;
      this.mouse.y = mouseY;
      this.pmouse.x = pmouseX;
      this.pmouse.y = pmouseY;
    },
    mouseDragged({ mouseX, mouseY, pmouseX, pmouseY }) {
      let m = this.p5.createVector(mouseX, mouseY);
      let pm = this.p5.createVector(pmouseX, pmouseY);
      let diff = pm.sub(m);
      let a = diff.heading();
      let plant = new this.Plant(this.p5, m, a);
      this.plants.push(plant);
      //console.log(this.plants);
    }
  }
}
</script>

<style lang="scss" scoped>

.planter {
  position: absolute;
  top: 0;
}
</style>