<template>
  <header class="container header">
      <h2>I'm the header</h2>
     <a href="/admin/home"><button class="cho" >Reserved Area</button></a>
     <nav>
       <ul>
          <li>
              <router-link :to="{ name: 'home' }">Home</router-link>
          </li>
          <li>
              <router-link router-link :to="{ name: 'about' }">About us</router-link>
          </li>
          <li>
              <router-link router-link :to="{ name: 'categories' }">Categories</router-link>
          </li>
       </ul>
     </nav>
  </header>
</template>

<script>
export default {
    name:"Header"
}
</script>

<style lang="scss" scoped>
.header {
    margin-bottom:20px;
    border-bottom: 2px solid;

        .cho {
                background-color: lightgreen;
                padding: 10px;
                border-radius: 20px;
                border:0;
        }
}


</style>