<script lang="ts">
  import FileDown from "@lucide/svelte/icons/file-down";
  import FileUp from "@lucide/svelte/icons/file-up";
  import FolderGit2 from "@lucide/svelte/icons/folder-git-2";
  import ImageDown from "@lucide/svelte/icons/image-down";
  import Info from "@lucide/svelte/icons/info";
</script>

<div class="flex w-full justify-end gap-2">
  <button
    class="cursor-not-allowed opacity-50"
    disabled
    title="Information (WIP)"
    aria-label="Information (WIP)"
  >
    <Info />
  </button>
  <a
    title="See source code on GitHub"
    aria-label="See source code on GitHub"
    href="https://github.com/Lihu0/YearInPixels"
    target="_blank"
    rel="noopener noreferrer"
  >
    <FolderGit2 />
  </a>
  <button
    class="cursor-not-allowed opacity-50"
    disabled
    title="Download as image (WIP)"
    aria-label="Download as image (WIP)"
  >
    <ImageDown />
  </button>
  <button
    class="cursor-not-allowed opacity-50"
    disabled
    title="Import JSON (WIP)"
    aria-label="Import JSON (WIP)"
  >
    <FileUp />
  </button>
  <button
    class="cursor-not-allowed opacity-50"
    disabled
    title="Export JSON (WIP)"
    aria-label="Export JSON (WIP)"
  >
    <FileDown />
  </button>
</div>
