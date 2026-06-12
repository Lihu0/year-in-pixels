<script lang="ts">
  import X from "@lucide/svelte/icons/x";

  import color_dialog from "../assets/color_dialog.png";
  import color_palette from "../assets/color_palette.webp";
  import import_and_export from "../assets/import_and_export.webp";
  import preview from "../assets/preview.webp";
  import year_selection from "../assets/year_selection.webp";
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

  <article class="space-y-6">
    <h1 class="font-semibold text-4xl">Year in Pixels</h1>
    <img alt="A preview of the app" src={preview} />

    <section class="space-y-4">
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

    <section class="space-y-4">
      <h2 class="font-semibold text-2xl">Features</h2>

      <section class="space-y-2">
        <h3 class="font-semibold text-xl">Add/Edit Colors</h3>
        <img
          alt="Customize Colors"
          src={color_palette}
          class="w-1/2 sm:w-1/3"
        />
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
          Select a color to open a color picker, or select the label to edit it.
        </p>
      </section>

      <section class="space-y-2">
        <h3 class="font-semibold text-xl">Year Selection</h3>
        <img alt="Select a Year" src={year_selection} class="w-1/3 sm:w-1/4" />
        <p>
          Select the year drop-down to open the list, then choose a different
          year to update your selection. The website will check your filled-in
          days and display a list of available years, including the current year
          if it is not already included.
        </p>
      </section>

      <section class="space-y-2">
        <h3 class="font-semibold text-xl">Fill In Pixels</h3>
        <img
          alt="Change the Color of a Day"
          src={color_dialog}
          class="w-1/2 sm:w-1/3"
        />
        <p>
          Click on any day in your grid and select the color that best
          represents your activity or mood for that day. You can clear a day by
          clicking the white button with a red diagonal slash.
        </p>
      </section>

      <section class="space-y-2">
        <h3 class="font-semibold text-xl">Import and Export</h3>
        <img
          alt="Export as a PNG or JSON, and import JSON"
          src={import_and_export}
          class="w-1/3 sm:w-1/4"
        />
        <p>
          You can download your Year in Pixels as a beautiful image to share or
          keep as a visual record. You can also import and export it as a JSON
          file.
        </p>
      </section>

      <section class="space-y-2">
        <h3 class="font-semibold text-xl">Autosave</h3>
        <p>
          Your data is automatically saved to your browser's
          <code>localStorage</code> and protected with the
          <code>navigator.storage.persist</code> API, so you can build your Year in
          Pixels over time without worrying about losing your progress.
        </p>
      </section>
    </section>

    <section class="space-y-4">
      <h2 class="font-semibold text-2xl">Why Use a Year in Pixels Tracker?</h2>
      <p>
        A Year in Pixels offers unique advantages for personal tracking and
        reflection:
      </p>
      <ul class="list-disc pl-6">
        <li>
          Visual trends in your Year in Pixels grid tend to reveal trends.
        </li>
        <li>
          You can easily identify periods of joy, stress, or stagnation. As you
          look at your Year in Pixels, you might notice your positive mood in
          summer or a period of unhappiness.
        </li>
        <li>
          You can track anything you choose to track in a Year in Pixels, from
          your mood to tracking your health.
        </li>
        <li>
          A Year in Pixels takes minimal time investment—just seconds each day
          to update it.
        </li>
        <li>
          You get a colorful grid at the end of the year that summarizes your
          whole year.
        </li>
      </ul>
    </section>

    <section class="space-y-4">
      <h2 class="font-semibold text-2xl">Conclusion</h2>
      <p>
        Using a Year In Pixels is just like painting yourself in the coming year
        through the use of colored pixels every day. You get the chance to
        choose the color you want to put every day according to your activities
        and moods and place it in the little box provided in your canvas. At the
        end of the year, you get a nice picture which is beautiful and easy to
        analyze.
      </p>
    </section>
  </article>
</dialog>
