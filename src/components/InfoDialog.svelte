<script lang="ts">
  import X from "@lucide/svelte/icons/x";

  import preview from "../assets/preview.webp";
</script>

<dialog
  id="info-dialog"
  class="fixed inset-0 m-0 p-5 bg-white w-full sm:w-125 h-screen max-h-none max-w-none shadow-xl backdrop:bg-black/33 backdrop:backdrop-blur-[2px]"
>
  <div class="flex justify-end">
    <button
      class="cursor-pointer text-gray-400 hover:text-gray-600"
      commandfor="info-dialog"
      command="close"><X /></button
    >
  </div>

  <h1 class="text-4xl">Year in Pixels</h1>
  <img alt="A preview of the app" src={preview} />
  <h2 class="text-2xl">What is a Year in Pixels?</h2>
  <p>
    A Year in Pixels is a beautiful way to visualize your emotions (or anything
    else you want to track) in a colorful grid. It lets you condense an entire
    day into a single pixel. By the end of the year you get a vibrant grid
    summarizing your entire year.
  </p>
  <br />
  <p>
    This Year in Pixels tracker is online, meaning it's easier to start doing
    and easier to keep up to date. You can just open the website from your
    phone/computer and color in a day.
  </p>
</dialog>
