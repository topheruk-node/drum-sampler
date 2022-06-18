<script lang="ts">
    import "@topheruk/audio";
    import { z } from "zod";

    const Data = z.object({
        tracks: z.array(
            z.object({ name: z.string().optional(), src: z.string() })
        ),
        inserts: z.array(
            z.object({
                type: z
                    .enum(["gain", "pan", "lowpass", "highpass"])
                    .default("gain"),
                value: z.number(),
                step: z.number(),
                min: z.number(),
                max: z.number(),
            })
        ),
    });
    type Data = z.infer<typeof Data>;

    const data: Data = {
        tracks: [
            { name: "kick", src: "/audio/kicks/kick02.wav" },
            { name: "clap", src: "/audio/clap01.wav" },
            { name: "snare", src: "/audio/snares/snare01.wav" },
            { name: "hi hat", src: "/audio/percs/perc02.wav" },
        ],
        inserts: [
            { type: "gain", value: 75, step: 1, min: 0, max: 100 },
            { type: "pan", value: 0, step: 1, min: -100, max: 100 },
            { type: "highpass", value: 40, step: 10, min: 0, max: 24000 },
            // { type: "highpass", value: 40, step: 10, min: 0, max: 24000 },
        ],
    };
</script>

<drum-sampler bus no-cache>
    {#each data.inserts as { type, value, step, min, max }}
        <effect-insert slot="insert" {type} {value} {step} {min} {max} />
    {/each}
    {#each data.tracks as { name, src }}
        <audio-track slot="track" {name} {src} />
    {/each}
</drum-sampler>
