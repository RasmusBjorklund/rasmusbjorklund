<script>
  import Nav from './lib/Nav.svelte';
  import Heading from './lib/Heading.svelte';
  import Card from './lib/Card.svelte';
  import { development, programs, jobs } from './items.json';
  import { onMount } from 'svelte';
  import { List } from 'svelte-bootstrap-icons';
  import ToggleMode from './lib/ToggleMode.svelte';

  let isOpen = false;
  $: screenWidth = 0;

  const sections = [
    { name: 'hello', id: 'hello' },
    { name: 'about', id: 'about' },
    { name: 'experience', id: 'experience' },
    { name: 'contact', id: 'contact' },
  ];

  const handleResize = () => {
    screenWidth = window.innerWidth;
  };

  onMount(() => {
    handleResize();
    window.addEventListener('resize', handleResize);
  });
</script>

<ToggleMode />

<aside class:mobile={screenWidth < 800}>
  {#if screenWidth < 800}
    <button on:click={() => (isOpen = !isOpen)}>
      <List color="black" />
    </button>
    <div>
      <Nav {sections} mobile={true} bind:isOpen />
    </div>
  {:else}
    <Nav {sections} />
  {/if}
</aside>

<main>
  <section id="hello" style="flex-direction: row;">
    <Heading />
  </section>
  <section id="about">
    <h2>about</h2>
    <p>
      Got a passion for web developing, user experience and good looking
      websites. Love Svelte, music & beer. An excellent combination. But, not in
      the long run. Have worked as a web developer, project manager & web
      designer for some years now. Pretty much got the basics figured out.
    </p>
  </section>
  <section id="experience">
    <h2>experience</h2>
    <div class="grid">
      <Card title="Development" {...development} />
      <Card title="Programs" {...programs} />
      <Card title="Jobs" {...jobs} />
    </div>
  </section>
  <section id="contact">
    <h2>contact</h2>
    <div class="grid">
      <a href="https://www.linkedin.com/in/rasmus-bj%C3%B6rklund-6b985a179/"
        >https://linkedin.com/rasmus-björklund</a
      >
    </div>
  </section>
</main>

<style lang="scss">
  aside {
    &.mobile {
      position: fixed;
      top: 0;
      z-index: 3;
      width: 100%;

      div {
        margin-top: 49px;
        position: relative;
      }
      button {
        position: fixed;
        top: 0;
        left: 0;
        z-index: 2;
        width: 100%;
        background-color: var(--color-secondary);
        border-radius: 0;
      }
    }
  }
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 96vh;
    padding: 2vh 0;
    background-color: var(--color-primary);

    // &:nth-child(odd) {
    //   background-color: var(--color-white);
    // }

    // &:nth-child(even) {
    //   background-color: var(--color-magenta);
    // }
  }
</style>
