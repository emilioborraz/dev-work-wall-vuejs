<template>
  <main role="main" id="wallApp">
    <section class="jumbotron text-center">
      <div class="container">
        <h1 class="jumbotron-heading">Código, reflexiones e inspiración.</h1>
        <p class="lead text-muted">
          El ingenio no tiene límites, en ingeniería, un resultado excelente se basa en saber cumplir las necesidades del usuario e ir mas allá!
        </p>
        <p>
          <a href="#" class="btn btn-primary my-2">Prueba tu suerte</a>
        </p>
      </div>
    </section>
    <div class="album py-5 bg-light">
      <div class="container">
        <div class="row">
          <wall-element
            v-for="wallElement in wallElements"
            v-bind:key="wallElement.id"
            v-bind:wall-element="wallElement"
            v-bind:get-pretty-date="getPrettyDate"
            ></wall-element>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
  import WallElement from './components/WallElement.vue'
  import axios from 'axios'

  let $http = axios

  export default {
    name: 'app',
    components: {
      WallElement
    },
    data: function() {
      return {
        version: 1.0,
        wallElementsLoaded: false,
        dataFeedUrl: 'http://borrazb.test',
        wallElements: []
      };
    },
    methods:{
        getPrettyDate: function(dateString){
            let dateObject = new Date(Date.parse(dateString));
            return dateObject.getDate()+'/'+dateObject.getMonth()+'/'+dateObject.getFullYear();
        }
    },
    mounted:
      function(){
        $http
        .get(this.dataFeedUrl)
        .then(response => {
          this.wallElementsLoaded = true;
          this.wallElements = response.data;
        })
        .catch(error => {
          this.wallElementsLoaded = error
        })
        .finally(() => this.wallElementsLoaded = false)
      }
  }
</script>

<style>
  /**
   * Todo: from CSS to SCSS
   */
  :root {
    --jumbotron-padding-y: 3rem;
  }
  /*
    Header
   */
  .jumbotron {
    padding-top: var(--jumbotron-padding-y);
    padding-bottom: var(--jumbotron-padding-y);
    margin-bottom: 0;
    background-color: #fff;
    background-size: cover;
  }
  @media (min-width: 300px) {
    .jumbotron {
      background-image: linear-gradient(to bottom, rgba(255, 111, 26, 0.2), rgba(248, 249, 250, 1)),url(./assets/hero_bg_xsmall.jpg);
    }
  }
  @media (min-width: 576px) {
    .jumbotron {
      background-image: linear-gradient(to bottom, rgba(255, 111, 26, 0.2), rgba(248, 249, 250, 1)),url(./assets/hero_bg_small.jpg);
    }
  }
  @media (min-width: 768px) {
    .jumbotron {
      padding-top: calc(var(--jumbotron-padding-y) * 2);
      padding-bottom: calc(var(--jumbotron-padding-y) * 2);
      background-image: linear-gradient(to bottom, rgba(255, 111, 26, 0.2), rgba(248, 249, 250, 1)),url(./assets/hero_bg_medium.jpg);
    }
  }
  @media (min-width: 1200px) {
    .jumbotron {
      padding-top: calc(var(--jumbotron-padding-y) * 2);
      padding-bottom: calc(var(--jumbotron-padding-y) * 2);
      background-image: linear-gradient(to bottom, rgba(255, 111, 26, 0.2), rgba(248, 249, 250, 1)),url(./assets/hero_bg_large.jpg);
    }
  }

  .jumbotron p:last-child {
    margin-bottom: 0;
  }

  .jumbotron-heading {
    font-weight: 300;
  }

  .jumbotron .container {
    max-width: 40rem;
  }

  /*
    Footer
   */
  footer {
    padding-top: 3rem;
    padding-bottom: 3rem;
  }

  footer p {
    margin-bottom: .25rem;
  }
</style>

