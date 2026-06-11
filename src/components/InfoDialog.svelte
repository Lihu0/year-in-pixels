<script lang="ts">
  import X from "@lucide/svelte/icons/x";

  import colorPalette from "../assets/colorPalette.webp";
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

  <article class="space-y-2">
    <h1 class="font-semibold text-4xl">Year in Pixels</h1>
    <img alt="A preview of the app" src={preview} />

    <section>
      <h2 class="font-semibold text-2xl">What is a Year in Pixels?</h2>
      <p>
        A Year in Pixels is a beautiful way to visualize your emotions (or
        anything else you want to track) in a colorful grid. It lets you
        condense an entire day into a single pixel. By the end of the year, you
        get a vibrant grid summarizing your entire year.
      </p>
      <p>
        This Year in Pixels tracker is online, meaning it's easier to start
        doing and easier to keep up to date. You can just open the website from
        your phone/computer and color in a day.
      </p>
    </section>

    <section>
      <h2 class="font-semibold text-2xl">Features</h2>

      <section>
        <h3 class="font-semibold text-xl">Add/Edit Colors</h3>
        <img alt="Customize Colors" src={colorPalette} width="33%" />
        <p>
          Click on "Add color" to add a new color to your color palette. You can
          add as many colors as you want (though using too many colors might not
          be effective for tracking), each representing a different habit,
          emotion, or activity you want to track.
        </p>
        <p>
          Click on the remove button next to the color to remove it. Note that
          removing a color will clear <strong>all</strong> of its uses in your Year
          in Pixels.
        </p>
        <p>
          Click on a color to change it, and click on its label to change the
          label.
        </p>
      </section>
    </section>
  </article>
</dialog>
