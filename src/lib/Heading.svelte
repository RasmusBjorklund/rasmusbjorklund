<script>
  import { onMount } from 'svelte';
  const text = 'hello there!';

  onMount(() => {
    let i = 0;

    function typeWriter() {
      if (i < text.length) {
        document.getElementById('heading').innerHTML += text.charAt(i);
        i++;
        setTimeout(typeWriter, 200);
      }
    }
    typeWriter();
  });
</script>

<h1 id="heading">
  <span class="sr-only">{text}</span>
</h1>
<span class="blinker"></span>

<style lang="scss">
  .blinker {
    display: inline-block;
    width: 2px;
    height: 50px;
    margin-bottom: -4px;
    background-color: var(--color-secondary);
    margin-left: 2px;
    animation: blink 0.3s linear infinite alternate;
  }

  @keyframes blink {
    0% {
      opacity: 1;
    }
    40% {
      opacity: 1;
    }
    60% {
      opacity: 0;
    }
    100% {
      opacity: 0;
    }
  }
</style>
