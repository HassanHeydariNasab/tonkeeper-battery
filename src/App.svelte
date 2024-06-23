<script>
  import { inview } from "svelte-inview";
  import Battery from "./lib/Battery.svelte";
  import BatteryFill from "./lib/BatteryFill.svelte";
  import Man from "./lib/Man.svelte";

  const sections = [
    {
      title: "",
      content: "",
    },
    {
      id: "section2",
      title: "Section 2",
      content: "This is the content of section 2",
    },
    {
      id: "section3",
      title: "Section 3",
      content: "This is the content of section 3",
    },
    {
      id: "section4",
      title: "Section 4",
      content: "This is the content of section 4",
    },
    {
      id: "section5",
      title: "Section 5",
      content: "This is the content of section 5",
    },
    {
      id: "section6",
      title: "Section 6",
      content: "This is the content of section 6",
    },
    {
      id: "section7",
      title: "Section 7",
      content: "This is the content of section 7",
    },
    {
      id: "section8",
      title: "",
      content: "",
    },
  ];

  let isInView = [];
  let y = 0;
  let screenHeight = 0;

  $: progress = Math.floor((y / screenHeight) * 100);
</script>

<svelte:window bind:scrollY={y} bind:innerHeight={screenHeight} />

<main class="relative flex justify-end">
  <div class="fixed inset-0 flex h-full w-1/3 items-center justify-center">
    <Battery class="absolute h-full w-full object-contain" />
    <BatteryFill
      class="absolute z-10 h-full w-full object-contain"
      {progress}
    />
    <Man class="z-20 h-full w-full object-contain" />
  </div>

  <div
    class="pointer-events-none fixed top-0 z-10 box-border h-1/3 w-2/3 bg-gradient-to-t from-transparent to-emerald-500"
  />
  <div
    class="pointer-events-none fixed bottom-0 z-10 box-border h-1/3 w-2/3 bg-gradient-to-b from-transparent to-emerald-500"
  />
  <div class="relative flex w-2/3 flex-col items-center bg-emerald-500">
    {#each sections as { title, content, id }, index}
      <section
        class="h-[30vh] snap-center scroll-mb-[40vh] scroll-mt-[40vh] rounded-lg p-4 text-center text-white outline-black"
        {id}
      >
        <a href={"#" + id}>
          <h2 class="text-4xl font-bold md:text-5xl">
            {title}
          </h2>
          <p>{content}</p>
        </a>
      </section>
    {/each}
  </div>
</main>

<style>
</style>
