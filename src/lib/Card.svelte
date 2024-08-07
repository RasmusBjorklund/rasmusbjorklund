<script>
  import Modal from './Modal.svelte';

  export let title;
  export let items;
  export let description;

  let showModal = false;
</script>

<Modal bind:showModal>
  <h3 slot="header">
    {title}
  </h3>
  {#each description as { heading, text }}
    <h4>{heading}</h4>
    <p>{text}</p>
  {/each}
</Modal>

<div>
  <h3>{title}</h3>
  <ul>
    {#each items as item}
      <li>{@html item}</li>
    {/each}
  </ul>
  <button on:click={() => (showModal = true)}>
    <span class="sr-only">Read more about {title}</span>
  </button>
</div>

<style lang="scss">
  div {
    position: relative;
    border-radius: 12px;
    padding: 35px 50px;
    flex: 100%;
    background-color: var(--color-primary);
    color: var(--color-secondary);
    border: 2px solid var(--color-secondary);
    transition: all 0.2s ease-out;
    box-shadow: 4px 4px 0 #000;

    &:hover {
      box-shadow: 0 0 0 #000;
      transform: translate(4px, 4px);
    }
  }

  h3 {
    border-bottom: 3px solid;
    margin: 5px 0;
    padding: 5px 0;
    border-bottom-style: dotted;
  }

  p {
    margin: 16px 0 32px;
  }

  ul {
    padding-left: 22px;
    list-style: square;
  }

  li {
    word-break: normal;
  }

  button {
    position: absolute;
    height: 100%;
    width: 100%;
    top: 0;
    left: 0;
    right: 0;
    background-color: transparent;
    padding: 0;
    box-shadow: none;
    border: none;

    &:hover {
      transform: none;
    }
  }

  @media (width <=400px) {
    div {
      padding: 25px;
    }

    h3 {
      font-size: 24px;
    }
  }
</style>
