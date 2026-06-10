<script lang="ts">
  import X from "@lucide/svelte/icons/x";
</script>

<dialog
  id="info-dialog"
  class="fixed inset-0 m-0 p-5 bg-white w-full sm:w-100 h-screen max-h-none max-w-none shadow-xl backdrop:bg-black/33 backdrop:backdrop-blur-[2px]"
>
  <div class="flex justify-end">
    <button
      class="cursor-pointer text-gray-400 hover:text-gray-600"
      commandfor="info-dialog"
      command="close"><X /></button
    >
  </div>

  <p>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Aperiam alias,
    natus quia suscipit odio, nisi laborum saepe rerum, repudiandae voluptatibus
    corporis autem dolor facere dignissimos.
  </p>
</dialog>
