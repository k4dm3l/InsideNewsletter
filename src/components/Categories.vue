<template>
  <div class="container-categories container-fluid d-flex p-3">
    <ul class="categorie-list align-self-start" v-for="(tag, index) in tags" :key="tag.id">
      <li v-if="index == 0 && index <= 8">
          <a href="/">All</a>
      </li>
      <li v-else>
          <a href="#">{{ tag.name }}</a>
      </li>
    </ul>
  </div>
</template>
<script>
    import axios from 'axios';

    export default {
        name: 'navbar-categories',
        data(){
            return {
                url_end_point: `${process.env.VUE_APP_URL}/tags`,
                tags: []
            }
        },
        methods: {
            getTags(){
                const endpoint = this.url_end_point;
                axios.get(endpoint)
                    .then(response => {
                        this.tags = response.data;
                    })
                    .catch(err => {
                        alert(err)
                    });
            }
        },
        created(){
            this.getTags();
        }
    };
</script>
<style scoped>
    .container-categories {
        background: #ff5c03;
        box-shadow: 0 4px 2px -2px gray;        
    }

    .categorie-list li {
        display: inline;
        margin: 1.3em;
    }

    li a {
        color: #fff;
        text-decoration: none;
    }

    li a:hover {
        color: #000;
        transition: 0.5s;
    }
</style>