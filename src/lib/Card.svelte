<script>
  export let title;
</script>

<div>
  <h2>{title}</h2>
  <ul>
    <li>Front-end development</li>
    <li>Amazon Web Services</li>
    <li>Svelte</li>
    <li>React</li>
  </ul>
</div>

<style lang="scss">
  div {
    border-radius: 6px;
    padding: 50px;
    background-color: white;
    color: black;
    box-shadow:
      rgba(0, 0, 0, 0.09) 0px 2px 1px,
      rgba(0, 0, 0, 0.09) 0px 4px 2px,
      rgba(0, 0, 0, 0.09) 0px 8px 4px,
      rgba(0, 0, 0, 0.09) 0px 16px 8px,
      rgba(0, 0, 0, 0.09) 0px 32px 16px;
  }

  ul {
    padding-left: 22px;
    list-style: circle;
  }

  h2 {
    font-size: 30px;
    border-bottom: 2px solid;
    margin: 5px 0;
    padding: 5px 0;
    border-bottom-style: dotted;
  }
</style>
