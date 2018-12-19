<template>
  <div class="col-md-4">
    <div class="card mb-4 shadow-sm">
      <div class="card-body card-body-bg-img" 
        v-bind:style="getBackgroundImageStyle" >
        <p class="card-text text-truncate">{{wallElement.text}}</p>
        <div class="d-flex justify-content-between align-items-center">
          <div class="text-muted">{{getPrettyDate(wallElement.created_at)}}</div>
          <div class="btn-group">
            <a type="button" v-bind:href="wallElement.resourceLink" class="btn btn-sm btn-outline-secondary">Ver</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'WallElement',
    props: ['wallElement', 'getPrettyDate'],
    data: function(){
      return {
        twitterDefaultImage: '/Twitter_Social_Icon_Square_Color.svg'
      }
    },
    computed: {
      getImageSource: function(){
        return this.wallElement.thumbnail.length ? this.wallElement.thumbnail : this.twitterDefaultImage;
      },
      getBackgroundImageStyle: function(){
        return 'background-image: linear-gradient(to bottom, rgba(255, 255, 255, 0.7), rgba(248, 249, 250, 1)), url('+ this.getImageSource + ')';
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  /*
    Wall elements
   */
  .source-icon {
    width: 2rem;
    height: 2rem;
  }

  .card-body-bg-img{
    background-repeat: no-repeat;
    background-size: cover;
  }
</style>
