<template>
  <div class="home">
    <Header/>
    <div class="container-fluid">
      <h1 class="mt-5">Noticias reales, elegidas por humanos reales</h1>
      <p class="mt-4">Noticias, tendencias y enlaces que te ayudarán a mantenerte informado.</p>
      <div class="container mt-5">
        <hr>
      </div>
      <div class="row m-5">
        <div class="col-4" v-for="newsletter in newsletters" :key="newsletter.id">
          <CardNewsletter :card_newsletter_data="newsletter"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue';
import CardNewsletter from '@/components/CardNewsletter.vue';
import axios from 'axios';

export default {
    name: 'home',
    components: {
      Header,
      CardNewsletter
    },
    data(){
      return {
        url_end_point: `${process.env.VUE_APP_URL}/newsletters`,
        newsletters: []
      }
    },
    methods: {
      getAllNewsletters(){
        const endpoint = this.url_end_point;

        axios.get(endpoint)
          .then(response => {
            this.newsletters = response.data;
          })
          .catch(err => {
            alert(err);
          });
      },
      seeData(data){
        console.log(data);
      }
    },
    created(){
      this.getAllNewsletters();
    }
}
</script>
<style scoped>
  p {
    color: #cccccc;
    font-size: 1.3em;
  }
</style>
