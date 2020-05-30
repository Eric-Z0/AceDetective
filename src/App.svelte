<script>
  import NarBar from "./NarBar.svelte";
  import Gallery from "./Gallery.svelte";
  import Banner from "./Banner.svelte";
  import Story from "./Story.svelte";
  import ThumbnailSlider from "./ThumbnailSlider.svelte";
  import Slider from "./Slider.svelte";
  export let name;
</script>

<style>
  .main {
    position: relative;
    top: 10vh;
  }

  .slide {
    height: 60vh;
    width: 100%;
    display: flex;
    align-content: center;
    justify-content: center;
  }
</style>

<NarBar />
<div class="main">
  <div class="slide">
    <div>
      <h2>Banner Section</h2>
    </div>
  </div>
  <!-- <Gallery></Gallery> -->
  <ThumbnailSlider />
  <!-- <Slider></Slider> -->
  <Story />
  <Banner />
</div>
