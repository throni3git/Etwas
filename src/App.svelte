<script lang="ts">
  import Background from "./Background.svelte";
  let rnd: number;
  function resetRnd() {
    rnd = Math.random() * 360;
  }
  resetRnd();
</script>

<main>
  <Background bgColorHue={rnd} />
  <h1>Etwas</h1>
  <p>Nimm dir Zeit und schreib etwas</p>
  <button on:click={resetRnd}>rnd</button>
</main>

<style>
  main {
    text-align: center;
    max-width: 240px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
  }

  h1,
  p {
    opacity: 0.2;
  }

  h1 {
    text-transform: uppercase;
    font-family: "Lora", serif;
    font-size: 6em;
    font-weight: 100;
  }

  p {
    font-size: 2em;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
