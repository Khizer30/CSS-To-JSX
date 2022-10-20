<script lang="ts">
  // ...
  import "./styles/styles.css" ;
</script>

<nav class="navbar navbar-light navbar-expand-md">
  <div class="container-fluid">
    <h1 class="navbar-brand navHeading"> CSS To JSX </h1>
  </div>
</nav>

<div class="container-fluid d-flex justify-content-center align-items-center mainContainer">
  <form method="post" target="_self" class="width80"
  enctype="application/x-www-form-urlencoded" autocomplete="off" novalidate>

    <p class="error"> Error </p>

    <input
      name="names"
      type="text"
      value=""
      maxlength="500"
      minlength="0"
      placeholder="CSS"
      required
      autofocus
      class="form-control textInput"
    />

    <div class="d-flex justify-content-evenly align-items-center">
      <button type="button" class="mainBtn"> mainDiv </button>
    </div>
    
    <input
      name="names"
      type="text"
      value=""
      maxlength="500"
      minlength="0"
      placeholder="JSX"
      required
      class="form-control textInput"
    />

    <div class="d-flex justify-content-evenly align-items-center">
      <button type="button" class="d-flex justify-content-center align-items-center copyBtn">
        <i class="far fa-copy"></i>
      </button>
    </div>

  </form>
</div>