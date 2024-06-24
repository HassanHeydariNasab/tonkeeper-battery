<script>
  import { inview } from "svelte-inview";
  import Battery from "./lib/Battery.svelte";
  import BatteryFill from "./lib/BatteryFill.svelte";
  import Man from "./lib/Man.svelte";
  import Section1 from "./lib/sections/Section1.svelte";
  import Section2 from "./lib/sections/Section2.svelte";
  import Section3 from "./lib/sections/Section3.svelte";
  import Section4 from "./lib/sections/Section4.svelte";
  import Section5 from "./lib/sections/Section5.svelte";
  import Ton from "./lib/Ton.svelte";
  import Tether from "./lib/Tether.svelte";
  import Not from "./lib/Not.svelte";

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
  ];

  let isInView = [];
  let y = 0;
  let screenHeight = 0;

  $: progress = Math.floor((y / screenHeight) * 100);
</script>

<svelte:window bind:scrollY={y} bind:innerHeight={screenHeight} />

<main class="relative flex justify-end">
  <div class="fixed inset-0 flex h-full w-1/3 items-center justify-center">
    <div id="man" class="relative">
      <Battery class="absolute top-0 h-full w-full" />
      <BatteryFill class="absolute top-0 h-full w-full" {progress} />
      <Man class="wiggle relative top-0  h-full w-full" />
    </div>
    <Tether
      class="absolute left-[10%] blur-[2px]"
      style="top:{progress / 3}%"
    />
    <Not
      class="absolute left-[15%] blur-[1px]"
      style="top:{progress / 3.5 - 10}%"
    />
    <Tether
      class="absolute left-[30%] scale-125"
      style="top:{progress / 2 - 50}%"
    />
    <Ton class="absolute right-[10%] scale-150" style="top:{progress - 100}%" />
    <Ton
      class="absolute left-[20%] scale-[200%]"
      style="top:{progress * 1.5 - 100}%"
    />
  </div>

  <div
    class="pointer-events-none fixed top-0 z-10 box-border h-1/3 w-2/3 bg-gradient-to-t from-transparent to-emerald-500"
  />
  <div
    class="pointer-events-none fixed bottom-0 z-10 box-border h-1/3 w-2/3 bg-gradient-to-b from-transparent to-emerald-500"
  />
  <div class="relative flex w-2/3 flex-col items-center bg-emerald-500">
    <div class="h-[40vh]" />
    {#each sections as { Content, id }, index}
      <section
        class="min-h-[30vh] snap-center scroll-mb-[40vh] scroll-mt-[40vh] rounded-lg p-4 text-center text-white outline-black"
        {id}
      >
        <div class="flex cursor-default flex-col">
          <svelte:component this={Content} />
        </div>
      </section>
    {/each}
    <div class="h-[40vh]" />
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
