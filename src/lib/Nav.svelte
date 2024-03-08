<script>
  import { onMount } from 'svelte';
  export let sections;

  let activeSection = window.location.hash.substring(1) || sections[0].id;

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          const id = entry.target.getAttribute('id');
          const link = document.querySelector(`nav li[id="${id}"]`);
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
  });

  // $: {
  //   window.addEventListener('hashchange', () =>
  //     console.log(window.location.hash)
  //   );
  // }
</script>

<nav>
  <ul>
    {#each sections as { name, id }}
      <li {id} class:active={activeSection === id}>
        {name}
      </li>
    {/each}
  </ul>
</nav>

<style>
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

  li {
    position: relative;
    font-size: 24px;
    font-weight: 700;
    padding: 5px;
    margin: 10px;
    display: block;
    color: var(--color-3);
    width: fit-content;
    transition: 0.2s;
  }

  li.active {
    color: var(--color-2);
    text-decoration: line-through;
  }

  li.active::after {
    position: absolute;
    right: -15px;
    top: 5px;
    display: block;
    height: 10px;
    width: 10px;
    color: rgb(224, 53, 53);
    content: '•';
    /* content: '';
    content: '•'; */
  }
</style>
