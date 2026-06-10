<script lang="ts">
  import FileDown from "@lucide/svelte/icons/file-down";
  import FileUp from "@lucide/svelte/icons/file-up";
  import FolderGit2 from "@lucide/svelte/icons/folder-git-2";
  import ImageDown from "@lucide/svelte/icons/image-down";
  import Info from "@lucide/svelte/icons/info";

  import { entries, palette } from "../lib/state.svelte";

  function importData() {
    const input = document.createElement("input");
    input.type = "file";
    input.accept = ".json";

    input.onchange = () => {
      const file = input.files?.[0];
      if (!file) return;

      const reader = new FileReader();
      reader.onload = (e) => {
        try {
          const content = JSON.parse(String(e.target?.result));

          if (!content.palette || !content.entries) {
            alert("Invalid file format. Expected keys: palette, entries");
            return;
          }

          palette.length = 0;
          palette.push(...content.palette); // Only mutate palette since it's an import

          Object.keys(entries).forEach((key) => delete entries[key]);
          Object.keys(content.entries).forEach(
            (key) => (entries[key] = content.entries[key]),
          ); // Only mutate entries since it's an import
        } catch (error) {
          alert(`Error reading file: ${error}`);
        }
      };

      reader.readAsText(file);
    };

    input.click();
  }

  function exportData() {
    const data = {
      palette: palette,
      entries: entries,
    };

    try {
      const blob = new Blob([JSON.stringify(data, null, 2)], {
        type: "application/json",
      });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");

      a.href = url;
      a.download = "year-in-pixels-export.json";
      a.click();
      URL.revokeObjectURL(url);
    } catch (error) {
      alert(`Error exporting data: ${error}`);
    }
  }
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
    class="cursor-pointer"
    title="Import JSON"
    aria-label="Import JSON"
    onclick={importData}
  >
    <FileUp />
  </button>
  <button
    class="cursor-pointer"
    title="Export JSON"
    aria-label="Export JSON"
    onclick={exportData}
  >
    <FileDown />
  </button>
</div>
