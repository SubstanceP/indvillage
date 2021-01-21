<template id="app">
  <div>
    <header class="header">
      <nav style="margin-top:-1.5rem; background-color:transparent;">
        <div class="nav-wrapper" style="background-color:none;">
          <ul class="flexnav">
            <li><a href="#post1">Veterans</a></li>
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
      <div class="container" style="line-height:1.66rem;">
      <h2>Independence Village</h2>
      <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>
      <p>It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution of letters, as opposed to using 'Content here, content here', making it look like readable English. Many desktop publishing packages and web page editors now use Lorem Ipsum as their default model text, and a search for 'lorem ipsum' will uncover many web sites still in their infancy. Various versions have evolved over the years, sometimes by accident, sometimes on purpose (injected humour and the like).
      </p>
      </div>
    </div>
    <div class="row container">
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
  }
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

.container {
  width:88% !important;
}

.flexnav{
  display: flex;
  justify-content: flex-end;
}


</style>