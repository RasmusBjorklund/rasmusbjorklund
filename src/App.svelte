<script>
  import Card from './lib/Card.svelte';
  import Nav from './lib/Nav.svelte';

  const sections = [
    { name: 'hello', id: 'hello' },
    { name: 'about', id: 'about' },
    { name: 'experience', id: 'experience' },
    { name: 'contact', id: 'contact' },
  ];
</script>

<aside>
  <Nav {sections} />
</aside>

<main>
  <section id="hello" style="background-color: var(--color-1);">
    <h1>hello</h1>
  </section>
  <section id="about" style="background-color: var(--color-4);">
    <h1>about</h1>
    <p style="max-width: 400px; text-align: center;">
      Korv Stroganoff på falukorv är en klassiker i det svenska vardagsköket -
      smakar lika bra i matlådan dagen efter. Här är ett recept från Vår kokbok.
      Tips! Prova även att göra grytan på frukostkorv eller grillkorv
      förvariation.
    </p>
  </section>
  <section id="experience" style="background-color: var(--color-1);">
    <h1>experience</h1>
    <div class="grid">
      <Card title="Dev" />
      <Card title="Tools" />
      <Card title="Jobs" />
    </div>
  </section>
  <section id="contact" style="background-color: var(--color-4);">
    <h1>contact</h1>
  </section>
</main>

<style lang="scss">
  .grid {
    display: flex;
    gap: 25px;
    flex-wrap: wrap;
    justify-content: center;
  }
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
</style>
