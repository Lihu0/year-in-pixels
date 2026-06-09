<script lang="ts">
  import { entries, palette } from "../lib/state.svelte";

  let {
    selectedCell,
    closeDialog,
  }: { selectedCell: string | null; closeDialog: () => void } = $props();

  let dialog: HTMLDialogElement;

  $effect(() => {
    if (!dialog) return;

    if (selectedCell !== null) {
      if (!dialog.open) dialog.showModal();
    } else {
      if (dialog.open) dialog.close();
    }
  });
</script>

<dialog
  class="border-2 border-black bg-white backdrop:bg-transparent outline-none
        fixed [position-anchor:--selected-cell] left-[calc(anchor(left)+5px)] top-[calc(anchor(top)+5px)]"
  onclick={(e) => {
    if (e.target === e.currentTarget) closeDialog();
  }}
  bind:this={dialog}
>
  <div
    class="grid select-none grid-cols-1 min-[350px]:grid-cols-2 sm:grid-cols-3 gap-1 p-2"
  >
    {#each palette as paletteValue, i}
      <button
        type="button"
        class="size-8 cursor-pointer border-2 border-black transition-opacity hover:opacity-75 outline-none"
        style:background-color={paletteValue.color}
        title={paletteValue.label}
        onclick={() => {
          entries[selectedCell!] = i;
          closeDialog();
        }}
      ></button>
    {/each}

    <button
      type="button"
      class="relative size-8 cursor-pointer border-2 border-black transition-opacity hover:opacity-75 outline-none"
      style:background-color="transparent"
      title="Clear"
      onclick={() => {
        delete entries[selectedCell!];
        closeDialog();
      }}
    >
      <svg class="absolute inset-0 size-full">
        <line x1="0" y1="0" x2="100%" y2="100%" stroke="red" stroke-width="2"
        ></line>
      </svg>
    </button>
  </div>
</dialog>
