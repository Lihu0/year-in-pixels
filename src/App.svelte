<script lang="ts">
  import CalendarGrid from "./components/CalendarGrid.svelte";
  import PaletteSelect from "./components/PaletteSelect.svelte";
  import Toolbar from "./components/Toolbar.svelte";
  import YearSelect from "./components/YearSelect.svelte";
</script>

<div
  class="flex min-h-screen w-screen items-center justify-center bg-stone-200 p-4"
>
  <div class="max-w-150 flex w-full flex-col items-center gap-2">
    <main
      class="text-graphite flex w-full flex-col bg-white p-4 shadow-[0_20px_40px_rgba(0,0,0,0.12)] outline outline-black/5 sm:p-8"
    >
      <h1
        class="font-handwritten-cursive mb-4 shrink-0 text-center text-4xl sm:text-6xl"
      >
        Year in Pixels
      </h1>
      <div
        class="font-handwritten-sans flex min-h-0 flex-1 flex-col items-center gap-4 sm:flex-row sm:justify-between"
      >
        <CalendarGrid />
        <div
          class="sm:w-fit flex w-full flex-col items-center justify-center gap-4"
        >
          <PaletteSelect />
          <YearSelect />
        </div>
      </div>
    </main>

    <Toolbar />
  </div>
</div>
