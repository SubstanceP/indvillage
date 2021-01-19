# indvillage

AppV2

<template>

  <div id="app"> 
  <nav>
    <div class="nav-wrapper">
      <a href="#" class="brand-logo">Logo</a>
      <ul id="nav-mobile" class="right hide-on-med-and-down">
        <li><a href="sass.html">Sass</a></li>
        <li><a href="badges.html">Components</a></li>
        <li><a href="collapsible.html">JavaScript</a></li>
      </ul>
    </div>
  </nav>
    <div class="row">
      <div class="col s12 test" v-for="(post, index) in posts" :key="index">
        <div class="img-container">
            <img class="col s5"
              v-if="post._embedded['wp:featuredmedia']"
              :src="post._embedded['wp:featuredmedia'][0].source_url"
            />
            
        </div>

          <div style="float:right;" class="col s5">
            <!--<h3>{{ post.title.renderered }}</h3>-->
            <h3 v-html="post.title.rendered"></h3>
            <div v-html="post.excerpt.rendered"></div>
          </div>
          <!--<div class="card-action">
            <a href="#">{{ post.title.rendered }}</a>
          </div>-->
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
      postsUrl: "http://indvillage.com/wp-json/wp/v2/posts",
      queryOptions: {
        per_page: 20,
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
        })
        .catch(error => {
          console.log(error);
        });
    },
    getPostDate(date) {
      return moment(date).format("111");
    }
  },
  mounted() {
    this.getRecentMessages();
  }
};
</script>

<style>
#app {
  padding:100px;
}

.test {
  margin-top:40px;
}

.post-img {
  
}
</style>


## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
