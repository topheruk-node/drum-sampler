<script lang="ts">
    import { z } from "zod";

    let div: HTMLDivElement;

    const Sample = z.object({
        name: z.string(),
        path: z.string(),
    });

    type Sample = z.infer<typeof Sample>;

    function onInput(e: Event) {
        for (const file of (e.target as HTMLInputElement).files!) {
            const { name, path } = Sample.parse({
                name: file.name,
                path: URL.createObjectURL(file),
            });

            // create audio tag
            const audio = document.createElement("audio");
            audio.src = path;
            audio.controls = true;
            div.appendChild(audio);
        }
    }
</script>

<div bind:this={div} />

<input
    type="file"
    on:input|preventDefault={onInput}
    webkitdirectory
    multiple
    accept="audio/*"
/>
