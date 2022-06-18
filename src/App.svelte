<script lang="ts">
    import SamplePicker from "./lib/SamplePicker.svelte";
    import { createEffectNode, createBufferSource } from "@topheruk/audio";
    import DrumSampler from "./lib/DrumSampler.svelte";

    const gain = createEffectNode({ type: "gain", value: 0.5 });
    console.log(gain);
</script>

<main>
    <!-- <SamplePicker /> -->
    <DrumSampler />
</main>
