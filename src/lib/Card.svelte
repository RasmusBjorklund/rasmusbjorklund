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
  <h2>{title}</h2>
  <ul>
    {#each items as item}
      <li>{item}</li>
    {/each}
  </ul>
  <button on:click={() => (showModal = true)}>
    <span class="sr-only">Read more</span>
  </button>
</div>

<style lang="scss">
  div {
    position: relative;
    border-radius: 12px;
    padding: 50px;
    max-width: 240px;
    background-color: var(--color-white);
    color: var(--color-black);
    transition: all 0.2s;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;

    &:hover {
      box-shadow:
        rgba(0, 0, 0, 0.09) 0px 2px 1px,
        rgba(0, 0, 0, 0.09) 0px 4px 2px,
        rgba(0, 0, 0, 0.09) 0px 8px 4px,
        rgba(0, 0, 0, 0.09) 0px 16px 8px,
        rgba(0, 0, 0, 0.09) 0px 32px 16px;
    }
  }

  h2 {
    font-size: 30px;
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
    list-style: circle;
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
  }

  @media (width <=400px) {
    div {
      padding: 25px;
    }

    h2 {
      font-size: 24px;
    }
  }
</style>
