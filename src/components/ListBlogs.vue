<template>
  <div id="show-blogs" v-theme:column="'wide'">
      <h1>List Blog Titles</h1>
      <input type="text" v-model="search" placeholder="Search blog...">
      <div class="single-blog" v-for="blog in filteredBlogs">
          <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
      </div>
  </div>
</template>

<script>
import SearchMixin from '../mixins/searchMixin'
export default {
 
  data () {
    return {
      blogs: [],
      search:''
    }
  },
  methods:{

  },
  created(){
      this.$http.get('https://jsonplaceholder.typicode.com/posts').then(function(data){
          this.blogs=data.body.slice(0,10)
      })
  },

  computed:{

  },

  filters:{
    toUppercase(value){
      return value.toUpperCase()
    }
  },

  directives:{
    'rainbow':{
        bind(el, binding, vnode) {
    el.style.color='#'+Math.random().toString().slice(2,8)
  }
    }
  },
  mixins:[SearchMixin]
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}
.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
}
input{
  width: 96%;
}
</style>
