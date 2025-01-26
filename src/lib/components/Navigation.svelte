<script lang="ts">
import { page } from '$app/stores';
import { onMount } from 'svelte';
import { slide } from 'svelte/transition';

export let navItems: Array<{
    href: string;
    label: string;
    icon?: string;
}>;

let isMenuOpen = false;
let isMobile = false;

function toggleMenu() {
    isMenuOpen = !isMenuOpen;
}

onMount(() => {
    const checkMobile = () => {
        isMobile = window.innerWidth < 768;
    };
    checkMobile();
    window.addEventListener('resize', checkMobile);
    return () => window.removeEventListener('resize', checkMobile);
});
</script>

<nav class="fixed top-0 left-0 w-full bg-black/90 backdrop-blur-md z-[100] border-b border-green-500/30 shadow-lg">
    <div class="container mx-auto px-4 py-4 relative">
        <div class="flex justify-between items-center">
            <a 
                href="/" 
                class="text-2xl text-green-400 font-mono tracking-widest glitch-text" 
                data-text="[JEROME_ANDREW]"
            >
                [JEROME_ANDREW]/
                <div class="text-sm text-green-300/80 mt-1 subtle-glitch">
                    // Security Research & Development Specialist
                </div>
            </a>
            
            <!-- Mobile Menu Button -->
            <button 
                class="md:hidden text-green-400 hover:text-green-300 transition-colors p-2 -mr-2"
                on:click={toggleMenu}
                aria-label="Toggle menu"
            >
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    {#if !isMenuOpen}
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
                    {:else}
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/>
                    {/if}
                </svg>
            </button>

            <!-- Desktop Navigation -->
            <div class="hidden md:flex space-x-6">
                {#each navItems as item}
                    <a 
                        href={item.href}
                        class="text-green-400 hover:text-green-300 transition-colors font-mono uppercase text-sm tracking-wider {$page.url.pathname === item.href ? 'border-b-2 border-green-400' : ''}"
                    >
                        {item.label}
                    </a>
                {/each}
            </div>
        </div>

        <!-- Mobile Navigation -->
        {#if isMenuOpen}
            <div 
                class="md:hidden fixed left-0 right-0 top-[72px] bg-black/95 border-t border-green-500/30 max-h-[calc(100vh-72px)] overflow-y-auto"
                transition:slide={{duration: 200}}
            >
                <div class="flex flex-col py-4 space-y-2">
                    {#each navItems as item}
                        <a 
                            href={item.href}
                            class="text-green-400 hover:text-green-300 transition-colors font-mono uppercase text-sm tracking-wider px-6 py-4 {$page.url.pathname === item.href ? 'bg-green-400/10' : ''} active:bg-green-400/20"
                            on:click={() => isMenuOpen = false}
                        >
                            {item.label}
                        </a>
                    {/each}
                </div>
            </div>
        {/if}
    </div>
</nav>

<style>
.glitch-text {
    position: relative;
    text-shadow: 0.02em 0 0 rgba(255, 0, 0, 0.3),
            -0.02em -0.01em 0 rgba(0, 255, 0, 0.3),
            -0.01em 0.02em 0 rgba(0, 0, 255, 0.3);
    animation: glitch 4s infinite;
}

.subtle-glitch {
    text-shadow: 0.01em 0 0 rgba(0, 255, 0, 0.2),
            -0.01em 0 0 rgba(0, 255, 0, 0.2);
    animation: subtle-glitch 6s infinite linear;
}

.glitch-text::before,
.glitch-text::after {
    content: attr(data-text);
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0.8;
}

.glitch-text::before {
    animation: glitch 650ms infinite;
    clip-path: polygon(0 0, 100% 0, 100% 45%, 0 45%);
    transform: translate(-0.025em, -0.0125em);
    opacity: 0.8;
}

.glitch-text::after {
    animation: glitch 375ms infinite;
    clip-path: polygon(0 80%, 100% 20%, 100% 100%, 0 100%);
    transform: translate(0.0125em, 0.025em);
    opacity: 0.8;
}

@keyframes glitch {
    0% {
        text-shadow: 0.02em 0 0 rgba(255, 0, 0, 0.3),
                -0.02em -0.01em 0 rgba(0, 255, 0, 0.3),
                -0.01em 0.02em 0 rgba(0, 0, 255, 0.3);
    }
    2% {
        text-shadow: 0.02em 0 0 rgba(255, 0, 0, 0.3),
                -0.02em -0.01em 0 rgba(0, 255, 0, 0.3),
                -0.01em 0.02em 0 rgba(0, 0, 255, 0.3);
    }
    3% {
        text-shadow: -0.02em -0.01em 0 rgba(255, 0, 0, 0.3),
                0.01em 0.01em 0 rgba(0, 255, 0, 0.3),
                -0.02em -0.02em 0 rgba(0, 0, 255, 0.3);
    }
    6% {
        text-shadow: none;
    }
    100% {
        text-shadow: none;
    }
}

@keyframes subtle-glitch {
    0% { transform: translate(0); }
    1% { transform: translate(-1px, 1px); }
    2% { transform: translate(1px, -1px); }
    3% { transform: translate(0); }
    100% { transform: translate(0); }
}
</style>
