<template>
  <div class="toolbar">
    <h1>{{ value }}</h1>
    <i-Button size="large" shape="circle" :icon="icon" @click="onClick"></i-Button>
    <Slider class="slider" :value.sync="value" :min="2010" :max="2016" show-stops></Slider>
  </div>
</template>


<script>
export default {
  data () {
    return {
      icon: 'play'
    }
  },

  computed: {
    value: {
      get () {
        return this.$store.state.year
      },

      set (newValue) {
        this.$store.commit('changeYear', {year: newValue})
      }
    }
  },

  methods: {
    onClick () {
      this.icon = this.icon === 'play' ? 'pause' : 'play'
      const animate = () => {
        if (this.icon === 'play') return

        this.value = (this.value + 1 - 2010) % 7 + 2010
        setTimeout(animate, 500)
      }

      setTimeout(animate, 500)
    }
  }
}
</script>


<style scoped>
.toolbar {
  width: 500px;
  padding: 10px;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.8);
}

h1 {
  text-align: center;
}

.slider {
  display: inline-block;
  vertical-align: middle;
  width: 430px;
  margin-left: 5px;
}
</style>
