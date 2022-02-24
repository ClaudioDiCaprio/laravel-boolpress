<template>
  <div>
      <h1>{{post.title}}</h1>
      <img :src="`/storage/${post.image}`" :alt="post.title">
      <p>
          {{post.content}}
      </p>
  </div>
</template>

<script>
export default {
    name:"SinglePost",
    data() {
        return {
            post: {}
        }
    },
    created() {
        // console.log(this.$route.params.slug);
        //localhost:8000/api/posts/slug
        axios.get(`/api/posts/${this.$route.params.slug}`)
            .then( (response) => {
                this.post = response.data;
        });
    }
}
</script>

<style>

</style>