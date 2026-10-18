<script>
    import { page } from "$app/state";

    let { children } = $props();
</script>

<svelte:head>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link
        href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600;800&family=Space+Grotesk:wght@400;600&family=Space+Mono:wght@700&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<main>
    <div class="nav">
        <a href="/" class:active={page.url.pathname === "/"}>Home</a>
        <a
            href="/Promos&Offers"
            class:active={page.url.pathname === "/Promos&Offers"}
            >Promos&Offers</a
        >
        <a href="/Impact" class:active={page.url.pathname === "/Impact"}
            >Impact</a
        >
        <a href="/Rocketship" class:active={page.url.pathname === "/Rocketship"}
            >Rocketship</a
        >
    </div>

    {@render children()}
</main>

<style>
    :global(body) {
        background-color: rgb(235, 235, 235);
        margin: 0;
    }
    .nav {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 3vw;
        padding: 2.5vh;
        background-color: black;
        border-bottom: 2px solid #7c3aed;
    }
    .nav a {
        text-decoration: none;
        color: white;
        font-family: "Orbitron", sans-serif;
        font-weight: 600;
        font-size: 0.9rem;
        text-transform: uppercase;
        letter-spacing: 0.1em;
        transition:
            transform 100ms ease-in-out,
            color 150ms;
    }
    .nav a:hover {
        transform: scale(1.1);
        color: #c084fc;
    }
    .nav a.active {
        color: #c084fc;
        border-bottom-color: #c084fc;
    }
</style>
