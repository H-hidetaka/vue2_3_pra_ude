<template>
  <div>
    <button @click="increment">+</button>
    <button @click="addCount">+</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: () => ({
  }),
  methods:{
    increment(){
      this.$store.commit('increment')
    },
    addCount(){
      this.$store.commit('addcount', {
        value: 10
      })
    }
  }
}
</script>

<style>

</style>
