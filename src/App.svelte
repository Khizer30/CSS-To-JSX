<script lang="ts">
  // ...
  import "./styles/styles.css" ;

  // Variables
  let css: string = "" ;
  let jsx: string = "" ;
  let error: string = "" ;
  let words: string[] = [] ;
  let selected: string[] = [] ;

  // Reactive
  $:
  {
    words = css.trim().split(" ") ;
    selected = [] ;

    createJSX() ;
  }

  // Select
  function select(word: string): void
  {
    let index: number = selected.indexOf(word) ;

    if (index === -1)
    {
      selected.push(word) ;
    }
    else
    {
      selected.splice(index, 1) ;
    }

    createJSX() ;

    // Render
    selected = selected ;
  }

  // Create JSX
  function createJSX(): void
  {
    let temp: string = css.trim() ;

    // Remove Selected
    for (let i: number = 0; i < selected.length; i++)
    {
      temp = temp.replaceAll(`${ selected[i] } `, "") ;
      temp = temp.replaceAll(` ${ selected[i] }`, "") ;
      temp = temp.replaceAll(selected[i], "") ;
    }

    // Add Selected
    let newTemp: string = temp ? `className={ "${ temp } "` : `className={ ` ;

    if (selected.length === 0)
    {
      newTemp = `className={ "${ temp }"` ;
    }

    for (let i: number = 0; i < selected.length; i++)
    {
      newTemp += ` + styles.${ selected[i] }` ;
    }

    if (selected.length === words.length)
    {
      newTemp = newTemp.replace(" + ", "") ;
    }

    newTemp += ` }` ;

    // Render
    if (newTemp !== `className={ "" }`)
    {
      jsx = newTemp ;
    }
    else
    {
      jsx = "" ;
    }
  }

  // Copy
  function copy(): void
  {
    navigator.clipboard.writeText(jsx) ;
    error = "JSX Copied!" ;

    // Reset
    css = "" ;
    jsx = "" ;
    setTimeout(() => { error = "" }, 1750) ;
    words = [] ;
    selected = [] ;
  }
</script>

<nav class="navbar navbar-light navbar-expand-md">
  <div class="container-fluid">
    <h1 class="navbar-brand navHeading"> CSS To JSX </h1>
  </div>
</nav>

<div class="container-fluid d-flex justify-content-center align-items-center mainContainer">
  <form method="post" target="_self" class="width80"
  enctype="application/x-www-form-urlencoded" autocomplete="off" novalidate>

  { #if error }
    <p class="error"> { error } </p>
  { :else }
    <p class="error"> <br /> </p>
  { /if }

    <input
      name="css"
      type="text"
      bind:value={ css }
      maxlength="500"
      minlength="0"
      placeholder="Enter CSS Here..."
      required
      autofocus
      class="form-control textInput"
    />

    <div class="d-flex justify-content-evenly align-items-center">
    { #each words as word }
      { #if (word !== "") }
        <button on:click={ () => select(word) } type="button" class="mainBtn"> { word } </button>
      { :else }
        <button type="button" class="mainBtn hidden"> NULL </button>
      { /if }
    { /each }
    </div>
    
    <input
      name="jsx"
      type="text"
      bind:value={ jsx }
      maxlength="500"
      minlength="0"
      placeholder="Your JSX Will Appear Here..."
      required
      class="form-control textInput"
    />

    <div class="d-flex justify-content-evenly align-items-center">
    { #if jsx }
      <button on:click={ copy } type="button" class="d-flex justify-content-center align-items-center copyBtn">
        <i class="far fa-copy"></i>
      </button>
    { :else }
      <button type="button" class="d-flex justify-content-center align-items-center copyBtn hidden">
        <i class="far fa-copy"></i>
      </button>
    { /if }
    </div>

  </form>
</div>