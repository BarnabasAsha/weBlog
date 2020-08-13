<template>
  <div class="main-post">
    <router-link :to="`/`">Home</router-link>
    <h2>{{post.title}}</h2>
    <p>{{post.body}}
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Lacus laoreet non curabitur gravida arcu ac tortor dignissim. Risus commodo viverra maecenas accumsan lacus vel facilisis volutpat est. Sed vulputate mi sit amet mauris. Purus ut faucibus pulvinar elementum. Blandit libero volutpat sed cras. Elementum integer enim neque volutpat ac tincidunt.<br><br>
Id consectetur purus ut faucibus. Neque laoreet suspendisse interdum consectetur libero id. Metus dictum at tempor commodo ullamcorper a. Tincidunt ornare massa eget egestas purus. Cras tincidunt lobortis feugiat vivamus at augue eget. Porttitor rhoncus dolor purus non enim praesent elementum facilisis leo. Faucibus pulvinar elementum integer enim neque volutpat. Porttitor massa id neque aliquam. Lectus mauris ultrices eros in.</p>
    <div class="comment-section">
      <h3>Comments({{comments.length}})</h3>
      <div class="comment-box">
        <div class="comment" v-for="comment in comments" :key="comment.id">
          <h4>{{comment.email}}</h4>
          <p>{{comment.body}}</p>
        </div>
      </div>
      <div class="add-comment">
      <span class="error"></span>
      <input type="email" name="" id="email" placeholder="Enter Email">
      <textarea name="" id="comment" cols="30" rows="10" placeholder="Enter Comment"></textarea>
      <button type="submit" @click="addComment">Comment</button>
    </div>
    </div>
  </div>
</template>

<script>

export default {
  data () {
    return {
      id: this.$route.params.id,
      post: {},
      comments: []
    }
  },
  created () {
    this.getPost()
    this.getComments()
  },
  methods: {
    getPost () {
      fetch(`https://jsonplaceholder.typicode.com/posts/${this.id}`)
        .then(res => { return res.json() })
        .then(data => { this.post = data })
    },
    getComments () {
      fetch(`https://jsonplaceholder.typicode.com/posts/${this.id}/comments`)
        .then(response => { return response.json() })
        .then(data => { this.comments = data })
    },
    addComment () {
      const emailValue = document.getElementById('email')
      const commentValue = document.getElementById('comment')
      const send = { email: emailValue.value, body: commentValue.value }
      if (emailValue.value === '' || commentValue.value === '') {
        document.querySelector('.error').textContent = 'Please fill all fields'
        setTimeout(() => {
          document.querySelector('.error').style.display = 'none'
        }, 2000)
        return null
      } else {
        this.comments.push(send)
        emailValue.value = ''
        commentValue.value = ''
      }
    }
  }
}
</script>

<style scoped>
  .main-post {
    width: 60%;
    margin: auto;
  }
  .main-post h2 {
    font-size: 1.8rem;
    font-weight: 600;
    line-height: 2.4rem;
    text-transform: capitalize;
  }

  .main-post p {
    font-size: 1.2rem;
    line-height: 2rem;
    font-weight: 500;
    letter-spacing: 1px;
  }

  .comment-section {
    margin-top: 3em;
    width: 80%;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
  }

  .comment {
    width: 85%;
    background: #fff;
    margin-left: 3em;
    margin-bottom: 1em;
    padding: 1.5em 2em;
    border-radius: 10px;
  }

  .comment h4 {
    margin: 0;
    margin-bottom: 3px;
  }

  .comment p {
    margin: 0;
    margin-top: 0;
    color: #2b2b2b;
    font-size: 0.9rem;
    line-height: 1.4rem;
  }

  .add-comment {
    align-self: flex-end;
    display: flex;
    align-items: flex-end;
    flex-direction: column;
    margin-left: 3em;
    margin-top: 1em;
  }

  .add-comment input {
    width: 300px;
    padding: 7px 10px;
    border: 1px solid #030303;
    border-radius: 5px;
    margin-bottom: 1em;
  }
  .add-comment textarea {
    width: 300px;
    height: 80px;
    padding: 7px 10px;
    border: 1px solid #030303;
    border-radius: 5px;
  }

  .add-comment button {
    border: none;
    background: #2b2b2b;
    color: #fff;
    border-radius: 5px;
    height: 35px;
    width: 80px;
    margin-top: 0.5em;
    cursor: pointer;
  }

  .error {
    align-self: flex-start;
    color: rgba(255, 0, 0, 0.719);
  }

  @media screen and (max-width: 1200px) {
    .main-post {
      width: 90%;
    }
  }

  @media screen and (max-width: 600px) {
    .main-post {
      width: 90%;
    }

    .main-post h2 {
      font-size: 1.4rem;
      line-height: 2rem;
    }

    .main-post p {
      font-size: 1.1rem;
    }

    .add-comment {
      margin-left: 0;
    }

    .comment-section {
      width: 100%;
    }

    .comment-box {
      width: 100%;
    }

    .comment {
      margin-left: 0;
      padding: 10px;
      width: 100%;
    }

    .comment p {
      font-size: 0.8rem;
    }

    .comment-section {
      display: block;
    }

    .add-comment {
      align-self: center;
      align-items: center;
      justify-content: center;
    }

    .add-comment button {
      align-self: flex-end;
    }
  }

  @media screen and (max-width: 350px) {
    .add-comment input, .add-comment textarea {
      width: 250px;
    }
  }

</style>
