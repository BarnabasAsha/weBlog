<template>
  <div class="container">
    <h2>Posts</h2>
      <div v-for="(post, index) in getPosts" :key="index" class="post-container">
          <!-- <div class="img">
              <img src="" alt="">
          </div> -->
          <router-link :to="`/post/${post.id}`">{{post.title}}</router-link>
      </div>
  </div>
</template>

<script>
export default {
  props: {
    getPosts: Array
  }
}
</script>

<style scoped>

.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 80%;
    margin: auto;
}

.post-container {
    width: 700px;
    margin: 1em;
    border: 1px solid #4e4e4e77;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 1em;
    border-radius: 10px;
}

.post-container a {
    text-decoration: none;
    font-size: 1.2rem;
    font-weight: 700;
    color: #030303;
    text-transform: capitalize;
}

@media screen and (max-width: 1000px) {
    .post-container {
      width: 100%;
    }
}
@media screen and (max-width: 500px){
    .container {
      width: 90%;
    }

    .container a {
      font-size: 1rem;
    }
}
</style>
