<script>
  import Battery from "./lib/Battery.svelte";
  import BatteryFill from "./lib/BatteryFill.svelte";
  import Man from "./lib/Man.svelte";
  import Section1 from "./lib/sections/Section1.svelte";
  import Section2 from "./lib/sections/Section2.svelte";
  import Section3 from "./lib/sections/Section3.svelte";
  import Section4 from "./lib/sections/Section4.svelte";
  import Section5 from "./lib/sections/Section5.svelte";
  import Section6 from "./lib/sections/Section6.svelte";
  import Section7 from "./lib/sections/Section7.svelte";

  const sections = [
    {
      id: "section1",
      Content: Section1,
    },
    {
      id: "section2",
      Content: Section2,
    },
    {
      id: "section3",
      title: "",
      Content: Section3,
    },
    {
      id: "section4",
      Content: Section4,
    },
    {
      id: "section5",
      Content: Section5,
    },
    {
      id: "section6",
      Content: Section6,
    },
    {
      id: "section7",
      Content: Section7,
    },
  ];

  let y = 0;
  let screenHeight = 0;

  $: progress = Math.floor((y / screenHeight) * 2 * 100);
</script>

<svelte:window bind:scrollY={y} />

<main class="relative flex justify-end" bind:clientHeight={screenHeight}>
  <div class="fixed inset-0 flex h-full w-1/3 items-center justify-center">
    <div id="man" class="relative z-40">
      <Battery class="absolute top-0 h-full w-full" />
      <BatteryFill class="absolute top-0 h-full w-full" {progress} />
      <Man class="wiggle relative top-0  h-full w-full" />
    </div>
  </div>

  <div
    class="pointer-events-none fixed top-0 z-10 box-border h-1/3 w-2/3 bg-gradient-to-t from-transparent to-emerald-500"
  />
  <div
    class="pointer-events-none fixed bottom-0 z-10 box-border h-1/3 w-2/3 bg-gradient-to-b from-transparent to-emerald-500"
  />
  <div class="relative flex w-2/3 flex-col items-center bg-emerald-500">
    <div class="h-[30vh]" />
    {#each sections as { Content, id }}
      <section
        class="mt-8 flex min-h-[50vh] cursor-default snap-center flex-col items-center justify-center rounded-lg p-4 text-center text-white outline-black [&_p]:max-w-[40rem]"
        {id}
      >
        <svelte:component this={Content} />
      </section>
    {/each}
    <div class="h-[30vh]" />
  </div>
</main>

<style>
  @keyframes wiggle {
    0% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-10px);
    }
    100% {
      transform: translateY(0px);
    }
  }

  #man {
    animation: wiggle 2s infinite;
  }
</style>
