<script>
    const activities = [
        {
            title: "Space",
            text: "SpaceX designs, builds and launches rockets like Falcon 9, Falcon Heavy and Starship, and the Dragon capsule that carries astronauts. Its customers include NASA, governments and companies that need satellites put into orbit.",
        },
        {
            title: "Starlink",
            text: "Satellite internet that works almost anywhere in the world. By June 2026 it had about 12 million subscribers and around 10,200 satellites. This is now where most of SpaceX’s money comes from.",
        },
        {
            title: "AI",
            text: "In February 2026 SpaceX took over xAI, the company behind Grok, and the social network X. It now sells AI models and cloud computing as well.",
        },
    ];

    const customers = [
        {
            who: "Homes",
            what: "Internet for people in villages and places where normal internet is slow or missing.",
        },
        {
            who: "Travel",
            what: "Wi-Fi on planes, ships and in cars, even far away from land.",
        },
        {
            who: "Phones",
            what: "Starlink Mobile works with phone companies like T-Mobile so phones can connect through satellites.",
        },
        {
            who: "Governments",
            what: "Launches for NASA and the US military, plus secure communication satellites.",
        },
    ];
</script>

<svelte:head>
    <title>SpaceX | Promos & Offers</title>
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
            <h1 class="Heading">What SpaceX offers</h1>
            <p class="tagline">Activities of the company</p>
            <p class="intro">
                SpaceX started as a rocket company, but today it makes most of
                its money from internet and is growing fast in AI.
            </p>
        </div>
    </section>

    <section class="block">
        <h2>Main activities</h2>
        <div class="grid three">
            {#each activities as a}
                <div class="card">
                    <h3>{a.title}</h3>
                    <p>{a.text}</p>
                </div>
            {/each}
        </div>
        <p class="note">
            SpaceX is in the <strong>secondary sector</strong> because it
            manufactures rockets and satellites, and in the
            <strong>tertiary sector</strong> because it sells services like launches,
            internet and AI.
        </p>
    </section>

    <section class="block">
        <h2>Who buys from SpaceX?</h2>
        <div class="grid two">
            {#each customers as c}
                <div class="card">
                    <h3>{c.who}</h3>
                    <p>{c.what}</p>
                </div>
            {/each}
        </div>
        <p class="note">
            In Q2 2026 Starlink brought in <strong>55%</strong> of all SpaceX
            revenue, while rocket launches brought in only about
            <strong>12%</strong>.
        </p>
    </section>

    <div class="next"><a href="/Impact">Stakeholders & objectives →</a></div>
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
    h3 {
        font-family: "Space Mono", monospace;
        color: #7c3aed;
        margin: 0 0 0.6rem;
    }
    .grid {
        display: grid;
        gap: 1.2rem;
    }
    .three {
        grid-template-columns: repeat(3, 1fr);
    }
    .two {
        grid-template-columns: repeat(2, 1fr);
    }
    .card {
        background: white;
        padding: 1.4rem;
        border-radius: 8px;
        line-height: 1.5;
    }
    .card p {
        margin: 0;
    }
    .note {
        margin-top: 1.2rem;
        padding: 1rem 1.2rem;
        border-left: 4px solid #7c3aed;
        background: white;
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
        .three,
        .two {
            grid-template-columns: 1fr;
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
