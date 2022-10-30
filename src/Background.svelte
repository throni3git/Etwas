<script lang="ts">
  import { afterUpdate, beforeUpdate } from "svelte";
  import { fade } from "svelte/transition";

  export let bgColorHue: number = 10;
  let fromColorHue = bgColorHue;
  let colorNeedsUpdate = false;

  function getNewRandomHSLColor(hue: number) {
    return `hsl(${Math.floor(hue)}, 80%, 50%)`;
  }

  function getGradientString(colorA: string, colorB: string) {
    const angle = Math.floor(Math.random() * 360);
    return `background: linear-gradient(${angle}deg, ${colorA}, ${colorB});`;
  }

  const HUE_DISTANCE = 60;

  let fromGradientString = getGradientString(
    getNewRandomHSLColor(fromColorHue),
    getNewRandomHSLColor(fromColorHue + HUE_DISTANCE)
  );

  let toGradientString = getGradientString(
    getNewRandomHSLColor(bgColorHue),
    getNewRandomHSLColor(bgColorHue + HUE_DISTANCE)
  );

  beforeUpdate(() => {
    console.log(["before", fromColorHue, bgColorHue]);

    if (fromColorHue != bgColorHue) {
      colorNeedsUpdate = true;
    }

    fromGradientString = toGradientString;

    toGradientString = getGradientString(
      getNewRandomHSLColor(bgColorHue),
      getNewRandomHSLColor(bgColorHue + HUE_DISTANCE)
    );
    fromColorHue = bgColorHue;
  });

  afterUpdate(() => {
    colorNeedsUpdate = false;
    console.log(["after", fromColorHue, bgColorHue]);
  });
</script>

<div class="container">
  <div class="to" style={toGradientString} />
  {#if colorNeedsUpdate}
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
