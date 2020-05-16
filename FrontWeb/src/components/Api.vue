<template>
<div>
  <ul v-if="posts && posts.length">
    <li v-for="post of posts" :key="post.id">
      <p><strong>{{post.title}}</strong></p>
      <p>{{post.body}}</p>
    </li>
  </ul>

  <ul v-if="errors && errors.length" > 
    <li v-for="error of errors" :key="error.id">
      {{error.message}}
    </li>
  </ul>
</div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Api',
  data() {
    return {
      posts: [],
      errors: []
    }
  },

  // lấy dữ liệu khi component được tạo thành công
  created() {
    axios.get(`http://jsonplaceholder.typicode.com/posts`)
    .then(response => {
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

