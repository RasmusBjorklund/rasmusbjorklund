<script>
  import { BrightnessHigh, MoonStars } from 'svelte-bootstrap-icons';
  import { onMount } from 'svelte';

  const currentHour = new Date().getHours();

  let mode = currentHour > 6 && currentHour < 18 ? 'light' : 'dark';
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
    >
      <BrightnessHigh width={20} height={20} />
      <MoonStars width={16} height={16} />
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
    width: 60px;
    height: 30px;
    padding: 0;
    border-radius: 25px;
    background: var(--color-secondary);

    &:focus,
    &:hover {
      outline: none;
      border: none;
      box-shadow: none;
    }
  }

  button::after {
    content: '';
    position: absolute;
    width: 24px;
    height: 24px;
    background: var(--color-primary);
    right: 32px;
    transition: transform 0.3s;
    border-radius: 100%;
  }

  button[aria-checked='true']::after {
    transform: translateX(28px);
    transition: transform 0.3s;
  }
</style>
