<template>
  <div class="home">
    <Posts :getPosts="postStore" />
  </div>
</template>

<script>
import Posts from '../components/posts'
export default {
  name: 'Home',
  components: {
    Posts
  },
  data () {
    return {
      postStore: []
    }
  },
  mounted () {
    fetch('https://jsonplaceholder.typicode.com/posts/')
      .then((response) => { return response.json() })
      .then((data) => { this.postStore = data.slice(0, 15) })
  }
}
</script>
