<script>
  import Nav from './lib/Nav.svelte';
  import Heading from './lib/Heading.svelte';
  import Card from './lib/Card.svelte';
  import { development, programs, jobs } from './items.json';

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
  <section id="hello" style="flex-direction: row;">
    <Heading />
  </section>
  <section id="about">
    <h1>about</h1>
    <p>
      Korv Stroganoff på falukorv är en klassiker i det svenska vardagsköket -
      smakar lika bra i matlådan dagen efter. Här är ett recept från Vår kokbok.
      Tips! Prova även att göra grytan på frukostkorv eller grillkorv
      förvariation.
    </p>
  </section>
  <section id="experience">
    <h1>experience</h1>
    <div class="grid">
      <Card title="Development" items={development} />
      <Card title="Programs" items={programs} />
      <Card title="Jobs" items={jobs} />
    </div>
  </section>
  <section id="contact">
    <h1>contact</h1>
  </section>
</main>

<style lang="scss">
  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-height: 96vh;
    padding: 2vh 0;

    &:nth-child(odd) {
      background-color: var(--color-1);
    }

    &:nth-child(even) {
      background-color: var(--color-4);
    }
  }
</style>
