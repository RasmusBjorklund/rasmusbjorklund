<script>
  import { BrightnessHigh, MoonStars } from 'svelte-bootstrap-icons';
  import { onMount } from 'svelte';

  const currentHour = new Date().getHours();

  let mode = currentHour > 6 && currentHour < 12 ? 'light' : 'dark';
  let mounted = false;
  let checked = mode === 'dark' ? true : false;

  onMount(() => {
    document.body.classList.add(mode);
    mounted = true;
  });

  function handleClick() {
    if (document.body.classList.contains('light')) {
      document.body.classList.add('dark');
      document.body.classList.remove('light');
      mode = 'dark';
    } else {
      document.body.classList.add('light');
      document.body.classList.remove('dark');
      mode = 'light';
    }

    checked = !checked;
  }
</script>

{#if mounted}
  <div class="slider">
    <button
      role="switch"
      aria-checked={checked}
      aria-labelledby={`switch-mode`}
      on:click={handleClick}
      style={mode === 'light' ? '--right-margin: 42px' : '--right-margin: 32px'}
    >
      <BrightnessHigh
        width={20}
        height={20}
        style={mode === 'light'
          ? 'color: var(--color-secondary)'
          : 'color: var(--color-primary)'}
      />
      <MoonStars
        width={16}
        height={16}
        style={mode === 'light'
          ? 'color: var(--color-primary)'
          : 'color: var(--color-secondary)'}
      />
    </button>
  </div>
{/if}

<style lang="scss">
  .slider {
    display: flex;
    align-items: center;
    top: 20px;
    right: 20px;
    position: fixed;
    z-index: 1;
  }

  button {
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: 80px;
    height: 40px;
    padding: 0;
    border-radius: 25px;
    background: var(--color-secondary);

    &:focus {
      outline: none;
    }
  }

  button::after {
    content: '';
    position: absolute;
    width: 34px;
    height: 34px;
    background: var(--color-primary);
    right: var(--right-margin);
    transition: all 0.2s ease-out;
    border-radius: 100%;
  }

  button[aria-checked='true']::after {
    transform: translateX(28px);
    transition: all 0.2s ease-out;
  }

  :global(button svg) {
    z-index: 999;
  }
</style>
