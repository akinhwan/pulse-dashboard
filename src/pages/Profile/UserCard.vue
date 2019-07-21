<template>
  <card type="user">
    <p class="card-text">
    </p>
    <div class="author">
      <div class="block block-one"></div>
      <div class="block block-two"></div>
      <div class="block block-three"></div>
      <div class="block block-four"></div>
      <a href="#">
        <img class="avatar" src="img/maryann.png" alt="...">
        <h5 class="title">Maryann Reese</h5>
      </a>
      <p class="description">
        President and Chief Executive Officer
      </p>
    </div>
    <p></p>
    <p class="card-description">
      She serves on the Missouri Hospital Association Board of Directors, Missouri Hospital Association Strategic Quality Advisory Committee, Cape Girardeau Chamber of Commerce Board, Cape Girardeau Chamber of Commerce Executive Committee, Boise State University Board of Ambassadors Advisory Council and Big Brothers Big Sisters of Eastern Missouri (BBBSEMO) Board.
    </p>
    <div slot="footer" class="button-container">
      <base-button icon round class="btn-facebook">
        <i class="fab fa-facebook"></i>
      </base-button>
      <base-button icon round class="btn-twitter">
        <i class="fab fa-twitter"></i>
      </base-button>
      <base-button icon round class="btn-google">
        <i class="fab fa-google-plus"></i>
      </base-button>
    </div>
  </card>
</template>
<script>
  export default {
    props: {
      user: {
        type: Object,
        default: () => {
          return {};
        }
      }
    }
  }
</script>
<style>
</style>
