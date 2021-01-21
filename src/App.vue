<template id="app">
  <div>
      <header class="header">
  <nav style="margin-top:-1.5rem">
    <div class="nav-wrapper">
      <ul>
        <li><a href="sass.html">Veterans</a></li>
        <li><a href="badges.html">Wellness</a></li>
        <li><a href="collapsible.html">Lifestyle</a></li>
      </ul>
    </div>
  </nav>
        <div class="header-content">
            <div id="header">
                <div class="row">
                    <div class="col s12" style="height:35em;">
                            <h3 style="text-align: center; margin-top: 3em; color: beige;">Experience, Knowledge, Commitment, Compassion</h3>
                            <!--<p class="p-heading p-large">Our family of communities remain entirely Covid free</p>
                            <a class="btn-solid-lg page-scroll" href="#contact">Contact Us</a>-->
                    </div> <!-- end of col -->
                </div> <!-- end of row -->
            </div> <!-- end of container -->
        </div> <!-- end of header-content -->
    </header>

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

.header {
  background: url('./assets/Indvillage-header.jpg') center;
  background-size: cover;
}

#post2 div:nth-child(2), #post3 div:nth-child(2), #post5 div:nth-child(2){
  padding-bottom: 4rem !important;
}



</style>