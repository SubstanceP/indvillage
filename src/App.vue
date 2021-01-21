<template>
  <div id="app">
    <nav>
    <div class="nav-wrapper">
      <a href="#" class="brand-logo">Logo</a>
      <ul>
        <li><a href="sass.html">Sass</a></li>
        <li><a href="badges.html">Components</a></li>
        <li><a href="collapsible.html">JavaScript</a></li>
      </ul>
    </div>
  </nav> 
    <div class="row">
      <div class="col s4 m4" v-for="(post, index) in posts" :key="index" :id="'post'+index">
        <div class="card" id="test">
          <div class="card-image">
            <img
              v-if="post._embedded['wp:featuredmedia']"
              :src="post._embedded['wp:featuredmedia'][0].source_url"
            />
          </div>
          

          <div class="card-content" v-html="post.excerpt.rendered"></div>
          <div class="card-action">
            <a href="#">{{ post.title.rendered }}</a>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";

export default {
  data() {
    return {
      postsUrl: "https://indvillage.com/wp-json/wp/v2/posts",
      queryOptions: {
        per_page: 6,
        page: 1,
        _embed: true     
      },
      
      posts: []
      
    };
  },
  methods: {
    // Get recent posts from wp
    getRecentMessages() {
      axios
        .get(this.postsUrl, { params: this.queryOptions })
        .then(response => {
          this.posts = response.data;
          console.log("Posts retreieved!");
          console.log(this.posts);
          if (this.posts[5])
            console.log("great");
          else
            console.log("nope");
          })
          
          //document.getElementById("test").id = "testing";
        
        .catch(error => {
          console.log(error);
        });
    },
    getPostDate(date) {
      return moment(date).format("111");
    },
    

  },
  mounted() {
    this.getRecentMessages();
  },
  /*setPostID() {
    document.getElementById("test").id = "testing";
    return console.log(document.getElementById("testing"));
   
  }*/
};


  


</script>

<style>
#app {
  padding:100px;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

.test {
  font-weight:bold;
}

</style>