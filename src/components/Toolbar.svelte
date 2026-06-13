<script lang="ts">
  import { toPng } from "html-to-image";

  import FileDown from "@lucide/svelte/icons/file-down";
  import FileUp from "@lucide/svelte/icons/file-up";
  import FolderGit2 from "@lucide/svelte/icons/folder-git-2";
  import ImageDown from "@lucide/svelte/icons/image-down";
  import Info from "@lucide/svelte/icons/info";

  import InfoDialog from "./InfoDialog.svelte";

  import { entries, palette } from "../lib/state.svelte";

  async function downloadImage() {
    await document.fonts.ready;

    const node = document.querySelector("main") as HTMLElement;
    if (!node) {
      alert("Could not find the main element to export.");
      return;
    }

    const dataUrl = await toPng(node, {
      cacheBust: true,
      pixelRatio: 1,
      filter: (el) => {
        if (!(el instanceof Element)) return true;
        if (el.hasAttribute("data-no-export")) return false;
        return true;
      },
    });

    const a = document.createElement("a");
    a.href = dataUrl;
    a.download = "year-in-pixels.png";
    a.click();
  }

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
    class="cursor-pointer"
    title="Information"
    aria-label="Information"
    command="show-modal"
    commandfor="info-dialog"
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
    class="cursor-pointer"
    title="Download as image"
    aria-label="Download as image"
    onclick={downloadImage}
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

<InfoDialog />
