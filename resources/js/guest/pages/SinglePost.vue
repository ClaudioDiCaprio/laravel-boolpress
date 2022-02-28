<template>
  <div class="container">
      <h1>{{post.title}}</h1>
      <img :src="`/storage/${post.image}`" :alt="post.title">
      <p>
          {{post.content}}
      </p>
       <div>
          <h3>Comment</h3>
          <form @submit.prevent="addComment()">
              <div>
                    <input type="text" id="name" placeholder="Insert Name" v-model="formData.name">
              </div>              
              <div>
                  <textarea  id="content" cols="30" rows="10" placeholder="Insert text *" v-model="formData.content"></textarea>
                  <div v-if="formErrors.content" style="background: red;color: white;">
                      <ul>
                          <li v-for="(error,index) in FormErrors.content" :Key="index">
                              {{error}}
                          </li>
                      </ul>
                  </div>
              </div>
              
              <div>
                  <button type="submit">Add Comment</button>
              </div>
          </form>
          <div v-show="commentSent" style="background: green; color: #fff; text-align: center;">
              Comment submitted to approvation!Thank you!!!
          </div>
      </div>
  </div>
</template>

<script>
export default {
    name:"SinglePost",
    data() {
        return {
            post: {},
            formData: {
                name:"",
                content:"",
                post_id: null
            },
            commentSent: false,
            formErrors: {}
        }
    },
    methods: {
        addComment() {
            // alert("add a comment")
            // /api/comments
            axios.post(`/api/comments`, this.formData).then( (response) => {
                //puliti i campi
                this.formData.name = "";
                this.formData.content = "";
                //mostro l'avviso di avvenuto inserimento
                this.commentSent= true;
            }).catch( (error) => {
                //handle error
                // console.log(error.response.data.errors);
                this.formErrors = error.response.data.errors;

            })           
        }
    },
    created() {
        // console.log(this.$route.params.slug);
        //localhost:8000/api/posts/slug
        axios.get(`/api/posts/${this.$route.params.slug}`)
            .then( (response) => {
                this.post = response.data;
                this.formData.post_id = this.post.id;
            }).catch( (error) => {
                //handle error
                this.$router.push({name:"page-404"});
            })
    }
}
</script>

<style>

</style>