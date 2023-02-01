<template>
  <div>
    <ImgSlide :option="option" />
  </div>
</template>

<script>
import ImgSlide from './components/ImgSlide.vue';

const BASE = `http://127.0.0.1:12010/../img`;

export default {
  name:'App',
  components: {
    ImgSlide
  },
  setup () {
    const option = {
      list:[{
        src:`${BASE}/butter.jpg`,
        name:"버터케이크",
        id:1
      },{
        src:`${BASE}/chocolate.jpg`,
        name:"초코케이크",
        id:2
      },{
        src:`${BASE}/strawberry.jpg`,
        name:"딸기케이크",
        id:3
      }],
      width:450,
      heigh:800
    }

    return {
      option
    }
  }
}
</script>

<style lang="css" scoped>

</style>