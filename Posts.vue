<template>
  <div class="container">
    <div class="row">
      <div class="col-md-8 col-md-offset-2">
        <div class="panel panel-default" v-for="post in laravelData.data">
          <div class="panel-heading" v-text="post.title"></div>

          <div class="panel-body" v-text="post.body">

          </div>
        </div>
        <pagination :data="posts" v-on:pagination-change-page="getResults"></pagination>
      </div>
    </div>
  </div>
</template>

<script>

//npm install laravel-vue-pagination
Vue.component('pagination', require('laravel-vue-pagination'));

export default {
  data() {
    return {
            // Our data object that holds the Laravel paginator data
            posts: {}
          }
        },

        created() {
        // Fetch initial results
        this.getResults();
      },

      methods: {
        // Our method to GET results from a Laravel endpoint
        getResults(page) {
          if (typeof page === 'undefined') {
            page = 1;
          }

            // Using vue-resource as an example
            axios.get('/posts?page=' + page)
            .then(response => {
              this.posts = response.data
            });
          }
        }
      }
    </script>
