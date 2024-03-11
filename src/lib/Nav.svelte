<script>
  import { onMount, onDestroy } from 'svelte';

  export let sections;

  let activeSection = window.location.hash.substring(1) || sections[0].id;
  let observer;

  const observeSections = () => {
    observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          const id = entry.target.getAttribute('id');
          const link = document.querySelector(`nav li a[href="#${id}"]`);
          if (entry.isIntersecting && entry.intersectionRatio >= 0) {
            window.location.hash = id;
            link.classList.add('active');
          } else {
            link.classList.remove('active');
          }
        });
      },
      { rootMargin: '-50% 0px' }
    );

    document.querySelectorAll('section[id]').forEach((section) => {
      observer.observe(section);
    });
  };

  onMount(() => {
    observeSections();
  });

  // Function that disconnects the observer and sets a timeout before re-attaching the observer
  const resetObserver = () => {
    if (observer) {
      observer.disconnect();
      setTimeout(observeSections, 700);
    }
  };

  // The observer is disconnected in the onDestroy lifecycle hook to clean up when the component is destroyed.
  onDestroy(() => {
    if (observer) {
      observer.disconnect();
    }
  });

  // Function is called when an anchor link is clicked, which triggers the reset of the observer.
  const anchorClickHandler = () => {
    resetObserver();
  };
</script>

<nav>
  <ul>
    {#each sections as { name, id }}
      <li>
        <a
          href={`#${id}`}
          class:active={activeSection === id}
          on:click={anchorClickHandler}
        >
          {name}
        </a>
      </li>
    {/each}
  </ul>
</nav>

<style lang="scss">
  nav {
    position: fixed;
    top: 0%;
    left: 20px;
    z-index: 2;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  a {
    position: relative;
    font-size: 24px;
    font-weight: 700;
    padding: 5px;
    margin: 10px;
    text-decoration: none;
    display: block;
    color: var(--color-3);
    width: fit-content;
    transition: 0.2s;

    &.active {
      color: var(--color-2);
      text-decoration: line-through;

      &::after {
        position: absolute;
        right: -15px;
        top: 5px;
        display: block;
        height: 12px;
        width: 12px;
        color: var(--color-red);
        content: '•';
      }
    }
  }
</style>
