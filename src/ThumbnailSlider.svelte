<script>
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
      currTransl[i] = -200;
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
        img.style.opacity = "1";
        img.style.transform = "translate(" + (currTransl[i] + 200) + "px)";
        currTransl[i] = currTransl[i] + 200;
      }

      var outerImg = document.getElementsByClassName("img")[outerIndex];
      outerImg.style.transform =
        "translate(" + (currTransl[outerIndex] - 200 * amount) + "px)";
      outerImg.style.opacity = "0.5";
      currTransl[outerIndex] = currTransl[outerIndex] - 200 * amount;
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
        img.style.opacity = "1";
        img.style.transform = "translate(" + (currTransl[i] - 200) + "px)";
        currTransl[i] = currTransl[i] - 200;
      }
      var outerImg = document.getElementsByClassName("img")[outerIndex];
      outerImg.style.transform =
        "translate(" + (currTransl[outerIndex] + 200 * amount) + "px)";
      outerImg.style.opacity = "0.5";
      currTransl[outerIndex] = currTransl[outerIndex] + 200 * amount;
    }
  }
</script>

<style>
  .gallery {
    position: relative;
    height: 30vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  #carousel {
    width: 1000px;
    height: 200px;
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
    transform: translate(-200px);
    left: 200px;
  }

  #controls {
    position: absolute;
    z-index: 1;
    width: 200px;
  }

  #left {
    float: left;
    width: 33.3%;
  }

  #index {
    display: inline-block;
    width: 33.3%;
    text-align: center;
  }

  #right {
    float: right;
    width: 33.3%;
  }
</style>

<div class="gallery">
  <div id="carousel" class="animate">
    <img class="img animate" src="http://lorempixel.com/200/200/cats/1/" />
    <img class="img animate" src="http://lorempixel.com/200/200/cats/2/" />
    <img class="img animate" src="http://lorempixel.com/200/200/cats/3/" />
    <img class="img animate" src="http://lorempixel.com/200/200/cats/4/" />
    <img class="img animate" src="http://lorempixel.com/200/200/cats/5/" />
  </div>
  <div id="controls">
    <button id="left" on:click={left}>&lt</button>
    <span id="index">2</span>
    <button id="right" on:click={right}>&gt</button>
  </div>
</div>
