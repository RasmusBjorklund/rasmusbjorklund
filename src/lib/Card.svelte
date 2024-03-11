<script>
  export let title;
  export let items;
</script>

<div>
  <h2>{title}</h2>
  <ul>
    {#each items as item}
      <li>{item}</li>
    {/each}
  </ul>
</div>

<style lang="scss">
  div {
    border-radius: 6px;
    padding: 50px;
    max-width: 240px;
    background-color: white;
    color: black;
    box-shadow:
      rgba(0, 0, 0, 0.09) 0px 2px 1px,
      rgba(0, 0, 0, 0.09) 0px 4px 2px,
      rgba(0, 0, 0, 0.09) 0px 8px 4px,
      rgba(0, 0, 0, 0.09) 0px 16px 8px,
      rgba(0, 0, 0, 0.09) 0px 32px 16px;
  }

  h2 {
    font-size: 30px;
    border-bottom: 3px solid;
    margin: 5px 0;
    padding: 5px 0;
    border-bottom-style: dotted;
  }

  ul {
    padding-left: 22px;
    list-style: circle;
  }

  li {
    word-break: normal;
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
