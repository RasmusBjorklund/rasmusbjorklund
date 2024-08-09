<script>
  import Nav from './lib/Nav.svelte';
  import Heading from './lib/Heading.svelte';
  import Card from './lib/Card.svelte';
  import { development, programs, jobs } from './items.json';
  import { onMount } from 'svelte';
  import {
    List,
    ArrowDownLeft,
    LightningFill,
    Github,
    Linkedin,
  } from 'svelte-bootstrap-icons';
  import ToggleMode from './lib/ToggleMode.svelte';
  import me from './assets/me.png';

  let isOpen = false;
  // let location;
  $: screenWidth = 0;

  const sections = [
    { name: 'hello', id: 'hello' },
    { name: 'who am i', id: 'about' },
    { name: 'experience', id: 'experience' },
    { name: 'contact', id: 'contact' },
  ];

  const handleResize = () => {
    screenWidth = window.innerWidth;
  };

  onMount(() => {
    handleResize();
    window.addEventListener('resize', handleResize);
    // location = Intl.DateTimeFormat().resolvedOptions().timeZone;
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
    <!-- <span class="sr-only">{location}</span> -->
    <Heading />
  </section>
  <section id="about">
    <LightningFill width={38} height={38} />
    <h2>who am i</h2>
    <img src={me} class="profile" alt="me the idiot" />
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
      <Card title="Jobs" {...jobs} />
      <Card title="Programs" {...programs} />
      <Card title="Development" {...development} />
    </div>
  </section>
  <section id="contact">
    <h2>reach out <ArrowDownLeft width={32} height={32} /></h2>
    <!-- <div class="circle">
      <img src={nalleLogo} class="logo svelte" alt="Svelte Logo" />
    </div> -->
    <div class="grid flex-d-column">
      <button class="button-effect button-link">
        <a href="https://www.linkedin.com/in/rasmus-bj%C3%B6rklund-6b985a179/">
          LinkedIn
        </a>
        <Linkedin />
      </button>
      <button class="button-effect button-link">
        <a href="https://github.com/RasmusBjorklund"> Github </a>
        <Github />
      </button>
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

  .profile {
    width: 400px;
    height: 100%;
  }

  // .circle {
  //   display: flex;
  //   justify-content: center;
  //   border-radius: 50%;
  //   border: 2px solid;
  //   margin-bottom: 53px;
  //   overflow: hidden;
  //   height: 250px;
  //   width: 250px;
  // }
</style>
