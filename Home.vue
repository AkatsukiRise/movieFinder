<template>
  <div class='home'>
    <div class='feature_card'>
      <router-link to='/movie/tt040591'>
        <img src='https://mir-s3-cdn-cf.behance.net/project_modules/disp/6ae75746996947.586cfecbef3b1.jpg' alt='La-La-Land' class='feature_img'>
        <div clas='detail'>
          <h3>La La Land</h3>
          <p>Mia, an aspiring actress, serves lattes to movie stars in between auditions and Sebastian, a jazz musician, scrapes by playing cocktail party gigs in dingy bars, but as success mounts they are faced with decisions that begin to fray the fragile fabric of their love affair, and the dreams they worked so hard to maintain in each other threaten to rip them apart</p>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.home {
  .feature_card {
    position: relative;

    .feature_img {
      display: block;
      width: 100%;
      height: 19rem;
      object-fit: cover;
      postition: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 1rem;
      z-index: 1;

      h3 {
        color: #FFF;
        margin: 1rem;
      }

      p {
        color: #FFF;
      }
    }
  }
}
</style>
