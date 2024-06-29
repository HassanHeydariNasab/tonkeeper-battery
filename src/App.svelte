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
  import Ton from "./lib/Ton.svelte";
  import Tether from "./lib/Tether.svelte";

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
  ];

  let y = 0;
  let screenHeight = 0;

  $: progress = Math.floor((y / screenHeight) * 1.4 * 100);
</script>

<svelte:window bind:scrollY={y} />

<main class="relative flex justify-end" bind:clientHeight={screenHeight}>
  <div class="fixed inset-0 flex h-full w-1/3 items-center justify-center">
    <div id="man" class="relative z-40">
      <Battery class="absolute top-0 h-full w-full" />
      <BatteryFill class="absolute top-0 h-full w-full" {progress} />
      <Man class="wiggle relative top-0  h-full w-full" />
    </div>
    <!-- <Ton class="absolute left-[5%] blur-[2px]" style="top:{progress - 25}%" /> -->
    <!-- <Ton class="absolute right-[30%] z-30" style="top:{progress - 30}%" /> -->
    <!-- <Ton -->
    <!--   class="absolute right-[10%] z-50 scale-150 blur-[1px]" -->
    <!--   style="top:{progress * 2.5 - 200}%" -->
    <!-- /> -->
    <!-- <Ton -->
    <!--   class="absolute left-[20%] z-50 scale-[200%]" -->
    <!--   style="top:{progress * 3.5 - 60}%" -->
    <!-- /> -->
    <!-- <Ton -->
    <!--   class="absolute left-[0%] scale-150 blur-[2px]" -->
    <!--   style="top:{progress * 2.3 - 10}%" -->
    <!-- /> -->
    <!-- <Tether -->
    <!--   class="absolute left-[5%] z-50 scale-150 blur-[1px]" -->
    <!--   style="top:{progress * 2.5 - 150}%" -->
    <!-- /> -->
    <!-- <Tether -->
    <!--   class="absolute right-[30%] z-50 scale-150" -->
    <!--   style="top:{progress * 2.5 - 50}%" -->
    <!-- /> -->
    <!-- <Tether -->
    <!--   class="absolute right-[5%] z-10 scale-125 blur-[1px]" -->
    <!--   style="top:{progress * 2.25 - 10}%" -->
    <!-- /> -->
    <!-- <Tether -->
    <!--   class="absolute left-[15%] blur-[1px]" -->
    <!--   style="top:{progress - 20}%" -->
    <!-- /> -->
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
        class="mt-8 flex min-h-[35vh] cursor-default snap-center scroll-mb-[40vh] scroll-mt-[40vh] flex-col items-center rounded-lg p-8 text-center text-white outline-black [&_p]:max-w-[40rem]"
        {id}
      >
        <svelte:component this={Content} />
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
