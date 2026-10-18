<script>
    const stats = [
        { number: "2002", label: "Founded by Elon Musk" },
        { number: "12M", label: "Starlink subscribers (June 2026)" },
        { number: "78", label: "Launches in the first half of 2026" },
        { number: "$135", label: "Share price at IPO, 12 June 2026" },
    ];
</script>

<svelte:head>
    <title>SpaceX | Home</title>
</svelte:head>

<div class="page">
    <section class="hero">
        {#each ["right", "left"] as side}
            <svg class="rocket {side}" viewBox="0 0 120 320" aria-hidden="true">
                <path
                    class="flame"
                    d="M45 255 Q60 320 75 255 Q68 275 60 300 Q52 275 45 255Z"
                    fill="#c084fc"
                />
                <path
                    class="flame"
                    d="M50 255 Q60 295 70 255Z"
                    fill="#fff"
                    opacity="0.8"
                />
                <path d="M38 190 L10 250 L38 240Z" fill="#7c3aed" />
                <path d="M82 190 L110 250 L82 240Z" fill="#7c3aed" />
                <path
                    d="M60 10 Q90 60 85 160 L82 255 L38 255 L35 160 Q30 60 60 10Z"
                    fill="#f4f4f5"
                />
                <path
                    d="M60 10 Q78 40 82 75 L38 75 Q42 40 60 10Z"
                    fill="#7c3aed"
                />
                <circle
                    cx="60"
                    cy="115"
                    r="14"
                    fill="#1e1b2e"
                    stroke="#7c3aed"
                    stroke-width="4"
                />
                <rect x="38" y="225" width="44" height="6" fill="#7c3aed" />
            </svg>
        {/each}
        <div class="content">
            <h1 class="Heading">SpaceX</h1>
            <p class="tagline">Space Exploration Technologies Corp.</p>
            <p class="intro">
                SpaceX was started in 2002 by Elon Musk with one big idea: make
                going to space much cheaper so that one day people can live on
                Mars. Today it launches more rockets than any other company in
                the world and runs Starlink, the biggest satellite internet
                network.
            </p>
        </div>
    </section>

    <section class="stats">
        {#each stats as s}
            <div class="stat">
                <span class="number">{s.number}</span>
                <span class="label">{s.label}</span>
            </div>
        {/each}
    </section>

    <section class="block">
        <h2>Interesting facts</h2>
        <ul class="facts">
            <li>
                In 2020 it became the first private company to fly NASA
                astronauts to the International Space Station.
            </li>
            <li>
                It lands its Falcon 9 boosters back on Earth and flies them
                again, which makes each launch much cheaper.
            </li>
            <li>
                Its headquarters moved from Hawthorne, California to Starbase,
                Texas.
            </li>
            <li>
                Its IPO in June 2026 raised about $86 billion, the biggest in
                history.
            </li>
        </ul>
    </section>

    <section class="block">
        <h2>Type of business</h2>
        <div class="card">
            <p class="big">
                SpaceX is a <strong>public limited company</strong>.
            </p>
            <p>
                Until June 2026 it was a <strong>private limited company</strong
                >, so the public could not buy its shares. On 12 June 2026 it
                listed on the Nasdaq (ticker SPCX) to raise money for Starship,
                Starlink and AI data centres.
            </p>
            <p>
                It is not a sole trader, a partnership or a franchise. Its
                shareholders have
                <strong>limited liability</strong>, which means they can only
                lose the money they put in. Even after going public, Musk keeps
                control because his shares come with extra votes.
            </p>
        </div>
    </section>

    <section class="block">
        <h2>Why I chose SpaceX</h2>
        <div class="card">
            <p>
                <!-- Write your own reasons here -->
                I chose SpaceX because it is one of the most well-known companies
                in the space industry and has ambitious goals for the future.
            </p>
            <p>
                Also, SpaceX changed this year from a private to public
                business, it was intresting because it would allow more people
                to invest into this company.
            </p>
        </div>
    </section>

    <div class="next"><a href="/Promos&Offers">What SpaceX offers →</a></div>
</div>

<style>
    .page {
        font-family: "Space Grotesk", sans-serif;
    }

    /* hero */
    .hero {
        position: relative;
        overflow: hidden;
        text-align: center;
        padding: 10vh 6vw 6vh;
        background: radial-gradient(
                circle at 80% 20%,
                #3b1a6e 0,
                transparent 50%
            ),
            radial-gradient(circle at 20% 20%, #3b1a6e 0, transparent 50%),
            radial-gradient(1px 1px at 20% 30%, white, transparent),
            radial-gradient(1px 1px at 70% 80%, white, transparent),
            radial-gradient(1px 1px at 40% 60%, #ddd, transparent),
            radial-gradient(1px 1px at 90% 50%, white, transparent),
            radial-gradient(1px 1px at 10% 85%, #ddd, transparent), black;
        color: white;
    }
    .content {
        position: relative;
        z-index: 1;
    }
    .Heading {
        font-family: "Orbitron", sans-serif;
        font-size: clamp(2.5rem, 8vw, 5.5rem);
        letter-spacing: 0.15em;
        margin: 0;
        text-transform: uppercase;
    }
    .tagline {
        font-family: "Space Mono", monospace;
        color: #c084fc;
        margin: 0.5rem 0 2rem;
        text-transform: uppercase;
        letter-spacing: 0.1em;
        font-size: 0.9rem;
    }
    .intro {
        max-width: 650px;
        margin: 0 auto;
        line-height: 1.6;
        font-size: 1.1rem;
    }
    .rocket {
        position: absolute;
        top: 50%;
        height: 85%;
        opacity: 0.35;
    }
    .rocket.right {
        right: 8%;
        transform: translateY(-50%) rotate(25deg);
        animation: floatRight 4s ease-in-out infinite;
    }
    .rocket.left {
        left: 8%;
        transform: translateY(-50%) rotate(-25deg);
        animation: floatLeft 4s ease-in-out infinite;
    }
    .flame {
        transform-box: fill-box;
        transform-origin: top center;
        animation: flicker 0.15s alternate infinite;
    }
    @keyframes floatRight {
        0%,
        100% {
            transform: translateY(-50%) rotate(25deg);
        }
        50% {
            transform: translateY(-56%) rotate(25deg);
        }
    }
    @keyframes floatLeft {
        0%,
        100% {
            transform: translateY(-50%) rotate(-25deg);
        }
        50% {
            transform: translateY(-56%) rotate(-25deg);
        }
    }
    @keyframes flicker {
        from {
            transform: scaleY(1);
        }
        to {
            transform: scaleY(0.85);
        }
    }

    /* stats */
    .stats {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        background: white;
        border-bottom: 1px solid #ddd;
    }
    .stat {
        padding: 2rem 1rem;
        text-align: center;
        border-right: 1px solid #eee;
    }
    .stat:last-child {
        border-right: none;
    }
    .number {
        display: block;
        font-family: "Space Mono", monospace;
        font-size: 2rem;
        font-weight: bold;
        color: #7c3aed;
    }
    .label {
        font-size: 0.85rem;
        color: #666;
    }

    /* sections */
    .block {
        max-width: 1100px;
        margin: 0 auto;
        padding: 3rem 6vw 1rem;
    }
    h2 {
        font-family: "Orbitron", sans-serif;
        font-size: 1.8rem;
        margin: 0 0 1.2rem;
        padding-bottom: 0.5rem;
        border-bottom: 3px solid #7c3aed;
        display: inline-block;
        text-transform: uppercase;
        letter-spacing: 0.05em;
    }
    .card {
        background: white;
        padding: 1.4rem;
        border-radius: 8px;
        line-height: 1.5;
    }
    .card p {
        margin: 0 0 0.7rem;
    }
    .big {
        font-size: 1.3rem;
    }
    .facts li {
        margin-bottom: 0.6rem;
        line-height: 1.5;
    }

    /* next button */
    .next {
        text-align: center;
        padding: 3rem 0 4rem;
    }
    .next a {
        display: inline-block;
        font-family: "Orbitron", sans-serif;
        text-transform: uppercase;
        letter-spacing: 0.1em;
        text-decoration: none;
        color: white;
        background: black;
        padding: 0.9rem 1.6rem;
        border: 2px solid #7c3aed;
        transition: background 150ms;
    }
    .next a:hover {
        background: #7c3aed;
    }

    @media (max-width: 800px) {
        .stats {
            grid-template-columns: repeat(2, 1fr);
        }
        .rocket {
            opacity: 0.2;
        }
        .rocket.right {
            right: -10%;
        }
        .rocket.left {
            left: -10%;
        }
    }
</style>
