<script lang="ts">
  // import Counter from './lib/Counter.svelte'
  import Todolist from './lib/Todolist.svelte'
  import svelteLogo from './assets/svelte.svg'
  // import viteLogo from '/vite.svg'
</script>

<main>
  <div>
    <!-- <a href="/" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a> -->
    <a href="/" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <!-- <h1>Vite + Svelte</h1> -->

  <!-- <div class="card">
    <Counter />
  </div> -->

  <!-- <p class="read-the-docs">
    Click on the Vite and Svelte logos to learn more
  </p> -->

  <Todolist />
</main>

<style lang="less">
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;

    &:hover {
      filter: drop-shadow(0 0 2em #646cffaa);
    }

    &.svelte:hover {
      filter: drop-shadow(0 0 2em #ff3e00aa);
    }
  }
  // .read-the-docs {
  //   color: #888;
  // }
</style>
