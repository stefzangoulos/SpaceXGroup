<script>
    const stakeholders = [
        {
            who: "Owners and shareholders",
            type: "Internal",
            why: "Want the company to grow and provide a financial return. Elon Musk is the biggest owner and controls about 82-85% of the votes.",
        },
        {
            who: "Employees",
            type: "Internal",
            why: "Want fair wages, job security and safe working conditions.",
        },
        {
            who: "Customers",
            type: "External",
            why: "Want reliable Starlink internet and successful rocket launches. This includes home users, airlines, NASA and other companies.",
        },
        {
            who: "Suppliers",
            type: "External",
            why: "Want regular orders and to be paid on time for the materials and equipment they provide, like metal, chips and fuel.",
        },
        {
            who: "Government and regulators",
            type: "External",
            why: "Want the company to follow laws and safety regulations. The US government is also a big customer, giving about a fifth of SpaceX revenue in 2025.",
        },
        {
            who: "Local communities",
            type: "External",
            why: "Want jobs and investment in their area, but also expect the company to manage noise, road closures and environmental impacts responsibly, for example around Starbase, Texas.",
        },
    ];

    const sources = [
        {
            title: "Initial public offering of SpaceX",
            site: "Wikipedia",
            url: "https://en.wikipedia.org/wiki/Initial_public_offering_of_SpaceX",
            supports: "IPO date, $135 share price, Musk voting control",
        },
        {
            title: "SpaceX sets terms for record-breaking IPO",
            site: "Renaissance Capital",
            url: "https://www.renaissancecapital.com/IPO-Center/News/119552/SpaceX-sets-terms-for-record-breaking-$75-billion-IPO",
            supports: "Size of the IPO, Starlink satellites, founded 2002",
        },
        {
            title: "SpaceX: $75 billion IPO priced at $135 per share",
            site: "Pulse 2.0",
            url: "https://pulse2.com/spacex-75-billion-ipo-priced-at-135-per-share/amp/",
            supports: "Final IPO price and amount raised",
        },
        {
            title: "SpaceX files IPO prospectus offering a peek into its finances",
            site: "Yahoo Finance",
            url: "https://finance.yahoo.com/markets/article/spacex-files-ipo-prospectus-offering-a-peek-into-its-finances-205406189.html",
            supports: "2025 revenue, Starlink subscribers, AI segment",
        },
        {
            title: "SpaceX reveals that Starlink is paying the bills",
            site: "Broadband Breakfast",
            url: "https://broadbandbreakfast.com/spacex-ready-to-go-public-in-massive-ipo-reveals-that-starlink-is-paying-the-bills",
            supports:
                "Starlink revenue of $11.4 billion in 2025, xAI and X joining SpaceX, government share of revenue",
        },
        {
            title: "SpaceX acquires xAI as Musk moves to unite AI and space ambitions",
            site: "New Straits Times",
            url: "https://www.nst.com.my/amp/business/corporate/2026/02/1370202/spacex-acquires-xai-musk-moves-unite-ai-space-ambitions",
            supports: "Acquisition of xAI in February 2026",
        },
        {
            title: "SpaceX Q2 earnings call highlights",
            site: "Nasdaq",
            url: "https://www.nasdaq.com/articles/spacex-q2-earnings-call-highlights",
            supports:
                "Q2 2026 revenue of $7.8 billion, 12 million subscribers, 78 launches, 10,200 satellites",
        },
        {
            title: "SpaceX stock falls despite revenue beat",
            site: "Techloy",
            url: "https://www.techloy.com/spacex-stock-falls-despite-revenue-beat/",
            supports:
                "Starlink 55% and launches 12% of revenue, $541 million loss",
        },
        {
            title: "Elon Musk’s SpaceX posts $541M loss; Starlink subscribers surge",
            site: "Fox6 News",
            url: "https://www.fox6now.com/news/elon-musks-spacex-posts-541m-loss-starlink-subscribers-surge",
            supports: "Q2 2026 loss, Moon landing goal for 2028",
        },
        {
            title: "NASA’s SpaceX Demo-2 launch",
            site: "NASA",
            url: "https://blogs.nasa.gov/commercialcrew/2020/05/30/nasas-spacex-demo-2-launch-a-great-day-for-america",
            supports: "First crewed flight to the space station in 2020",
        },
        {
            title: "Elon Musk says he’s moving SpaceX headquarters from California to Texas",
            site: "Manufacturing.net",
            url: "https://www.manufacturing.net/operations/news/22915135/elon-musk-says-hes-moving-spacex-x-headquarters-from-california-to-texas",
            supports: "Headquarters move to Starbase, Texas",
        },
    ];

    const objectives = [
        {
            type: "Financial",
            title: "Make a profit",
            goal: "Turn the Q2 2026 net loss of $541 million into a net profit in at least one quarter before 30 June 2027.",
            smart: [
                ["Specific", "net profit in a quarter"],
                ["Measurable", "shown in the quarterly accounts"],
                [
                    "Achievable",
                    "the loss already went down from $1 billion a year earlier",
                ],
                ["Relevant", "new shareholders expect profit"],
                ["Time-bound", "by 30 June 2027"],
            ],
        },
        {
            type: "Financial",
            title: "Grow Starlink revenue",
            goal: "Increase Connectivity (Starlink) revenue by 40%, from $11.4 billion in 2025 to $16 billion in 2026.",
            smart: [
                ["Specific", "revenue of one part of the business"],
                ["Measurable", "a dollar amount"],
                ["Achievable", "Q2 2026 alone brought in $4.29 billion"],
                ["Relevant", "it is the biggest source of income"],
                ["Time-bound", "by the end of 2026"],
            ],
        },
        {
            type: "Non-financial",
            title: "Land on the Moon",
            goal: "Land astronauts on the Moon using Starship by 31 December 2028.",
            smart: [
                ["Specific", "a crewed Moon landing"],
                ["Measurable", "it either happens or it does not"],
                [
                    "Achievable",
                    "SpaceX has a NASA contract and is testing Starship",
                ],
                ["Relevant", "fits the mission of reaching other worlds"],
                ["Time-bound", "by the end of 2028"],
            ],
        },
        {
            type: "Non-financial",
            title: "More customers",
            goal: "Grow Starlink from 12 million to 18 million subscribers by 30 June 2027.",
            smart: [
                ["Specific", "number of subscribers"],
                ["Measurable", "reported every quarter"],
                ["Achievable", "it added 6 million in the last 12 months"],
                ["Relevant", "connecting more people around the world"],
                ["Time-bound", "by 30 June 2027"],
            ],
        },
    ];

    let openObjective = $state(null);

    function toggle(i) {
        openObjective = openObjective === i ? null : i;
    }
</script>

<svelte:head>
    <title>SpaceX | Impact</title>
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
            <h1 class="Heading">Impact</h1>
            <p class="tagline">Stakeholders & objectives</p>
            <p class="intro">
                Who SpaceX affects, and what it is trying to achieve.
            </p>
        </div>
    </section>

    <section class="block">
        <h2>Stakeholders</h2>
        <p class="lead">
            A stakeholder is any person or group affected by what a business
            does. SpaceX has six main stakeholder groups.
        </p>
        <div class="grid three">
            {#each stakeholders as s}
                <div class="card">
                    <span class="tag" class:nonfin={s.type === "External"}
                        >{s.type}</span
                    >
                    <h3>{s.who}</h3>
                    <p>{s.why}</p>
                </div>
            {/each}
        </div>
        <div class="note">
            <p><strong>Conflicting interests</strong></p>
            <p>
                Stakeholders do not always want the same thing. For example, <strong
                    >shareholders</strong
                >
                may want SpaceX to keep costs low so profits are higher, while
                <strong>employees</strong> want higher wages, which increases costs.
            </p>
            <p>
                Another example: shareholders want SpaceX to test and launch
                rockets as often as possible, but <strong
                    >local communities</strong
                > near the launch site want less noise and less damage to the environment.
            </p>
        </div>
    </section>

    <section class="block">
        <h2>Objectives</h2>
        <p class="hint">Click an objective to see why it is SMART.</p>
        <div class="grid objectives">
            {#each objectives as o, i}
                <button
                    class="card objective"
                    class:open={openObjective === i}
                    onclick={() => toggle(i)}
                >
                    <span class="tag" class:nonfin={o.type === "Non-financial"}
                        >{o.type}</span
                    >
                    <h3>{o.title}</h3>
                    <p>{o.goal}</p>
                    {#if openObjective === i}
                        <ul class="smart">
                            {#each o.smart as [letter, reason]}
                                <li><strong>{letter}:</strong> {reason}</li>
                            {/each}
                        </ul>
                    {/if}
                </button>
            {/each}
        </div>
    </section>

    <section class="block sources">
        <h2>Sources / References</h2>
        <ol>
            {#each sources as src}
                <li>
                    <a href={src.url} target="_blank" rel="noopener noreferrer"
                        >{src.title}</a
                    >
                    <span class="site">({src.site})</span>
                    <br /><span class="supports">Supports: {src.supports}</span>
                </li>
            {/each}
        </ol>
    </section>

    <div class="next"><a href="/">← Back to home</a></div>
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
        grid-template-columns: repeat(2, 1fr);
        gap: 1.2rem;
    }
    .grid.three {
        grid-template-columns: repeat(3, 1fr);
    }
    .lead {
        margin: 0 0 1.2rem;
        line-height: 1.5;
    }
    .note p {
        margin: 0 0 0.6rem;
    }
    .note p:last-child {
        margin-bottom: 0;
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
    .note {
        margin-top: 1.2rem;
        padding: 1rem 1.2rem;
        border-left: 4px solid #7c3aed;
        background: white;
        line-height: 1.5;
    }
    .hint {
        color: #666;
        margin-top: -0.5rem;
    }

    /* objectives */
    .objectives {
        align-items: start;
    }
    .objective {
        text-align: left;
        border: 2px solid transparent;
        cursor: pointer;
        font: inherit;
        color: inherit;
        transition: border-color 150ms;
    }
    .objective:hover,
    .objective.open {
        border-color: #7c3aed;
    }
    .tag {
        display: inline-block;
        font-family: "Space Mono", monospace;
        font-size: 0.75rem;
        font-weight: bold;
        text-transform: uppercase;
        padding: 0.2rem 0.6rem;
        border-radius: 20px;
        background: #7c3aed;
        color: white;
        margin-bottom: 0.6rem;
    }
    .tag.nonfin {
        background: black;
    }
    .smart {
        margin: 0.8rem 0 0;
        padding-left: 1.1rem;
        font-size: 0.95rem;
    }
    .sources {
        font-size: 0.95rem;
        color: #333;
    }
    .sources li {
        margin-bottom: 0.8rem;
        line-height: 1.4;
    }
    .sources a {
        color: #7c3aed;
        font-weight: 600;
    }
    .site {
        color: #666;
    }
    .supports {
        font-size: 0.85rem;
        color: #777;
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
        .grid,
        .grid.three {
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
