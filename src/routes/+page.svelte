<script>
  import { onMount } from "svelte";
  import gsap from "gsap";

  let boxesContainer, tl = gsap.timeline({ paused: true });

  const toggleTimeline = () => {
    tl.reversed(!tl.reversed());
  };

  onMount(() => {
    const ctx = gsap.context((self) => {
      const boxes = self.selector(".box");
      tl = gsap.timeline({ paused: true });
      tl.to(boxes[0], { x: 120, rotation: 360 })
        .to(boxes[1], { x: -120, rotation: -360 }, "<")
        .to(boxes[2], { y: -166 })
        .reverse();
    }, boxesContainer); // <- Scope!

    return () => ctx.revert(); // <- Cleanup!
  });
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<main>
  <section class="boxes-container" bind:this={boxesContainer}>
    <h1>Use the button to toggle a Timeline</h1>
    <div>
      <button on:click={toggleTimeline}>Toggle Timeline</button>
    </div>
    <div class="box">Box 1</div>
    <div class="box">Box 2</div>
    <div class="box">Box 3</div>
  </section>
</main>
