<template>
  <pre>page: {{(offset / limit) + 1}}</pre>

  <p v-for='post in posts' v-bind:key='post.id'>
    <pre v-if="post.type == 'video'" v-html="post.player[2].embed_code"></pre>

    <a v-if="post.type == 'link'" :href="post.url">
      <h3>{{post.title}}</h3>
      <em>{{post.excerpt}}</em>
    </a>

    <div v-if="post.type == 'text'" v-html="post.body"></div>
  </p>
</template>


<style lang="less">
// body {
//   display: flex;
//   flex-direction: column;
//   align-items: center
// }

#app {
  a { color: #0969da }
  &> h1 { text-align: center }
}
</style>


<script lang="ts">
import useSWRV from 'swrv';

interface TumblrJSON {
  meta: any,
  response: {
    blog: any,
    posts: any[]
  }
}

interface Pokemon {
  url: string,
  name: string
}

const url = 'https://api.tumblr.com/v2/blog/codemonkeygames.tumblr.com/posts/'
const api_key = '&api_key=GWDLyIP3XAXArF5oLyzFUTZsWycuAuKzuYRfBRCl5RrJkLShGf'

export default {
  name: 'HellowWorld',
  props: {
    offset: {
      type: Number,
      default: 0
    },
    type: {
      type: String,
      default: ''
    },
    limit: {
      type: Number,
      default: 5
    }
  },
  setup (props) {
    const { data: posts } = useSWRV<TumblrJSON>(() => `${url}${props.type}?offset=${props.offset}&limit=${props.limit}${api_key}`, key =>
      fetch(key)
        .then(res => res.json())
        .then(json => ({ ...(json.response.posts), url: key }))
    )
    return {
      posts,
      ...props
    }
  }
}
</script>