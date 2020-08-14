<template>
  <div class="container">
    <h2>Posts</h2>
    <div class="wrapper">
<div v-for="(post, index) in getPosts" :key="index" class="post-container">
          <div class="tag">
              <span>Science</span>
              <span>Technology</span>
          </div>
          <router-link :to="`/post/${post.id}`">{{post.title}}</router-link>
      </div>
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
    height: 150px;
    margin: 1em;
    border: 1px solid #4e4e4e77;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    padding: 1em;
    border-top-right-radius: 10px;
    border-top-left-radius: 10px;
    position: relative;
}

.post-container::after {
  position: absolute;
  content: '';
  top: 0;
  right: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #03030336;
}

.wrapper >
:nth-child(even) {
  background: url(../assets/post-img.jpg);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.wrapper >
:nth-child(odd) {
  background: url(../assets/post-img2.png);
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

.post-container a {
    text-decoration: none;
    font-size: 1.1rem;
    font-weight: 700;
    color: #fff;
    text-transform: capitalize;
    z-index: 10;
}

.tag {
  color: #fff;
  font-size: 0.8rem;
}

.tag :nth-child(even) {
  background: red;
  padding: 5px;
}

.tag :nth-child(odd) {
  background: blueviolet;
  padding: 5px;
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

    .wrapper >
:nth-child(even) {
  background: url(../assets/mobile-post-img.jpg);
}

.wrapper >
:nth-child(odd) {
  background: url(../assets/post-img-mobile.jpg);
}

    .container a {
      font-size: 1rem;
    }
}
</style>
