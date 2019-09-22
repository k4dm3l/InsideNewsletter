<template>
  <div class="home">
    <section>
      <div class="container-fluid">
        <h1 class="mt-5">Noticias reales, elegidas por humanos reales</h1>
        <p class="mt-4">Noticias, tendencias y enlaces que te ayudarán a mantenerte informado.</p>
        <div class="container mt-5">
          <hr />
        </div>
        <div class="row m-5">
          <div class="col-4" v-for="newsletter in newsletters" :key="newsletter.id">
            <CardNewsletter :card_newsletter_data="newsletter" />
            <ModalNewsletter :newsletter_subs_data="newsletter" />
          </div>
        </div>
      </div>
    </section>
    <div class="container mt-5">
      <hr />
    </div>
    <section>
      <div class="container-fluid">
        <h1 class="mt-5">Próximo y prometedor</h1>
        <p class="mt-4">Si estos boletines alcanzan sus objetivos (o consiguen un patrocinio), atraeremos a escritores expertos y los lanzaremos. Vote por todos sus favoritos:</p>
        <div class="container mt-5">
          <hr />
        </div>
        <div class="row m-5">
          <div class="col-4" v-for="next_newsletter in potential_newsletters" :key="next_newsletter.id">
            <CardNextNewsletter :card_next_newsletter_data="next_newsletter" />
            <VoteModalNewsletter :vote_newsletter_subs_data="next_newsletter" />
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import CardNewsletter from "@/components/CardNewsletter.vue";
import CardNextNewsletter from "@/components/CardNextNewsletter.vue";
import VoteModalNewsletter from "@/components/VoteModalNewsletter.vue";
import ModalNewsletter from "@/components/ModalNewsletter.vue";

import axios from "axios";

export default {
  name: "home",
  components: {
    Header,
    CardNewsletter,
    CardNextNewsletter,
    VoteModalNewsletter,
    ModalNewsletter
  },
  data() {
    return {
      url_end_point: `${process.env.VUE_APP_URL}/newsletters`,
      newsletters: [],
      potential_newsletters: []
    };
  },
  methods: {
    getAllNewsletters() {
      const endpoint = this.url_end_point;

      axios
        .get(endpoint)
        .then(response => {
          response.data.forEach(newsletter => {
            if((newsletter.target == 0) || (newsletter.target == newsletter.subscribed)){
              this.newsletters.push(newsletter);
            }
          });
        })
        .catch(err => {
          alert(err);
        });
    },
    getNextNewsletters() {
      const endpoint = this.url_end_point;

      axios
        .get(endpoint)
        .then(response => {
          response.data.forEach(newsletter => {
            if(newsletter.target > 0){
              this.potential_newsletters.push(newsletter);
            }
          });
        })
        .catch(err => {
          alert(err);
        });
    }
  },
  created() {
    this.getAllNewsletters();
    this.getNextNewsletters();
  }
};
</script>
<style scoped>
p {
  color: #cccccc;
  font-size: 1.3em;
}
</style>
