<script lang="ts">
    import { page } from "$app/state";
    import { Home } from "lucide-svelte";
    import { resolve } from "$app/paths";

    const navItems = [{ label: "Shortcuts", path: "/", icon: Home }];

    function isActive(path: string, currentPath: string): boolean {
        if (path === "/") return currentPath === "/";
        return currentPath.startsWith(path);
    }
</script>

<nav
    aria-label="Mobile navigation"
    class="fixed bottom-0 left-0 right-0 z-50 flex border-t-2 border-white bg-black p-2.5 md:hidden standalone:flex"
>
    <div
        class="mx-auto flex h-16 w-full max-w-md items-center justify-around px-2"
    >
        {#each navItems as item (item.path)}
            {@const active = isActive(item.path, page.url.pathname)}

            <a
                href={resolve(item.path)}
                aria-current={active ? "page" : undefined}
                class={`flex flex-1 flex-col items-center justify-center gap-1 transition-all duration-200 ${
                    active
                        ? "text-[#E95420]"
                        : "text-white hover:text-[#E95420]"
                }`}
            >
                <div class="relative flex items-center justify-center">
                    <item.icon
                        size={active ? 24 : 22}
                        strokeWidth={active ? 2.5 : 2}
                        aria-hidden="true"
                    />

                    {#if active}
                        <span
                            class="absolute -bottom-1 h-1 w-1 rounded-full bg-[#E95420] shadow-[0_0_8px_#E95420]"
                        ></span>
                    {/if}
                </div>

                <span class="text-[10px] font-medium tracking-wide">
                    {item.label}
                </span>
            </a>
        {/each}
    </div>
</nav>

<style>
    nav {
        -webkit-tap-highlight-color: transparent;
        user-select: none;
    }

    @media (min-width: 900px) {
        nav {
            display: none;
        }
    }

    @media (display-mode: standalone) {
        nav {
            display: flex !important;
        }
    }
</style>
