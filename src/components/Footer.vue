<template>
  <body class="d-flex flex-column">
  <!-- <div id="page-content">
    <div class="container text-center">
      <div class="row justify-content-center">
        <div class="col-md-7">
          <h1 class="fw-light mt-4 text-white">Sticky Footer using Flexbox</h1>
          <p class="lead text-white-50">Use just two Bootstrap utility classes and three custom CSS rules and you will have a flexbox enabled sticky footer for your website!</p>
        </div>
      </div>
    </div>
  </div> -->
  <footer id="sticky-footer" class="flex-shrink-0 py-4 bg-light text-white-50">
    <div class="container text-center">
      <small>Copyright &copy; KickingnScreaming</small>
    </div>
  </footer>
</body>
</template>

<script>
export default {

}
</script>

<style>


#page-content {
  flex: 1 0 auto;
}

/* Other Classes for Page Styling */

body {
  /* background: #007bff;
  background: linear-gradient(to right, #0062E6, #33AEFF); */
    background: black;
  box-shadow: 8px 8px 15px #e4e4e4, -8px -8px 15px #ffffff;
}

.container {
  color: aqua;
}
footer {
  z-index: 1000;
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
}
</style>