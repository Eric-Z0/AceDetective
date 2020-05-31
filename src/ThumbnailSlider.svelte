<script>
  import { onMount } from "svelte";

  let slide;
  let items = 4;
  let shiftValue;

  // Use sevlete onMount function to initilize the slider layout
  onMount(() => {
    var allBox = slide.children;
    var slideWidth = slide.offsetWidth;
    shiftValue = slideWidth / items;

    for (let i = 0; i < allBox.length; i++) {
      allBox[i].style.width = shiftValue + "px";
    }
  });

  var index = 0;
  var amount = 0; //amount of images
  var currTransl = [];
  var translationComplete = true;

  var transitionCompleted = function() {
    translationComplete = true;
  };

  document.addEventListener("DOMContentLoaded", function(event) {
    amount = document.getElementById("carousel").children.length;
    document.getElementsByTagName("span")[0].innerHTML = amount;
    for (var i = 0; i < amount; i++) {
      currTransl[i] = -1 * shiftValue;
      document
        .getElementsByTagName("img")
        [i].addEventListener("transitionend", transitionCompleted, true);
      document
        .getElementsByTagName("img")
        [i].addEventListener("webkitTransitionEnd", transitionCompleted, true);
      document
        .getElementsByTagName("img")
        [i].addEventListener("oTransitionEnd", transitionCompleted, true);
      document
        .getElementsByTagName("img")
        [i].addEventListener("MSTransitionEnd", transitionCompleted, true);
    }
    console.log("DOM fully loaded and parsed");
  });

  function right() {
    if (translationComplete === true) {
      translationComplete = false;
      index--;
      if (index == -1) {
        index = amount - 1;
      }
      var outerIndex = index % amount;
      document.getElementById("index").innerHTML =
        outerIndex === 0 ? 5 : outerIndex;
      for (var i = 0; i < amount; i++) {
        var img = document.getElementsByClassName("img")[i];
        // img.style.opacity = "1";
        img.style.transform =
          "translate(" + (currTransl[i] + shiftValue) + "px)";
        currTransl[i] = currTransl[i] + shiftValue;
      }

      var outerImg = document.getElementsByClassName("img")[outerIndex];
      outerImg.style.transform =
        "translate(" + (currTransl[outerIndex] - shiftValue * amount) + "px)";
      // outerImg.style.opacity = "0.5";
      currTransl[outerIndex] = currTransl[outerIndex] - shiftValue * amount;
    }
  }

  function left() {
    if (translationComplete === true) {
      translationComplete = false;
      index++;
      var outerIndex = (index - 1) % amount;
      document.getElementById("index").innerHTML = outerIndex + 1;
      for (var i = 0; i < amount; i++) {
        var img = document.getElementsByClassName("img")[i];
        // img.style.opacity = "1";
        img.style.transform =
          "translate(" + (currTransl[i] - shiftValue) + "px)";
        currTransl[i] = currTransl[i] - shiftValue;
      }
      var outerImg = document.getElementsByClassName("img")[outerIndex];
      outerImg.style.transform =
        "translate(" + (currTransl[outerIndex] + shiftValue * amount) + "px)";
      // outerImg.style.opacity = "0.5";
      currTransl[outerIndex] = currTransl[outerIndex] + shiftValue * amount;
    }
  }
</script>

<style>
  .gallery {
    position: relative;
    height: 22vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  #carousel {
    height: 100%;
    display: flex;
    justify-content: center;
    overflow: hidden;
  }

  .animate {
    -webkit-transition-duration: 1s;
    -moz-transition-duration: 1s;
    -o-transition-duration: 1s;
    transition-duration: 1s;
    -webkit-transition-property: -webkit-transform;
    -moz-transition-property: -moz-transform;
    -o-transition-property: -o-transform;
    transition-property: transform;
  }

  img {
    position: relative;
    float: left;
    left: 448px; /* A hard coded value, may change it later */
    height: 100%;
    object-fit: cover;
    transform: translate(
      -448px
    ); /* A hard coded value, may change it later */
  }

  #controls {
    position: absolute;
    z-index: 1;
    width: 448px;
    color: red;
  }

  button {
    background-color: transparent;
    border: none;
    margin-bottom: 0;
    height: 200px;
    color: white;
    font-size: 2em;
    cursor: pointer;
    opacity: 0.6;
  }

  button:hover {
    opacity: 1;
    transition: opacity 0.5s;
  }

  button:active {
    background-color: transparent;
    /* font-size: 2.5em; */
  }

  #left {
    float: left;
    width: 15%;
  }

  #index {
    display: inline-block;
    width: 70%;
    text-align: center;
  }

  #right {
    float: right;
    width: 15%;
  }
</style>

<div class="gallery">
  <div id="carousel" class="animate" bind:this={slide}>
    <img
      class="img animate"
      src="images/sherlock_holmes.jpg"
      alt="Sherlock Holmes" />
    <img
      class="img animate"
      src="images/kogoro_akechi.jpg"
      alt="Kogoro Akechi" />
    <img
      class="img animate"
      src="images/kosuke_kindaichi.jpg"
      alt="Kosuke Kindaichi" />
    <img
      class="img animate"
      src="images/hercule_poirot.jpg"
      alt="Hercule Poirot" />
    <img
      class="img animate"
      src="images/jules_maigret.jpg"
      alt="Jules Maigret" />
  </div>
  <div id="controls">
    <button id="left" on:click={left}>&lt</button>
    <span id="index">2</span>
    <button id="right" on:click={right}>&gt</button>
  </div>
</div>
