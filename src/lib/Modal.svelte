<script>
  import { X } from 'svelte-bootstrap-icons';

  export let showModal;

  let dialog;

  $: if (dialog && showModal) {
    dialog.showModal();
    document.body.style.overflowY = 'hidden';
  } else {
    document.body.style.overflowY = '';
  }
</script>

<!-- svelte-ignore a11y-click-events-have-key-events a11y-no-noninteractive-element-interactions -->
<dialog
  bind:this={dialog}
  on:close={() => (showModal = false)}
  on:click|self={() => dialog.close()}
>
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div on:click|stopPropagation>
    <div class="modal-top">
      <slot name="header" />
      <button class="button-x" on:click={() => dialog.close()}>
        <X height={30} width={30} />
      </button>
    </div>
    <div class="modal-content">
      <slot />
    </div>
    <div class="modal-bottom">
      <button class="primary" on:click={() => dialog.close()}>Close</button>
    </div>
  </div>
</dialog>

<style lang="scss">
  dialog {
    max-width: 50em;
    border-radius: 12px;
    border: none;
    padding: 0;
    background-color: var(--color-primary);
    color: var(--color-secondary);
  }

  dialog::backdrop {
    background: rgba(0, 0, 0, 0.7);
  }

  .modal-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 30px;
    border-bottom: 2px solid var(--color-secondary);

    :global(h3) {
      margin: 0;
    }
  }

  .modal-content {
    padding: 0 30px 32px;

    :global(h4) {
      margin: 32px 0 10px;
    }

    :global(p) {
      margin: 0;
    }
  }

  .modal-bottom {
    padding: 15px 30px;
    border-top: 2px solid var(--color-secondary);
    text-align: end;
  }

  dialog[open] {
    animation: zoom 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
  }

  @keyframes zoom {
    from {
      transform: scale(0.95);
    }
    to {
      transform: scale(1);
    }
  }

  dialog[open]::backdrop {
    animation: fade 0.2s ease-out;
  }

  @keyframes fade {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  .button-x {
    display: block;
    padding: 5px 5px 1px;
    background-color: transparent;

    :global(svg) {
      fill: var(--color-secondary);
    }

    &:hover {
      box-shadow: none;
    }
  }
</style>
