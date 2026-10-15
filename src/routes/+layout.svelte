<script lang="ts">
    import "./layout.css";
    import favicon from "../lib/assets/shortcuts.png";
    import type { LayoutProps } from "./$types";
    import Navbar from "../lib/components/Navbar.svelte";

    let { children }: LayoutProps = $props();

    import { onMount } from "svelte";

    onMount(async () => {
        const { registerSW } = await import("virtual:pwa-register");
        registerSW({ immediate: true });
    });
</script>

<svelte:head>
    <link rel="icon" href={favicon} />
</svelte:head>

{@render children()}

<Navbar />
