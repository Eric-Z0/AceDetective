<script>
  import { onMount } from "svelte";

  let slide;
  let initial = -178.25;
  let items = 4;
  let imgArrLen = 4;
  let shiftUnit;
  let shiftValue = shiftUnit;
  let current = 1; // A counter declared to decide the recycle time

  // Use sevlete onMount function to initilize the slider layout
  onMount(() => {
    initSlider();
  });

  function initSlider() {
    var allBox = slide.children;
    var slideWidth = slide.offsetWidth;
    shiftUnit = slideWidth / items;
    shiftValue = shiftUnit;
    for (let i = 0; i < allBox.length; i++) {
      allBox[i].style.width = shiftUnit + "px";
    }

    // Clone the first and last two image elements
    // Note: need to clone at least first and last image to make infinite loop slider function
    var first = allBox[0];
    var second = allBox[1];
    var last = allBox[4];
    var secondlast = allBox[3];

    first.before(secondlast.cloneNode(true));
    first.before(last.cloneNode(true));
    last.after(second.cloneNode(true));
    last.after(first.cloneNode(true));

    // slide.style.transform = "translateX(" + initial + "px)";
    shiftValue = shiftUnit * 1 * -1;
  }

  function sliderButtonClick() {
    var delta = this.id === "prev" ? -1 : 1;
    shiftValue += shiftUnit * delta * -1;
    current += delta;

    var cycle = current === 0 || current > imgArrLen;

    if (cycle) 
    {
      if (current == 0) 
      {
        current = imgArrLen;
      } else 
      {
        current = 1;
      }
      shiftValue = shiftUnit * (current + 1) * -1;
    }
  }
</script>

<style>
  .wrapper {
    /* height: 30vh;
    display: flex;
    align-items: center;
    justify-content: center; */
  }

  .slider {
    width: 365px;
    height: 200px;
    border: 1px green dotted;
    position: relative;
    /* background: aquamarine; */
    background: #000;
    /* overflow: hidden; */
  }

  .btn-container {
    display: flex;
    justify-content: center;
  }

  .slider-btn {
    display: flex;
    cursor: pointer;
  }

  .slide {
    position: absolute;
    white-space: nowrap;
    height: 200px;
    transition: all 1s linear;
  }

  .slide img {
    display: inline-block;
    white-space: normal;
    opacity: 0.6;
    height: 200px;
    object-fit: cover;
    /* transform: scale(1.15); */
    transition: transform 0.5s, opacity 0.5s;
    /* padding: 0 25px; */
  }

  .slide img:hover {
    opacity: 1;
    transform: scale(1.05);
  }
</style>

<div class="btn-container">
  <button id="prev" class="slider-btn" on:click={sliderButtonClick}>&lt</button>
  <button id="next" class="slider-btn" on:click={sliderButtonClick}>&gt</button>
</div>
<div class="wrapper">
  <div class="slider">
    <div class="slide" bind:this={slide} style="left: {shiftValue}px">
      <img
        src="https://img5.goodfon.com/wallpaper/nbig/1/33/by-beth193-sherlock-sherlock-bbc-sherlock-holmes-sherlock--1.jpg"
        alt="Sherlock Holmes" />
      <img
        src="https://aramajapan.com/wp-content/uploads/2015/09/aramajapan_movie.jpg"
        alt="Kogoro Akechi" />
      <img
        src="https://img.cinematoday.jp/a/N-A-PQj2XjSk/_size_r1200x630/_v_1540488894/main.jpg"
        alt="Kosuke Kindaichi" />
      <img
        src="https://ichef.bbci.co.uk/images/ic/1200x675/p01l5gt5.jpg"
        alt="Hercule Poirot" />
      <img
        src="https://pmcdeadline2.files.wordpress.com/2019/07/123519.jpg?w=620&h=383&crop=1"
        alt="Jules Maigret" />
    </div>
  </div>
</div>
