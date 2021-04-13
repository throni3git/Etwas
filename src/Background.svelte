<script lang="ts">
  import { afterUpdate, beforeUpdate } from "svelte";
  import { fade } from "svelte/transition";

  export let bgColorHue: number = 10;
  let fromColorHue = bgColorHue;
  let fresh = false;

  beforeUpdate(() => {
    console.log(["before", fromColorHue, bgColorHue]);

    if (fromColorHue != bgColorHue) {
      fresh = true;
    }

    fromGradientString = toGradientString;

    toGradientString = getGradientString(
      getNewRandomHSLColor(bgColorHue),
      getNewRandomHSLColor(bgColorHue + 100)
    );
    fromColorHue = bgColorHue;
  });

  afterUpdate(() => {
    fresh = false;
    console.log(["after", fromColorHue, bgColorHue]);
  });

  function getNewRandomHSLColor(hue: number) {
    return `hsl(${Math.floor(hue)}, 80%, 60%)`;
  }

  function getGradientString(colorA: string, colorB: string) {
    return `background: linear-gradient(${Math.floor(
      Math.random() * 360
    )}deg, ${colorA}, ${colorB});`;
  }

  let fromGradientString = getGradientString(
    getNewRandomHSLColor(fromColorHue),
    getNewRandomHSLColor(fromColorHue + 100)
  );

  let toGradientString = getGradientString(
    getNewRandomHSLColor(bgColorHue),
    getNewRandomHSLColor(bgColorHue + 100)
  );
</script>

<div class="container">
  <div class="to" style={toGradientString} />
  {#if fresh}
    <div
      class="from"
      style={fromGradientString}
      out:fade={{ duration: 2000 }}
    />
  {/if}
</div>

<style>
  .container,
  .from,
  .to {
    width: 100%;
    height: 100%;
  }

  .container {
    position: absolute;
    z-index: -1;
  }

  .from {
    position: absolute;
  }

  .to {
    position: absolute;
  }
</style>
