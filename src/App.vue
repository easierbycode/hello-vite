<template>
  <h1>CodeMonkey</h1>

  <select v-model="type">
    <option value="">ALL POSTS</option>
    <option>text</option>
    <option>quote</option>
    <option>link</option>
    <option>answer</option>
    <option>video</option>
    <option>audio</option>
    <option>photo</option>
    <option>chat</option>
  </select>

  <button v-if='offset != 0' @click="offset-=Number(limit)">&larrhk;</button>
  <button @click="offset+=Number(limit)">&rarrhk;</button>

  <select v-model="limit" @change="offset = 0">
    <option>5</option>
    <option>10</option>
    <option>15</option>
    <option>20</option>
  </select>

  / page

  <HelloWorld :offset="offset" :type="type" :limit='limit' />
</template>

<script lang='ts'>
import HelloWorld from './components/HelloWorld.vue'
export default {
  components: { HelloWorld },
  data: () => ({ 
    offset: 0,
    type: '',
    limit: 5
  })
}
</script>

<style scoped>
h1 {
  color: #4fc08d;
}
h1, p {
  font-family: Arial, Helvetica, sans-serif;
}
</style>