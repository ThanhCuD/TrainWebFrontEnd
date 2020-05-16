<template>
<div>
  <ul v-if="posts && posts.length">
    <li v-for="post of posts" :key="post.id">
      <p><strong>{{post.date}}</strong></p>
      <p>{{post.temperatureC}}</p>
      <p>{{post.summary}}</p>
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
    axios.get(`https://localhost:44351/weatherforecast`)
    .then(response => {
      this.posts = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

