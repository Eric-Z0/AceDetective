<script>
  import { onMount } from "svelte";

  let gallery;
  let len;
  let current = 1;
  let shiftValue = -200;
  let slide;
  let test = true;

  onMount(() => {
    var items = gallery.children[0].children;
    len = items.length;

    var first = items[0];
    var second = items[1];
    var last = items[len - 1];
    var secondlast = items[len - 2];

    first.before(secondlast.cloneNode(true));
    first.before(last.cloneNode(true));
    last.after(second.cloneNode(true));
    last.after(first.cloneNode(true));

    console.log(slide.style.left);
  });


  function ButtonClick() {
    var cycle = false;
    var delta = this.id === "prev" ? -1 : 1;
    test = true;
    shiftValue += -100 * delta;

    // slide.style.left = shiftValue + "px";

    current += delta;

    cycle = current === 0 || current > len;
    console.log(cycle);

    if (cycle) {
      if (current == 0) {
        current = len;
      } else {
        current = 1;
      }
      test = false;
      setTimeout(() => {shiftValue = -100 * (current + 1);}, 500);
      
    }
  }
</script>

<style>

  .test {
    transition: 500;
  }
  
  #gallery {
    position: relative;
    width: 100px;
    height: 100px;
    border: 1px green dotted;
    margin: 30px 0 0 300px;
    /* usually an «overflow:hidden» is set here */
  }

  #overflow:checked + #gallery {
    overflow: hidden;
  }

  #gallery ul {
    font-size: 0;
    white-space: nowrap;
    position: absolute;
    top: 0;
    left: -200px;
    margin: 0;
    padding: 0;
    /* transition: all 0.8s linear; */
  }

  #gallery li {
    display: inline-block;
    vertical-align: top;
    width: 96px;
    height: 96px;
    white-space: normal;
    padding: 2px;
  }

  button {
    font: 40px "Courier New";
    border: 1px #d8d8d8 dotted;
    color: #626262;
    background: none;
    cursor: pointer;
    width: 50px;
    text-align: center;
    margin: 20px -150px 0 150px;
  }

  label,
  a {
    font: 14px Georgia;
    font-style: italic;
    color: #626262;
  }
</style>

<div>
  <label for="overflow">
    This checkbox toggles
    <b>overflow: hidden</b>
    property on the gallery
    <br />
    to see the effect when a mask is applied:
  </label>
  <input type="checkbox" id="overflow" />

  <div id="gallery" bind:this={gallery}>
    <!-- mask -->
    <ul id="slide" bind:this={slide} style="left: {shiftValue}px" class:test>
      <!-- container -->
      <li>
        <img src="http://dummyimage.com/96x96/f0f0f0/626262.png&text=1" />
      </li>
      <li>
        <img src="http://dummyimage.com/96x96/f0f0f0/626262.png&text=2" />
      </li>
      <li>
        <img src="http://dummyimage.com/96x96/f0f0f0/626262.png&text=3" />
      </li>
      <li>
        <img src="http://dummyimage.com/96x96/f0f0f0/626262.png&text=4" />
      </li>
    </ul>
  </div>

  <button type="button" id="prev" on:click={ButtonClick}>&laquo;</button>
  <button type="button" id="next" on:click={ButtonClick}>&raquo;</button>

  <p>
    <a href="http://stackoverflow.com/a/15877302/1098851">
      Further information about this demo on this Stackoverflow discussion
    </a>
  </p>
</div>
