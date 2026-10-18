<script>
    import { onMount } from "svelte";

    let vw = $state(1200);
    let vh = $state(800);
    let mouseX = $state(600);
    let mouseY = $state(400);
    let rocketX = $state(600);
    let rocketY = $state(400);
    let angle = $state(0);
    let speed = $state(0);
    let puffs = $state([]);

    // Plain values (not state) so Svelte doesn't warn about local state references.
    let last = { x: 600, y: 400 };
    let puffId = 0;
    let lastPuff = 0;

    const compass = ["N", "NE", "E", "SE", "S", "SW", "W", "NW"];
    let heading = $derived(((Math.round(angle) % 360) + 360) % 360);
    let direction = $derived(compass[Math.round(heading / 45) % 8]);
    // Higher on screen means higher altitude.
    let altitude = $derived(Math.max(0, ((vh - mouseY) / vh) * 140));
    let px = $derived(mouseX / vw - 0.5);
    let py = $derived(mouseY / vh - 0.5);

    onMount(() => {
        mouseX = window.innerWidth / 2;
        mouseY = window.innerHeight / 2;
        rocketX = mouseX;
        rocketY = mouseY;
        last = { x: mouseX, y: mouseY };

        let frame;
        const animate = () => {
            // Smoothly accelerate toward the cursor instead of snapping to it.
            const dx = mouseX - rocketX;
            const dy = mouseY - rocketY;
            const distance = Math.hypot(dx, dy);
            rocketX += dx * 0.16;
            rocketY += dy * 0.16;

            if (distance > 1.5) {
                const targetAngle = Math.atan2(dy, dx) * (180 / Math.PI) + 90;
                const turn = ((targetAngle - angle + 540) % 360) - 180;
                angle += turn * 0.18;
            }
            speed = Math.min(60, distance * 0.7);
            if (distance < 0.5) speed = 0;

            frame = requestAnimationFrame(animate);
        };
        frame = requestAnimationFrame(animate);
        return () => cancelAnimationFrame(frame);
    });

    function handleMove(event) {
        const x = event.clientX;
        const y = event.clientY;
        const dx = x - last.x;
        const dy = y - last.y;
        const dist = Math.hypot(dx, dy);

        // The animation loop handles smooth steering and acceleration.

        // Vapour trail: soft puffs that spread out and fade behind the engine.
        const now = performance.now();
        if (dist > 3 && now - lastPuff > 35) {
            lastPuff = now;
            const rad = ((angle - 90) * Math.PI) / 180;
            const id = puffId++;
            const size = 16 + Math.random() * 14;
            const jitter = () => (Math.random() - 0.5) * 8;
            puffs = [
                ...puffs.slice(-45),
                {
                    id,
                    size,
                    x: x - Math.cos(rad) * 105 + jitter(),
                    y: y - Math.sin(rad) * 105 + jitter(),
                },
            ];
            setTimeout(() => {
                puffs = puffs.filter((p) => p.id !== id);
            }, 1500);
        }

        mouseX = x;
        mouseY = y;
        last = { x, y };
    }

    // Deterministic pseudo-random so the sky is identical on server and client.
    const rand = (n) => {
        const v = Math.sin(n * 127.1) * 43758.5453;
        return v - Math.floor(v);
    };
    const tints = ["#ffffff", "#ffffff", "#dbe6ff", "#ffeede"];
    const layers = [0, 1].map((layer) =>
        Array.from({ length: layer === 0 ? 150 : 60 }, (_, i) => {
            const n = i + layer * 1000;
            return {
                id: n,
                x: rand(n) * 100,
                y: rand(n + 7) * 100,
                size: layer === 1 && rand(n + 3) > 0.8 ? 2 : 1,
                opacity: 0.25 + rand(n + 5) * 0.65,
                color: tints[Math.floor(rand(n + 9) * tints.length)],
                twinkle: i % 6 === 0,
                delay: rand(n + 11) * 5,
            };
        }),
    );
    const depth = [6, 16];
</script>

<svelte:head>
    <title>SpaceX | Rocket Experience</title>
    <meta
        name="description"
        content="An interactive space experience where a rocket follows your mouse."
    />
</svelte:head>

<svelte:window
    bind:innerWidth={vw}
    bind:innerHeight={vh}
    onpointermove={handleMove}
/>

<div class="space">
    <div class="stars" aria-hidden="true">
        {#each layers as stars, l}
            <div
                class="layer"
                style:transform="translate({-px * depth[l]}px, {-py *
                    depth[l]}px)"
            >
                {#each stars as s (s.id)}
                    <span
                        class="star"
                        class:twinkle={s.twinkle}
                        style:left="{s.x}%"
                        style:top="{s.y}%"
                        style:width="{s.size}px"
                        style:height="{s.size}px"
                        style:background={s.color}
                        style:opacity={s.opacity}
                        style:animation-delay="{s.delay}s"
                    ></span>
                {/each}
            </div>
        {/each}
    </div>

    <!-- Earth's limb -->
    <div class="earth" aria-hidden="true"></div>
    <div class="grain" aria-hidden="true"></div>

    <header class="intro">
        <h1>Fly your own rocket.</h1>
        <p class="description">
            Move your cursor and the vehicle follows. Climb higher and the sky
            gets darker.
        </p>
    </header>

    {#each puffs as p (p.id)}
        <span
            class="puff"
            style:left="{p.x}px"
            style:top="{p.y}px"
            style:width="{p.size}px"
            style:height="{p.size}px"
            aria-hidden="true"
        ></span>
    {/each}

    <div
        class="rocket"
        style:left="{rocketX}px"
        style:top="{rocketY}px"
        style:--angle="{angle}deg"
        style:--thrust={1 + speed / 40}
        aria-hidden="true"
    >
        <div class="engine-glow"></div>

        <svg
            class="rocket-art"
            viewBox="0 0 120 260"
            xmlns="http://www.w3.org/2000/svg"
        >
            <defs>
                <linearGradient id="white" x1="0" x2="1">
                    <stop offset="0" stop-color="#868c96" />
                    <stop offset="0.25" stop-color="#e6e9ee" />
                    <stop offset="0.5" stop-color="#ffffff" />
                    <stop offset="0.8" stop-color="#c2c7cf" />
                    <stop offset="1" stop-color="#747a85" />
                </linearGradient>
                <linearGradient id="dark" x1="0" x2="1">
                    <stop offset="0" stop-color="#14161a" />
                    <stop offset="0.4" stop-color="#30343b" />
                    <stop offset="1" stop-color="#0d0e11" />
                </linearGradient>
                <linearGradient id="soot" x1="0" x2="0" y1="0" y2="1">
                    <stop offset="0" stop-color="#2a2522" stop-opacity="0" />
                    <stop offset="1" stop-color="#2a2522" stop-opacity="0.6" />
                </linearGradient>
                <linearGradient id="flame" x1="0" x2="0" y1="0" y2="1">
                    <stop offset="0" stop-color="#ffffff" />
                    <stop offset="0.25" stop-color="#ffe2b3" />
                    <stop
                        offset="0.6"
                        stop-color="#ff9a45"
                        stop-opacity="0.8"
                    />
                    <stop offset="1" stop-color="#ff6a1a" stop-opacity="0" />
                </linearGradient>
            </defs>

            <!-- Exhaust -->
            <g class="thrust">
                <path
                    class="flame"
                    d="M48 196 C50 220 56 240 60 258 C64 240 70 220 72 196Z"
                    fill="url(#flame)"
                />
                <path
                    class="core"
                    d="M54 196 C55 212 58 224 60 236 C62 224 65 212 66 196Z"
                    fill="#fff"
                />
            </g>

            <!-- Landing legs and grid fins -->
            <path d="M43 168 L35 190 L43 186Z" fill="#2a2e35" />
            <path d="M77 168 L85 190 L77 186Z" fill="#2a2e35" />
            <rect x="34" y="134" width="9" height="7" fill="#1c1f24" />
            <rect x="77" y="134" width="9" height="7" fill="#1c1f24" />

            <!-- Fairing -->
            <path
                d="M60 6 C68 14 73 28 77 56 L77 62 L43 62 L43 56 C47 28 52 14 60 6Z"
                fill="url(#white)"
            />
            <!-- Second stage -->
            <rect x="43" y="62" width="34" height="46" fill="url(#white)" />
            <!-- Interstage -->
            <rect x="43" y="108" width="34" height="22" fill="url(#dark)" />
            <!-- First stage -->
            <rect x="43" y="130" width="34" height="56" fill="url(#white)" />
            <rect x="43" y="150" width="34" height="36" fill="url(#soot)" />
            <!-- Panel lines -->
            <path
                d="M43 96 H77 M43 62 H77 M43 130 H77"
                stroke="#000"
                stroke-opacity="0.18"
            />
            <!-- Engine section -->
            <path d="M44 186 H76 L73 194 H47Z" fill="#15171b" />
            <rect x="49" y="194" width="5" height="4" fill="#0c0d10" />
            <rect x="57.5" y="194" width="5" height="4" fill="#0c0d10" />
            <rect x="66" y="194" width="5" height="4" fill="#0c0d10" />
        </svg>
    </div>

    <!-- Telemetry -->
    <aside class="telemetry" aria-label="Flight data">
        <div><span>Altitude</span><b>{altitude.toFixed(1)} km</b></div>
        <div>
            <span>Speed</span><b
                >{Math.round(speed * 95).toLocaleString("en-US")} km/h</b
            >
        </div>
        <div>
            <span>Heading</span><b
                >{String(heading).padStart(3, "0")}° {direction}</b
            >
        </div>
    </aside>
</div>

<style>
    .space {
        font-family: "Space Grotesk", sans-serif;
        color: #f4f5f7;
        position: relative;
        min-height: calc(100vh - 65px);
        overflow: hidden;
        isolation: isolate;
        background: linear-gradient(#000 0%, #02040a 60%, #050b1a 100%);
    }

    .stars,
    .layer {
        position: absolute;
        inset: 0;
        pointer-events: none;
    }

    .layer {
        transition: transform 500ms ease-out;
    }

    .star {
        position: absolute;
        border-radius: 50%;
    }

    .twinkle {
        animation: twinkle 4s ease-in-out infinite alternate;
    }

    @keyframes twinkle {
        to {
            opacity: 0.2;
        }
    }

    /* The curve of the planet with a thin lit atmosphere. */
    .earth {
        position: absolute;
        z-index: -1;
        left: 50%;
        bottom: calc(10vh - 170vw);
        width: 170vw;
        aspect-ratio: 1;
        border-radius: 50%;
        transform: translateX(-50%);
        background: radial-gradient(
            circle at 50% 0%,
            #2c6aa8 0%,
            #153a6b 14%,
            #0a1f40 32%,
            #040b1a 60%
        );
        box-shadow:
            0 -1px 2px 1px #bcdcff,
            0 -6px 22px 4px #4f94e0aa,
            0 -30px 90px 10px #1d4f9440;
        pointer-events: none;
    }

    /* Fine film grain keeps the black from looking flat and digital. */
    .grain {
        position: absolute;
        inset: 0;
        z-index: 3;
        opacity: 0.07;
        mix-blend-mode: screen;
        pointer-events: none;
        background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='160' height='160'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
    }

    .intro {
        position: relative;
        z-index: 2;
        width: min(640px, 90%);
        padding: clamp(60px, 12vh, 120px) 0 100px;
        margin-left: clamp(24px, 8vw, 120px);
        pointer-events: none;
    }

    h1 {
        margin: 0 0 20px;
        font-size: clamp(2.4rem, 5.6vw, 4.8rem);
        font-weight: 500;
        line-height: 1.05;
        letter-spacing: -0.03em;
        color: #fff;
    }

    .description {
        max-width: 400px;
        margin: 0;
        color: #9aa1ad;
        font-size: 1.05rem;
        line-height: 1.7;
    }

    /* Exhaust vapour */
    .puff {
        position: fixed;
        z-index: 4;
        border-radius: 50%;
        background: radial-gradient(
            circle,
            rgba(255, 255, 255, 0.42) 0%,
            rgba(205, 210, 220, 0.16) 55%,
            transparent 72%
        );
        filter: blur(3px);
        pointer-events: none;
        animation: puff 1.5s ease-out forwards;
    }

    @keyframes puff {
        from {
            opacity: 0.8;
            transform: translate(-50%, -50%) scale(0.4);
        }
        to {
            opacity: 0;
            transform: translate(-50%, -50%) scale(3.4);
        }
    }

    .rocket {
        position: fixed;
        z-index: 5;
        width: 100px;
        height: 225px;
        transform: translate(-50%, -50%) rotate(var(--angle));
        transition: none;
        pointer-events: none;
        will-change: left, top, transform;
    }

    .rocket-art {
        position: relative;
        z-index: 2;
        width: 100%;
        height: 100%;
        overflow: visible;
        filter: drop-shadow(0 2px 6px #00000080);
    }

    .thrust {
        transform-box: fill-box;
        transform-origin: top center;
        transform: scaleY(var(--thrust));
        transition: transform 120ms ease-out;
    }

    .flame {
        transform-box: fill-box;
        transform-origin: top center;
        animation: flicker 0.09s infinite alternate;
    }

    .core {
        animation: core 0.07s infinite alternate;
    }

    @keyframes flicker {
        from {
            transform: scale(1, 0.94);
            opacity: 0.85;
        }
        to {
            transform: scale(1.06, 1.04);
            opacity: 1;
        }
    }

    @keyframes core {
        from {
            opacity: 0.8;
        }
        to {
            opacity: 1;
        }
    }

    .engine-glow {
        position: absolute;
        left: 32%;
        top: 70%;
        width: 36%;
        height: 40%;
        background: #ff8a3d;
        opacity: 0.3;
        filter: blur(20px);
        border-radius: 50%;
    }

    .telemetry {
        position: absolute;
        z-index: 2;
        right: 28px;
        bottom: 24px;
        display: grid;
        gap: 6px;
        min-width: 190px;
        padding-top: 12px;
        border-top: 1px solid #ffffff40;
        font-size: 0.85rem;
        pointer-events: none;
    }

    .telemetry div {
        display: flex;
        justify-content: space-between;
        gap: 24px;
    }

    .telemetry span {
        color: #8b93a1;
    }

    .telemetry b {
        font-weight: 500;
        font-variant-numeric: tabular-nums;
        color: #fff;
    }

    @media (max-width: 700px) {
        .intro {
            margin-left: 24px;
            padding-top: 60px;
        }

        h1 {
            font-size: clamp(2.2rem, 10vw, 3.4rem);
        }

        .rocket {
            width: 65px;
            height: 146px;
        }

        .telemetry {
            right: 14px;
            bottom: 14px;
            min-width: 160px;
            font-size: 0.75rem;
        }
    }

    @media (prefers-reduced-motion: reduce) {
        .twinkle,
        .flame,
        .core {
            animation: none;
        }

        .rocket,
        .layer,
        .thrust {
            transition: none;
        }

        .puff {
            display: none;
        }
    }
</style>
