<script lang="ts">
    import ShortcutLogo from "#lib/assets/shortcuts.png";
    import { shortcuts } from "#lib/data/shortcuts.ts";
</script>

<svelte:head>
    <meta
        name="description"
        content="PassionTech shortcuts to your favorite apps and developer tools."
    />
    <meta name="theme-color" content="#000000" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
</svelte:head>

<main class="app">
    <section class="desktop-gate">
        <img
            class="PassionTech gate-logo"
            src={ShortcutLogo}
            alt="PassionTech logo"
        />

        <div class="install-info">
            <p>
                To use shortcuts on your phone, open this web app on your mobile
                browser and install it as a PWA. Use your browser's menu and
                choose "Add to Home Screen" or "Install app".
            </p>
        </div>
    </section>

    <!-- Mobile app -->
    <div class="app-content">
        <section class="hero">
            <img
                class="PassionTech"
                src={ShortcutLogo}
                alt="PassionTech logo"
            />

            <h1>
                <span class="brand">
                    <span>Shortcuts</span>
                </span>
            </h1>

            <p class="subtitle">Your favorite apps, one tap away.</p>
        </section>

        <section class="shortcut-section" aria-label="App shortcuts">
            <div class="shortcut-grid">
                {#each shortcuts as shortcut (shortcut.name)}
                    <a
                        class="shortcut-card"
                        href={shortcut.url}
                        target="_blank"
                        rel="noopener noreferrer"
                        aria-label={`Open ${shortcut.name}`}
                    >
                        <span class="shortcut-name">
                            {shortcut.name}
                        </span>
                    </a>
                {/each}
            </div>
        </section>
    </div>
</main>

<style>
    :global(*) {
        box-sizing: border-box;
    }

    :global(body) {
        margin: 0;
        background: #000;
        color: #fff;
        font-family: monospace;
    }

    .app {
        min-height: 100vh;
        padding: 1.25rem;
        background: #000;
        color: #fff;
    }

    .desktop-gate {
        display: none;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        min-height: 80vh;
        text-align: center;
    }

    .gate-logo {
        width: 200px;
        height: 200px;
    }

    .install-info {
        max-width: 500px;
        margin-top: 20px;
        padding: 1.5rem;
        border: 1px solid #333;
        border-radius: 16px;
        background: #0a0a0a;
        font-size: 1rem;
        line-height: 1.7;
    }

    .app-content {
        display: block;
        width: 100%;
        max-width: 560px;
        margin: 0 auto;
    }

    .hero {
        padding: 2rem 0;
        text-align: center;
    }

    .PassionTech {
        display: block;
        width: 80px;
        height: 80px;
        max-width: 80%;
        margin: 0 auto 1rem;
        object-fit: contain;
    }

    .brand {
        font-size: 2rem;
        font-weight: 800;
    }

    .brand span {
        padding: 0.2rem 0.5rem;
        border-radius: 10px;
        background: #e95420;
        color: #000;
    }

    .subtitle {
        margin-top: 1rem;
        color: #999;
        font-size: 0.85rem;
    }

    .shortcut-section {
        padding: 1rem 0 2rem;
    }

    .shortcut-grid {
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        gap: 12px;
    }

    .shortcut-card {
        position: relative;
        display: flex;
        min-width: 0;
        min-height: 112px;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 12px;
        padding: 1rem 0.5rem;
        border: 1px solid #262626;
        border-radius: 16px;
        background: #101010;
        color: #fff;
        text-decoration: none;
        -webkit-tap-highlight-color: transparent;
        transition:
            background 0.2s ease,
            border-color 0.2s ease,
            transform 0.2s ease;
    }

    .shortcut-card:active {
        transform: scale(0.96);
        background: #1b1b1b;
    }

    .shortcut-card:focus-visible {
        outline: 2px solid #e95420;
        outline-offset: 3px;
    }

    .shortcut-name {
        max-width: 100%;
        overflow-wrap: anywhere;
        font-size: 0.9rem;
        font-weight: 700;
        text-align: center;
    }

    /* Desktop browser */
    @media (min-width: 900px) {
        .app-content {
            display: none;
        }

        .desktop-gate {
            display: flex;
        }
    }

    /* Installed PWA: show the application */
    @media (display-mode: standalone) {
        .app-content {
            display: block;
        }

        .desktop-gate {
            display: none;
        }
    }

    /* Desktop standalone PWA */
    @media (min-width: 900px) and (display-mode: standalone) {
        :global(body) {
            background: #111;
        }

        .app {
            width: 100%;
            max-width: 420px;
            min-height: 100vh;
            margin: auto;
            border: 1px solid #222;
            border-radius: 20px;
        }
    }

    /* Small mobile screens */
    @media (max-width: 360px) {
        .app {
            padding: 0.75rem;
        }

        .shortcut-grid {
            grid-template-columns: repeat(2, minmax(0, 1fr));
        }

        .shortcut-card {
            min-height: 105px;
        }
    }
</style>
