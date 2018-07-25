<template>
  <section class="background-color" :style="style">
    <div @mousemove="changeColorOnParent" class="selector-area">
      
    </div>
  </section>
</template>

<script>
import Toolbar from '~/components/Toolbar.vue'

export default {
  components: {
    Toolbar
  },
  data() {
    return {
      style: {
        backgroundColor: '#ffffff'
      },
      mousePos: {
        x: 0,
        y: 0
      }
    }
  },
  methods: {
    changeColorOnParent(event) {
      this.getMousePos(event);
      this.style.backgroundColor = this.calcColor(this.mousePos);
      console.log(this.style.backgroundColor);
    },
    getMousePos(event) {
      this.mousePos.x = 1 + Math.floor((event.offsetX / event.target.offsetWidth)*100);
      this.mousePos.y = 1 + Math.floor((event.offsetY / event.target.offsetHeight)*100);
    },
    calcColor(mousePos){
      //0,0 = 
      //
      const h = Math.floor(360 * (mousePos.x / 100));
      const s = '100%';
      const l = 100 - mousePos.y + '%';

      return 'hsl(' + h + ',' + s + ',' + l + ')';
    }
  }
}
</script>

<style lang="scss">
.background-color {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;

  .selector-area {
    width:100%;
    min-height: calc(100vh - 40px);
    border: solid 1px #000;
    margin: 20px;
  }
}
</style>

