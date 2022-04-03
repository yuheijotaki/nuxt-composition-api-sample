<template>
  <ul>
    <li v-for="item in data" :key="item.title">
      <h1>{{ item.title }}</h1>
      <div>
        <img
          :src="item.image"
          :alt="item.title"
          width="220"
        />
        <dl>
          <dt>Description</dt>
          <dd>{{ item.description }}</dd>
          <dt>Continent</dt>
          <dd>{{ item.continent }}</dd>
          <dt>Height</dt>
          <dd>{{ item.height }}</dd>
          <dt>Countries</dt>
          <dd>{{ item.countries.join(', ') }}</dd>
        </dl>
      </div>
    </li>
  </ul>
</template>

<script>
import {
  defineComponent,
  useStatic,
  computed,
} from '@nuxtjs/composition-api'

import axios from 'axios'

export default defineComponent({
  setup() {
    const param = computed(() => 'hoge')
    const keyBase = 'fuga'
    const data = useStatic(
      async (param, key) => {
        console.log(param) // hoge
        console.log(key) // fuga-hoge
        const mountains = await axios.get(`https://api.nuxtjs.dev/mountains`)
        return mountains.data
      },
      param,
      keyBase
    )
    return { data }
  }
})
</script>

<style scoped>
ul {
  list-style: none;
}
li {
  padding: 4rem;
}
li:nth-child(even) {
  background-color: #f0f0f0;
}
h1 {
  color: #333;
  font-size: 1.6rem;
}
div {
  display: flex;
}
img {
  margin-top: 1rem;
  flex-shrink: 0;
  display: inline-block;
  margin-right: 2rem;
}
dl {
  margin-top: .5rem;
  font-size: 1.2rem;
}
dl dt {
  float: left;
  padding-top: .25rem;
  color: #666;
}
dl dd {
  margin-left: 8rem;
  padding-top: .25rem;
}
</style>
