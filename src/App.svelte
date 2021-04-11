<main>
  <h1>Etwas</h1>
  <p>Nimm dir Zeit und schreib etwas</p>
</main>

<style>
  main {
    text-align: center;
    max-width: 240px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  h1,
  p {
    opacity: 0.3;
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
