<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Assignment 6.3 — Overflow & Layout Fixing</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Fira+Code:wght@400;500&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['"Plus Jakarta Sans"', 'sans-serif'],
                        mono: ['"Fira Code"', 'monospace'],
                    },
                    colors: {
                        brand: {
                            50: '#eef2ff',
                            100: '#e0e7ff',
                            500: '#6366f1',
                            600: '#4f46e5',
                            700: '#4338ca',
                            900: '#312e81',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        /* Custom scrollbar styling for custom auto containers */
        .custom-scrollbar::-webkit-scrollbar {
            width: 8px;
            height: 8px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: rgba(99, 102, 241, 0.05);
            border-radius: 9999px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: rgba(99, 102, 241, 0.4);
            border-radius: 9999px;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb:hover {
            background: rgba(99, 102, 241, 0.7);
        }

        /* Overflow specific behavior classes for playground test */
        .overflow-demo-visible { overflow: visible !important; }
        .overflow-demo-hidden { overflow: hidden !important; }
        .overflow-demo-auto { overflow: auto !important; }
        .overflow-demo-scroll { overflow: scroll !important; }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 font-sans min-h-screen flex flex-col antialiased">

    <!-- Top Navigation Header -->
    <header class="sticky top-0 z-50 bg-slate-900/80 backdrop-blur-md border-b border-slate-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3">
                <div class="h-10 w-10 rounded-xl bg-gradient-to-tr from-indigo-600 to-violet-500 flex items-center justify-center text-white font-bold text-lg shadow-lg shadow-indigo-500/20">
                    <i class="fa-solid fa-arrows-to-dot"></i>
                </div>
                <div>
                    <h1 class="font-bold text-slate-100 text-base sm:text-lg leading-tight">Assignment 6.3</h1>
                    <p class="text-xs text-indigo-400 font-medium">Overflow & Layout Fixing</p>
                </div>
            </div>
            
            <nav class="hidden md:flex items-center gap-1 bg-slate-800/80 p-1 rounded-xl border border-slate-700/60 text-xs font-medium">
                <a href="#overview" class="px-3 py-1.5 rounded-lg text-slate-300 hover:text-white hover:bg-slate-700/50 transition">Overview</a>
                <a href="#demo" class="px-3 py-1.5 rounded-lg text-slate-300 hover:text-white hover:bg-slate-700/50 transition">Step 1-3: Properties</a>
                <a href="#auto-box" class="px-3 py-1.5 rounded-lg text-slate-300 hover:text-white hover:bg-slate-700/50 transition">Step 4: Auto Container</a>
                <a href="#fix-exercise" class="px-3 py-1.5 rounded-lg text-slate-300 hover:text-white hover:bg-slate-700/50 transition">Step 5: Layout Fix</a>
                <a href="#submission" class="px-3 py-1.5 rounded-lg text-indigo-400 hover:text-indigo-300 hover:bg-indigo-950/40 transition">Submission Code</a>
            </nav>

            <div class="flex items-center gap-2">
                <a href="#submission" class="bg-indigo-600 hover:bg-indigo-500 text-white text-xs font-semibold px-4 py-2 rounded-lg shadow-md transition flex items-center gap-2">
                    <i class="fa-solid fa-paper-plane"></i>
                    <span>Export Code</span>
                </a>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 space-y-12">

        <!-- Header / Overview Section -->
        <section id="overview" class="bg-gradient-to-r from-slate-800/80 via-indigo-950/40 to-slate-800/80 border border-slate-700/60 rounded-3xl p-6 sm:p-8 backdrop-blur-sm relative overflow-hidden">
            <div class="absolute -right-16 -bottom-16 w-64 h-64 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none"></div>
            
            <div class="flex flex-col md:flex-row gap-6 justify-between items-start md:items-center relative z-10">
                <div class="space-y-3 max-w-3xl">
                    <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-indigo-500/10 text-indigo-400 border border-indigo-500/20 text-xs font-semibold">
                        <i class="fa-solid fa-graduation-cap"></i> Web Development Module 6
                    </div>
                    <h2 class="text-2xl sm:text-3xl font-extrabold text-white tracking-tight">
                        Assignment 6.3 — Overflow & Layout Fixing
                    </h2>
                    <p class="text-slate-300 text-sm sm:text-base leading-relaxed">
                        Explore how CSS handles content when elements exceed their fixed dimensions. Learn to utilize <code class="bg-slate-900 text-indigo-300 px-1.5 py-0.5 rounded font-mono text-xs">overflow: visible</code>, <code class="bg-slate-900 text-indigo-300 px-1.5 py-0.5 rounded font-mono text-xs">hidden</code>, <code class="bg-slate-900 text-indigo-300 px-1.5 py-0.5 rounded font-mono text-xs">auto</code>, and <code class="bg-slate-900 text-indigo-300 px-1.5 py-0.5 rounded font-mono text-xs">scroll</code>, and diagnose real-world layout breaking issues.
                    </p>
                </div>

                <!-- Checklist summary -->
                <div class="bg-slate-900/90 border border-slate-700/80 rounded-2xl p-4 w-full md:w-72 shrink-0 space-y-2 text-xs">
                    <div class="font-bold text-slate-200 uppercase tracking-wider text-[10px] mb-2 flex items-center justify-between">
                        <span>Assignment Checklist</span>
                        <span class="text-indigo-400">5 / 5 Complete</span>
                    </div>
                    <div class="flex items-center gap-2.5 text-slate-300">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i>
                        <span>1. Fixed Height Container</span>
                    </div>
                    <div class="flex items-center gap-2.5 text-slate-300">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i>
                        <span>2. Overflowing Content</span>
                    </div>
                    <div class="flex items-center gap-2.5 text-slate-300">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i>
                        <span>3. Test 4 Overflow Properties</span>
                    </div>
                    <div class="flex items-center gap-2.5 text-slate-300">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i>
                        <span>4. Dedicated auto Container</span>
                    </div>
                    <div class="flex items-center gap-2.5 text-slate-300">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i>
                        <span>5. Diagnose & Fix Layout Issue</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Steps 1-3: Interactive Overflow Simulator & Grid Comparison -->
        <section id="demo" class="space-y-6">
            <div class="flex flex-col md:flex-row md:items-end justify-between gap-4">
                <div>
                    <div class="text-indigo-400 text-xs font-bold uppercase tracking-wider">Steps 1, 2 & 3</div>
                    <h3 class="text-xl sm:text-2xl font-bold text-white">Interactive CSS Overflow Testbench</h3>
                    <p class="text-slate-400 text-sm mt-1">Test each CSS overflow value on a fixed height (160px) & width container filled with excess text.</p>
                </div>

                <!-- Controls for active property filter in main preview -->
                <div class="flex flex-wrap items-center gap-1.5 bg-slate-800 p-1.5 rounded-xl border border-slate-700">
                    <button onclick="setGlobalOverflow('all')" id="btn-all" class="overflow-tab-btn active px-3 py-1.5 rounded-lg text-xs font-semibold transition bg-indigo-600 text-white">Grid View (All 4)</button>
                    <button onclick="setGlobalOverflow('visible')" id="btn-visible" class="overflow-tab-btn px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">visible</button>
                    <button onclick="setGlobalOverflow('hidden')" id="btn-hidden" class="overflow-tab-btn px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">hidden</button>
                    <button onclick="setGlobalOverflow('auto')" id="btn-auto" class="overflow-tab-btn px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">auto</button>
                    <button onclick="setGlobalOverflow('scroll')" id="btn-scroll" class="overflow-tab-btn px-3 py-1.5 rounded-lg text-xs font-semibold text-slate-400 hover:text-white transition">scroll</button>
                </div>
            </div>

            <!-- 4 Cards Grid -->
            <div id="overflow-grid" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">

                <!-- 1. OVERFLOW VISIBLE -->
                <div class="card-overflow-item bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 flex flex-col justify-between relative group hover:border-slate-600 transition" data-prop="visible">
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="font-mono text-sm font-bold text-amber-400 bg-amber-400/10 px-2.5 py-1 rounded-md border border-amber-400/20">
                                overflow: visible
                            </span>
                            <span class="text-xs text-slate-400">Default</span>
                        </div>
                        <p class="text-xs text-slate-300 mb-4 h-12">
                            Content is not clipped and renders outside the container box boundaries without scrollbars.
                        </p>

                        <!-- Fixed Height Container -->
                        <div class="relative bg-slate-900 border-2 border-dashed border-amber-500/60 rounded-xl p-4 h-40 w-full mb-12 overflow-demo-visible">
                            <div class="absolute -top-2.5 left-3 bg-amber-500 text-slate-950 font-bold text-[10px] uppercase px-1.5 rounded">
                                Height: 160px
                            </div>
                            <p class="text-slate-200 text-xs leading-relaxed">
                                <strong class="text-amber-300">Overflowing Content:</strong> Cascading Style Sheets (CSS) allows web developers to dictate layout styles. When text inside a container exceeds the declared height limit of 160px, <code class="font-mono text-amber-300">overflow: visible</code> lets the content spill straight out into adjacent elements or page areas without masking or providing scrolling functionality. This can cause overlapping content bugs!
                            </p>
                        </div>
                    </div>

                    <div class="mt-auto pt-4 border-t border-slate-700/50 text-[11px] text-slate-400 space-y-1">
                        <div class="flex items-center gap-1.5 text-amber-400 font-medium">
                            <i class="fa-solid fa-triangle-exclamation"></i> Risks layout collisions
                        </div>
                    </div>
                </div>

                <!-- 2. OVERFLOW HIDDEN -->
                <div class="card-overflow-item bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 flex flex-col justify-between relative group hover:border-slate-600 transition" data-prop="hidden">
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="font-mono text-sm font-bold text-rose-400 bg-rose-400/10 px-2.5 py-1 rounded-md border border-rose-400/20">
                                overflow: hidden
                            </span>
                            <span class="text-xs text-slate-400">Clipped</span>
                        </div>
                        <p class="text-xs text-slate-300 mb-4 h-12">
                            Content is clipped to fit the container bounds. Overflowing content is invisible and unscrollable.
                        </p>

                        <!-- Fixed Height Container -->
                        <div class="relative bg-slate-900 border-2 border-slate-700 rounded-xl p-4 h-40 w-full mb-6 overflow-demo-hidden">
                            <div class="absolute -top-2.5 left-3 bg-slate-700 text-slate-200 font-bold text-[10px] uppercase px-1.5 rounded">
                                Height: 160px
                            </div>
                            <p class="text-slate-200 text-xs leading-relaxed">
                                <strong class="text-rose-300">Clipped Content:</strong> Cascading Style Sheets (CSS) allows web developers to dictate layout styles. When text inside a container exceeds the declared height limit of 160px, <code class="font-mono text-rose-300">overflow: hidden</code> neatly cuts off all excess text at the exact bottom border. The remaining text is permanently inaccessible unless revealed programmatically.
                            </p>
                        </div>
                    </div>

                    <div class="mt-auto pt-4 border-t border-slate-700/50 text-[11px] text-slate-400 space-y-1">
                        <div class="flex items-center gap-1.5 text-rose-400 font-medium">
                            <i class="fa-solid fa-eye-slash"></i> Excess text hidden entirely
                        </div>
                    </div>
                </div>

                <!-- 3. OVERFLOW AUTO -->
                <div class="card-overflow-item bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 flex flex-col justify-between relative group hover:border-slate-600 transition" data-prop="auto">
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="font-mono text-sm font-bold text-emerald-400 bg-emerald-400/10 px-2.5 py-1 rounded-md border border-emerald-400/20">
                                overflow: auto
                            </span>
                            <span class="text-xs text-emerald-400 font-semibold">Recommended</span>
                        </div>
                        <p class="text-xs text-slate-300 mb-4 h-12">
                            Scrollbars are added <em class="text-emerald-300">only if needed</em> when content exceeds the container height.
                        </p>

                        <!-- Fixed Height Container -->
                        <div class="relative bg-slate-900 border-2 border-emerald-500/50 rounded-xl p-4 h-40 w-full mb-6 overflow-demo-auto custom-scrollbar">
                            <div class="absolute -top-2.5 left-3 bg-emerald-600 text-white font-bold text-[10px] uppercase px-1.5 rounded">
                                Height: 160px
                            </div>
                            <p class="text-slate-200 text-xs leading-relaxed">
                                <strong class="text-emerald-300">Adaptive Scrollbar:</strong> Cascading Style Sheets (CSS) allows web developers to dictate layout styles. When text inside a container exceeds the declared height limit of 160px, <code class="font-mono text-emerald-300">overflow: auto</code> detects the overflow condition and dynamically injects vertical or horizontal scrollbars. If the text were short, no scrollbar tracks would appear!
                            </p>
                        </div>
                    </div>

                    <div class="mt-auto pt-4 border-t border-slate-700/50 text-[11px] text-slate-400 space-y-1">
                        <div class="flex items-center gap-1.5 text-emerald-400 font-medium">
                            <i class="fa-solid fa-sliders"></i> Dynamic smart scrollbars
                        </div>
                    </div>
                </div>

                <!-- 4. OVERFLOW SCROLL -->
                <div class="card-overflow-item bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 flex flex-col justify-between relative group hover:border-slate-600 transition" data-prop="scroll">
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <span class="font-mono text-sm font-bold text-sky-400 bg-sky-400/10 px-2.5 py-1 rounded-md border border-sky-400/20">
                                overflow: scroll
                            </span>
                            <span class="text-xs text-slate-400">Always On</span>
                        </div>
                        <p class="text-xs text-slate-300 mb-4 h-12">
                            Scrollbars are <em class="text-sky-300">always visible</em> regardless of whether content overflows or fits.
                        </p>

                        <!-- Fixed Height Container -->
                        <div class="relative bg-slate-900 border-2 border-sky-500/50 rounded-xl p-4 h-40 w-full mb-6 overflow-demo-scroll custom-scrollbar">
                            <div class="absolute -top-2.5 left-3 bg-sky-600 text-white font-bold text-[10px] uppercase px-1.5 rounded">
                                Height: 160px
                            </div>
                            <p class="text-slate-200 text-xs leading-relaxed">
                                <strong class="text-sky-300">Constant Scrollbars:</strong> Cascading Style Sheets (CSS) allows web developers to dictate layout styles. When text inside a container exceeds the declared height limit of 160px, <code class="font-mono text-sky-300">overflow: scroll</code> forces scrollbars to render continuously. Notice how even if content fits, scrollbar tracks reserve layout space.
                            </p>
                        </div>
                    </div>

                    <div class="mt-auto pt-4 border-t border-slate-700/50 text-[11px] text-slate-400 space-y-1">
                        <div class="flex items-center gap-1.5 text-sky-400 font-medium">
                            <i class="fa-solid fa-square-parking"></i> Static track reservation
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Step 4: Dedicated `overflow: auto` Container Deep Dive -->
        <section id="auto-box" class="bg-slate-800/40 border border-slate-700/70 rounded-3xl p-6 sm:p-8 space-y-6">
            <div class="flex flex-col sm:flex-row justify-between sm:items-center gap-4 border-b border-slate-700/70 pb-5">
                <div>
                    <div class="text-indigo-400 text-xs font-bold uppercase tracking-wider">Step 4 Requirement</div>
                    <h3 class="text-xl sm:text-2xl font-bold text-white flex items-center gap-2">
                        <span>Dedicated <code class="text-emerald-400 font-mono">overflow: auto</code> Content Container</span>
                        <span class="bg-emerald-500/10 text-emerald-400 text-xs font-semibold px-2.5 py-0.5 rounded-full border border-emerald-500/20">Featured Component</span>
                    </h3>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="toggleAutoContentLength()" class="text-xs bg-slate-700 hover:bg-slate-600 text-slate-200 px-3 py-2 rounded-lg transition flex items-center gap-2 border border-slate-600">
                        <i class="fa-solid fa-arrows-rotate"></i>
                        <span id="auto-toggle-text">Toggle Short/Long Content</span>
                    </button>
                </div>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
                
                <!-- Left: Interactive Styled Scrollable Card -->
                <div class="lg:col-span-7 space-y-3">
                    <div class="flex items-center justify-between text-xs text-slate-400 px-1">
                        <span><i class="fa-solid fa-cube text-indigo-400"></i> Container Component Preview</span>
                        <span class="font-mono">height: 220px | width: 100%</span>
                    </div>

                    <!-- Scrollable Container Box -->
                    <div id="dedicated-auto-box" class="h-[220px] w-full bg-slate-900 border-2 border-emerald-500/40 rounded-2xl p-5 overflow-auto custom-scrollbar shadow-xl relative transition-all">
                        <div class="flex items-center justify-between border-b border-slate-800 pb-3 mb-4 sticky -top-5 bg-slate-900/95 backdrop-blur-md pt-1 z-10">
                            <div class="flex items-center gap-2">
                                <span class="h-2.5 w-2.5 rounded-full bg-emerald-400 animate-pulse"></span>
                                <h4 class="font-bold text-slate-100 text-sm">Web Standard Specifications — CSS Box Model</h4>
                            </div>
                            <span class="text-[10px] font-mono bg-emerald-950 text-emerald-400 border border-emerald-800/60 px-2 py-0.5 rounded">overflow: auto</span>
                        </div>

                        <div id="dedicated-auto-text" class="space-y-3 text-xs text-slate-300 leading-relaxed">
                            <p>
                                The CSS Box Model forms the foundation of all web layout architecture. Every element rendered on a webpage is a rectangular box comprising margins, borders, padding, and the actual content height and width.
                            </p>
                            <p>
                                When explicit <code class="font-mono text-indigo-300">height</code> constraints are declared on a container (such as this 220px tall component), any content surpassing that dimension is forced into an overflow condition.
                            </p>
                            <p>
                                By configuring <code class="font-mono text-emerald-400">overflow: auto</code>, we instruct the browser engine to dynamically evaluate the content box height. If the content height exceeds 220px, scrollbars are synthesized automatically to grant full accessibility to hidden text without compromising page structure.
                            </p>
                            <p>
                                Furthermore, custom vendor scrollbar styling can be attached via pseudo-elements like <code class="font-mono text-indigo-300">::-webkit-scrollbar</code>, granting full visual alignment with sleek dark-mode UI designs.
                            </p>
                        </div>
                    </div>

                    <!-- Status Bar -->
                    <div class="bg-slate-900/60 border border-slate-800 rounded-xl px-4 py-2.5 flex items-center justify-between text-xs">
                        <span class="text-slate-400 flex items-center gap-2">
                            <i class="fa-solid fa-info-circle text-indigo-400"></i>
                            <span id="scroll-status-text">Scrollbar currently active due to excess text.</span>
                        </span>
                        <span class="font-mono text-indigo-300 text-[11px]" id="scroll-percentage">Scroll Y: 0%</span>
                    </div>
                </div>

                <!-- Right: Code Snippet & Best Practices -->
                <div class="lg:col-span-5 space-y-4">
                    <div class="bg-slate-900 border border-slate-800 rounded-2xl p-5 space-y-4">
                        <h4 class="font-bold text-sm text-slate-100 flex items-center gap-2">
                            <i class="fa-solid fa-code text-emerald-400"></i> CSS Implementation Guide
                        </h4>
                        
                        <!-- Snippet -->
                        <pre class="bg-slate-950 p-3.5 rounded-xl text-xs font-mono text-slate-300 border border-slate-800/80 overflow-x-auto leading-relaxed">
<span class="text-indigo-400">.scrollable-card</span> {
  <span class="text-sky-300">height</span>: <span class="text-amber-300">220px</span>;
  <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">auto</span>; <span class="text-slate-500">/* Dynamic scrollbar */</span>
  <span class="text-sky-300">padding</span>: <span class="text-amber-300">1.25rem</span>;
}

<span class="text-slate-500">/* Sleek Custom Scrollbar */</span>
<span class="text-indigo-400">.scrollable-card::-webkit-scrollbar</span> {
  <span class="text-sky-300">width</span>: <span class="text-amber-300">8px</span>;
}
<span class="text-indigo-400">.scrollable-card::-webkit-scrollbar-thumb</span> {
  <span class="text-sky-300">background</span>: <span class="text-amber-300">#6366f1</span>;
  <span class="text-sky-300">border-radius</span>: <span class="text-amber-300">9999px</span>;
}</pre>

                        <div class="space-y-2 text-xs text-slate-300">
                            <div class="font-semibold text-slate-200">Why overflow: auto is standard practice:</div>
                            <ul class="space-y-1.5 list-disc list-inside text-slate-400">
                                <li>Prevents unnecessary scrollbars when text fits comfortably.</li>
                                <li>Ensures responsiveness on smaller screens and mobile devices.</li>
                                <li>Avoids layout clipping bug inherent with <code class="font-mono text-slate-300">overflow: hidden</code>.</li>
                            </ul>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Step 5: "Identify and Fix Layout Overflow Issue" Interactive Exercise -->
        <section id="fix-exercise" class="space-y-6">
            <div class="flex flex-col md:flex-row md:items-end justify-between gap-4">
                <div>
                    <div class="text-indigo-400 text-xs font-bold uppercase tracking-wider">Step 5 Requirement</div>
                    <h3 class="text-xl sm:text-2xl font-bold text-white">Identify & Fix Layout Overflow Issue</h3>
                    <p class="text-slate-400 text-sm mt-1">Simulate a broken user profile card with unhandled text & image overflow, then toggle the layout fix.</p>
                </div>

                <!-- Fix Toggle Control -->
                <div class="flex items-center bg-slate-800 p-1.5 rounded-xl border border-slate-700">
                    <button id="btn-show-broken" onclick="setFixState('broken')" class="px-4 py-2 rounded-lg text-xs font-bold transition bg-rose-600 text-white flex items-center gap-2">
                        <i class="fa-solid fa-bug"></i> Broken Layout (Issue Identified)
                    </button>
                    <button id="btn-show-fixed" onclick="setFixState('fixed')" class="px-4 py-2 rounded-lg text-xs font-bold transition text-slate-400 hover:text-white flex items-center gap-2">
                        <i class="fa-solid fa-wand-magic-sparkles text-emerald-400"></i> Fixed Layout
                    </button>
                </div>
            </div>

            <!-- Problem & Diagnosis Box -->
            <div id="diagnosis-box" class="bg-rose-950/30 border border-rose-500/30 rounded-2xl p-4 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
                <div class="flex items-start gap-3">
                    <div class="p-2.5 rounded-xl bg-rose-500/10 text-rose-400 border border-rose-500/20 text-lg">
                        <i id="diagnosis-icon" class="fa-solid fa-triangle-exclamation"></i>
                    </div>
                    <div>
                        <h4 id="diagnosis-title" class="font-bold text-slate-100 text-sm">Issue Identified: Card Layout Overflow & Destruction</h4>
                        <p id="diagnosis-desc" class="text-xs text-slate-300 mt-0.5">
                            Long URL strings without word-breaks extend out of the fixed width card border. Unconstrained images blow past container boundaries, breaking adjacent cards.
                        </p>
                    </div>
                </div>
                <div id="diagnosis-badge" class="shrink-0 px-3 py-1 rounded-full bg-rose-500/20 text-rose-300 font-mono text-xs font-semibold border border-rose-500/30">
                    STATUS: BROKEN (OVERFLOW VISIBLE)
                </div>
            </div>

            <!-- Side-by-Side or Simulator Layout -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
                
                <!-- Card Visualizer Container -->
                <div class="lg:col-span-6 bg-slate-950/80 border border-slate-800 rounded-3xl p-6 relative overflow-hidden flex flex-col items-center justify-center min-h-[380px]">
                    <div class="text-xs text-slate-400 mb-4 font-mono self-start flex items-center gap-2">
                        <i class="fa-solid fa-laptop-code text-indigo-400"></i> Live Card Render Output:
                    </div>

                    <!-- THE PROFILE CARD (Swaps styles dynamically via JS) -->
                    <div id="sample-card-container" class="w-full max-w-sm bg-slate-900 border-2 border-slate-700 rounded-2xl p-5 shadow-2xl transition-all duration-300">
                        
                        <!-- Header with Avatar -->
                        <div class="flex items-center gap-4 mb-4">
                            <div class="relative w-14 h-14 shrink-0 rounded-full border-2 border-indigo-500/40 p-0.5 bg-slate-800">
                                <!-- Oversized image issue simulation -->
                                <img id="sample-card-img" src="https://images.unsplash.com/photo-1534528741775-53994a69daeb?w=150&auto=format&fit=crop&q=80" alt="Avatar" class="w-full h-full object-cover rounded-full">
                            </div>
                            <div>
                                <h4 class="font-bold text-white text-base leading-snug">Alex Morgan</h4>
                                <span class="text-xs text-slate-400">Senior UI Architect</span>
                            </div>
                        </div>

                        <!-- Bio Container with height constraint -->
                        <div id="sample-card-bio-box" class="h-24 bg-slate-800/80 rounded-xl p-3 border border-slate-700/60 transition-all">
                            <p id="sample-card-bio-text" class="text-xs text-slate-300 leading-relaxed">
                                Extremely passionate designer building high-performance scalable web systems. Specializing in responsive layouts, box-model dynamics, CSS grid architectures, and cross-browser overflow mitigation techniques.
                            </p>
                        </div>

                        <!-- Long unbroken URL section -->
                        <div class="mt-4 pt-3 border-t border-slate-800">
                            <span class="text-[10px] font-bold uppercase tracking-wider text-slate-400 block mb-1">Portfolio Link:</span>
                            <div id="sample-card-link-box" class="bg-slate-950 p-2.5 rounded-lg border border-slate-800">
                                <a id="sample-card-url" href="#" class="text-xs text-indigo-400 hover:underline">
                                    https://alexmorgan-design-portfolio-and-case-studies.io/projects/2026/overflow-fixing-demo-and-masterclass-submission
                                </a>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Fix Explanation & Code Solution -->
                <div class="lg:col-span-6 space-y-4">
                    <div class="bg-slate-800/60 border border-slate-700/80 rounded-2xl p-5 space-y-4">
                        <div class="flex items-center justify-between">
                            <h4 class="font-bold text-sm text-slate-100 flex items-center gap-2">
                                <i class="fa-solid fa-wrench text-indigo-400"></i> CSS Fix Breakdown
                            </h4>
                            <span class="text-xs text-indigo-400 font-mono">3 key CSS rules</span>
                        </div>

                        <!-- 3 Rules breakdown -->
                        <div class="space-y-3 text-xs">
                            <div class="bg-slate-900 p-3 rounded-xl border border-slate-800 flex items-start gap-3">
                                <span class="bg-indigo-600 text-white font-bold h-5 w-5 rounded-full flex items-center justify-center text-[10px] shrink-0 mt-0.5">1</span>
                                <div>
                                    <strong class="text-slate-200 block">Contain Long Unbroken Text / URLs</strong>
                                    <code class="font-mono text-emerald-400">overflow-wrap: break-word;</code> or <code class="font-mono text-emerald-400">word-break: break-all;</code> allows URLs to break lines cleanly inside containers instead of spilling past borders.
                                </div>
                            </div>

                            <div class="bg-slate-900 p-3 rounded-xl border border-slate-800 flex items-start gap-3">
                                <span class="bg-indigo-600 text-white font-bold h-5 w-5 rounded-full flex items-center justify-center text-[10px] shrink-0 mt-0.5">2</span>
                                <div>
                                    <strong class="text-slate-200 block">Manage Scrollable Container Heights</strong>
                                    Applying <code class="font-mono text-emerald-400">overflow: auto;</code> to fixed-height bio blocks provides vertical scrolling for lengthy text without corrupting the parent card height.
                                </div>
                            </div>

                            <div class="bg-slate-900 p-3 rounded-xl border border-slate-800 flex items-start gap-3">
                                <span class="bg-indigo-600 text-white font-bold h-5 w-5 rounded-full flex items-center justify-center text-[10px] shrink-0 mt-0.5">3</span>
                                <div>
                                    <strong class="text-slate-200 block">Media & Image Bounds</strong>
                                    Using <code class="font-mono text-emerald-400">max-width: 100%; object-fit: cover;</code> ensures responsive media clips perfectly within rounded borders.
                                </div>
                            </div>
                        </div>

                        <!-- Fix Code Snippet -->
                        <div class="space-y-1.5">
                            <span class="text-[11px] font-semibold text-slate-400 uppercase tracking-wider">Corrective CSS:</span>
                            <pre class="bg-slate-950 p-3.5 rounded-xl text-xs font-mono text-slate-300 border border-slate-800/80 overflow-x-auto">
<span class="text-indigo-400">.card-bio</span> {
  <span class="text-sky-300">height</span>: <span class="text-amber-300">96px</span>;
  <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">auto</span>; <span class="text-slate-500">/* Fix 1: Add dynamic scroll */</span>
}

<span class="text-indigo-400">.portfolio-link</span> {
  <span class="text-sky-300">overflow-wrap</span>: <span class="text-emerald-400">break-word</span>; <span class="text-slate-500">/* Fix 2: Break long URLs */</span>
  <span class="text-sky-300">text-overflow</span>: <span class="text-emerald-400">ellipsis</span>;
}</pre>
                        </div>
                    </div>
                </div>

            </div>
        </section>

        <!-- Submission & Code Export Section -->
        <section id="submission" class="bg-slate-800/80 border border-indigo-500/30 rounded-3xl p-6 sm:p-8 space-y-6 shadow-2xl">
            <div class="flex flex-col sm:flex-row justify-between sm:items-center gap-4 border-b border-slate-700/80 pb-5">
                <div>
                    <div class="text-indigo-400 text-xs font-bold uppercase tracking-wider">Submission Artifact</div>
                    <h3 class="text-xl sm:text-2xl font-bold text-white flex items-center gap-2">
                        <i class="fa-solid fa-file-code text-indigo-400"></i>
                        <span>Assignment Submission Code Export</span>
                    </h3>
                </div>
                
                <button onclick="copySubmissionCode()" class="bg-indigo-600 hover:bg-indigo-500 text-white font-semibold text-xs px-4 py-2.5 rounded-xl shadow-lg shadow-indigo-500/20 transition flex items-center gap-2">
                    <i id="copy-icon" class="fa-solid fa-copy"></i>
                    <span id="copy-btn-text">Copy Submission HTML/CSS</span>
                </button>
            </div>

            <!-- Code tabs -->
            <div class="space-y-4">
                <div class="flex items-center gap-2 border-b border-slate-700/60 pb-2">
                    <button class="px-3 py-1.5 rounded-lg text-xs font-semibold bg-indigo-600/20 text-indigo-300 border border-indigo-500/30">
                        Complete CSS Overflow Assignment HTML Document
                    </button>
                </div>

                <div class="relative">
                    <pre id="submission-code-block" class="bg-slate-950 p-5 rounded-2xl text-xs font-mono text-slate-300 border border-slate-800 overflow-x-auto max-h-[420px] custom-scrollbar leading-relaxed">
<span class="text-slate-500">&lt;!-- Assignment 6.3 — Overflow & Layout Fixing Submission --&gt;</span>
&lt;<span class="text-indigo-400">html</span> lang="en"&gt;
&lt;<span class="text-indigo-400">head</span>&gt;
  &lt;<span class="text-indigo-400">style</span>&gt;
    <span class="text-slate-500">/* Step 1 & 2: Fixed Height Container with Overflowing Text */</span>
    <span class="text-indigo-300">.fixed-box</span> {
      <span class="text-sky-300">width</span>: <span class="text-amber-300">280px</span>;
      <span class="text-sky-300">height</span>: <span class="text-amber-300">160px</span>;
      <span class="text-sky-300">border</span>: <span class="text-amber-300">2px solid #4f46e5</span>;
      <span class="text-sky-300">padding</span>: <span class="text-amber-300">12px</span>;
      <span class="text-sky-300">margin-bottom</span>: <span class="text-amber-300">20px</span>;
    }

    <span class="text-slate-500">/* Step 3: Demonstrating 4 Overflow Values */</span>
    <span class="text-indigo-300">.demo-visible</span> { <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">visible</span>; }
    <span class="text-indigo-300">.demo-hidden</span>  { <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">hidden</span>; }
    <span class="text-indigo-300">.demo-auto</span>    { <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">auto</span>; }
    <span class="text-indigo-300">.demo-scroll</span>  { <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">scroll</span>; }

    <span class="text-slate-500">/* Step 4: Dedicated auto container with custom scrollbar */</span>
    <span class="text-indigo-300">.dedicated-auto-box</span> {
      <span class="text-sky-300">width</span>: <span class="text-amber-300">100%</span>;
      <span class="text-sky-300">height</span>: <span class="text-amber-300">200px</span>;
      <span class="text-sky-300">overflow</span>: <span class="text-emerald-400">auto</span>;
      <span class="text-sky-300">border</span>: <span class="text-amber-300">2px solid #10b981</span>;
      <span class="text-sky-300">border-radius</span>: <span class="text-amber-300">12px</span>;
    }

    <span class="text-slate-500">/* Step 5: Layout Fix for unbroken text & card overflow */</span>
    <span class="text-indigo-300">.fixed-card-link</span> {
      <span class="text-sky-300">overflow-wrap</span>: <span class="text-emerald-400">break-word</span>;
      <span class="text-sky-300">word-break</span>: <span class="text-emerald-400">break-all</span>;
    }
  &lt;/<span class="text-indigo-400">style</span>&gt;
&lt;/<span class="text-indigo-400">head</span>&gt;
&lt;<span class="text-indigo-400">body</span>&gt;
  &lt;<span class="text-indigo-400">h1</span>&gt;Assignment 6.3 - Overflow Showcase&lt;/<span class="text-indigo-400">h1</span>&gt;

  <span class="text-slate-500">&lt;!-- Step 3 Demo Boxes --&gt;</span>
  &lt;<span class="text-indigo-400">div</span> class="fixed-box demo-visible"&gt;Visible Content...&lt;/<span class="text-indigo-400">div</span>&gt;
  &lt;<span class="text-indigo-400">div</span> class="fixed-box demo-hidden"&gt;Clipped Content...&lt;/<span class="text-indigo-400">div</span>&gt;
  &lt;<span class="text-indigo-400">div</span> class="fixed-box demo-auto"&gt;Auto Scrollbar...&lt;/<span class="text-indigo-400">div</span>&gt;
  &lt;<span class="text-indigo-400">div</span> class="fixed-box demo-scroll"&gt;Static Scrollbar...&lt;/<span class="text-indigo-400">div</span>&gt;

  <span class="text-slate-500">&lt;!-- Step 4 Container --&gt;</span>
  &lt;<span class="text-indigo-400">div</span> class="dedicated-auto-box"&gt;Scrollable Auto Content...&lt;/<span class="text-indigo-400">div</span>&gt;
&lt;/<span class="text-indigo-400">body</span>&gt;
&lt;/<span class="text-indigo-400">html</span>&gt;</pre>
                </div>
            </div>
        </section>
    </main>

    <!-- Footer -->
    <footer class="border-t border-slate-800 bg-slate-950 py-6 text-center text-xs text-slate-500">
        <div class="max-w-7xl mx-auto px-4 flex flex-col sm:flex-row items-center justify-between gap-3">
            <span>Assignment 6.3 — Overflow & Layout Fixing Interactive Submission</span>
            <span>Built for Web Development Curriculum</span>
        </div>
    </footer>

    <!-- Notification Toast for Copy -->
    <div id="toast" class="fixed bottom-5 right-5 bg-emerald-500 text-slate-950 font-bold text-xs px-4 py-3 rounded-xl shadow-2xl transition-all duration-300 transform translate-y-20 opacity-0 flex items-center gap-2 z-50">
        <i class="fa-solid fa-circle-check"></i>
        <span>Code copied to clipboard! Ready for submission.</span>
    </div>

    <!-- JavaScript Interactive Logic -->
    <script>
        // Track state for dedicated auto box content toggle
        let isLongAutoContent = true;

        // Toggle global overflow view filter in step 1-3 section
        function setGlobalOverflow(prop) {
            const cards = document.querySelectorAll('.card-overflow-item');
            const buttons = document.querySelectorAll('.overflow-tab-btn');

            // Reset buttons
            buttons.forEach(btn => {
                btn.classList.remove('bg-indigo-600', 'text-white');
                btn.classList.add('text-slate-400');
            });

            // Highlight active button
            const activeBtn = document.getElementById(`btn-${prop}`);
            if (activeBtn) {
                activeBtn.classList.add('bg-indigo-600', 'text-white');
                activeBtn.classList.remove('text-slate-400');
            }

            // Filter grid display
            cards.forEach(card => {
                if (prop === 'all' || card.dataset.prop === prop) {
                    card.style.display = 'flex';
                } else {
                    card.style.display = 'none';
                }
            });
        }

        // Toggle short vs long text inside Step 4 dedicated auto box
        function toggleAutoContentLength() {
            const textBox = document.getElementById('dedicated-auto-text');
            const statusText = document.getElementById('scroll-status-text');
            
            if (isLongAutoContent) {
                textBox.innerHTML = `
                    <p>
                        This is a concise paragraph of text inside the fixed height container (220px).
                    </p>
                    <p class="text-emerald-400 font-medium">
                        Notice how with <code class="font-mono bg-slate-800 px-1 py-0.5 rounded">overflow: auto</code>, when the content fits inside the container height, the browser automatically hides the vertical scrollbars, keeping the card UI clean!
                    </p>
                `;
                statusText.innerText = "Content fits within 220px height; scrollbar automatically hidden.";
                isLongAutoContent = false;
            } else {
                textBox.innerHTML = `
                    <p>
                        The CSS Box Model forms the foundation of all web layout architecture. Every element rendered on a webpage is a rectangular box comprising margins, borders, padding, and the actual content height and width.
                    </p>
                    <p>
                        When explicit <code class="font-mono text-indigo-300">height</code> constraints are declared on a container (such as this 220px tall component), any content surpassing that dimension is forced into an overflow condition.
                    </p>
                    <p>
                        By configuring <code class="font-mono text-emerald-400">overflow: auto</code>, we instruct the browser engine to dynamically evaluate the content box height. If the content height exceeds 220px, scrollbars are synthesized automatically to grant full accessibility to hidden text without compromising page structure.
                    </p>
                    <p>
                        Furthermore, custom vendor scrollbar styling can be attached via pseudo-elements like <code class="font-mono text-indigo-300">::-webkit-scrollbar</code>, granting full visual alignment with sleek dark-mode UI designs.
                    </p>
                `;
                statusText.innerText = "Scrollbar currently active due to excess text.";
                isLongAutoContent = true;
            }
        }

        // Scroll progress tracker for step 4 box
        const dedicatedAutoBox = document.getElementById('dedicated-auto-box');
        const scrollPercentage = document.getElementById('scroll-percentage');
        
        dedicatedAutoBox.addEventListener('scroll', () => {
            const scrollTop = dedicatedAutoBox.scrollTop;
            const scrollHeight = dedicatedAutoBox.scrollHeight - dedicatedAutoBox.clientHeight;
            const pct = scrollHeight > 0 ? Math.round((scrollTop / scrollHeight) * 100) : 0;
            scrollPercentage.innerText = `Scroll Y: ${pct}%`;
        });

        // Step 5 Interactive Layout Fix Simulator
        function setFixState(state) {
            const cardBioBox = document.getElementById('sample-card-bio-box');
            const cardBioText = document.getElementById('sample-card-bio-text');
            const cardUrl = document.getElementById('sample-card-url');
            const cardContainer = document.getElementById('sample-card-container');
            
            const btnBroken = document.getElementById('btn-show-broken');
            const btnFixed = document.getElementById('btn-show-fixed');

            const diagBox = document.getElementById('diagnosis-box');
            const diagTitle = document.getElementById('diagnosis-title');
            const diagDesc = document.getElementById('diagnosis-desc');
            const diagBadge = document.getElementById('diagnosis-badge');
            const diagIcon = document.getElementById('diagnosis-icon');

            if (state === 'broken') {
                // Apply broken styles
                cardBioBox.className = 'h-16 bg-slate-800/80 rounded-xl p-3 border border-slate-700/60 overflow-visible';
                cardBioText.className = 'text-xs text-slate-300 leading-relaxed';
                cardUrl.style.wordBreak = 'normal';
                cardUrl.style.overflowWrap = 'normal';
                cardUrl.className = 'text-xs text-indigo-400 inline-block whitespace-nowrap';
                cardContainer.className = 'w-full max-w-sm bg-slate-900 border-2 border-rose-500/80 rounded-2xl p-5 shadow-2xl transition-all duration-300';

                // Update Diagnosis Box UI
                diagBox.className = 'bg-rose-950/30 border border-rose-500/30 rounded-2xl p-4 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4';
                diagTitle.innerText = 'Issue Identified: Card Layout Overflow & Destruction';
                diagDesc.innerText = 'Unbroken URL string overflows the card width rightwards; Bio text overflows past the fixed height (16px box) into lower elements.';
                diagBadge.className = 'shrink-0 px-3 py-1 rounded-full bg-rose-500/20 text-rose-300 font-mono text-xs font-semibold border border-rose-500/30';
                diagBadge.innerText = 'STATUS: BROKEN (OVERFLOW VISIBLE)';
                diagIcon.className = 'fa-solid fa-triangle-exclamation text-rose-400';

                // Buttons UI
                btnBroken.className = 'px-4 py-2 rounded-lg text-xs font-bold transition bg-rose-600 text-white flex items-center gap-2';
                btnFixed.className = 'px-4 py-2 rounded-lg text-xs font-bold transition text-slate-400 hover:text-white flex items-center gap-2';
            } else {
                // Apply fixed styles
                cardBioBox.className = 'h-24 bg-slate-800/80 rounded-xl p-3 border border-slate-700/60 overflow-auto custom-scrollbar';
                cardBioText.className = 'text-xs text-slate-300 leading-relaxed';
                cardUrl.style.wordBreak = 'break-all';
                cardUrl.style.overflowWrap = 'break-word';
                cardUrl.className = 'text-xs text-indigo-400 hover:underline block';
                cardContainer.className = 'w-full max-w-sm bg-slate-900 border-2 border-emerald-500/80 rounded-2xl p-5 shadow-2xl transition-all duration-300';

                // Update Diagnosis Box UI
                diagBox.className = 'bg-emerald-950/30 border border-emerald-500/30 rounded-2xl p-4 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4';
                diagTitle.innerText = 'Layout Resolved: Correct Overflow Rules Applied';
                diagDesc.innerText = 'overflow: auto adds a clean vertical scroll to bio text; word-break: break-all breaks long URL strings neatly within boundaries.';
                diagBadge.className = 'shrink-0 px-3 py-1 rounded-full bg-emerald-500/20 text-emerald-300 font-mono text-xs font-semibold border border-emerald-500/30';
                diagBadge.innerText = 'STATUS: FIXED (OVERFLOW CONTROLLED)';
                diagIcon.className = 'fa-solid fa-circle-check text-emerald-400';

                // Buttons UI
                btnFixed.className = 'px-4 py-2 rounded-lg text-xs font-bold transition bg-emerald-600 text-white flex items-center gap-2';
                btnBroken.className = 'px-4 py-2 rounded-lg text-xs font-bold transition text-slate-400 hover:text-white flex items-center gap-2';
            }
        }

        // Copy Code Functionality
        function copySubmissionCode() {
            const rawCode = `<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Assignment 6.3 - Overflow & Layout Fixing</title>
  <style>
    /* Step 1 & 2: Container with fixed height and width */
    .overflow-container {
      width: 300px;
      height: 150px;
      border: 2px solid #4f46e5;
      padding: 12px;
      margin-bottom: 20px;
    }

    /* Step 3: 4 Overflow Properties */
    .visible-box { overflow: visible; }
    .hidden-box  { overflow: hidden;  }
    .auto-box    { overflow: auto;    }
    .scroll-box  { overflow: scroll;  }

    /* Step 4: Dedicated auto box with customized scrollbar */
    .dedicated-scroll-box {
      width: 100%;
      max-width: 500px;
      height: 200px;
      overflow: auto;
      border: 2px solid #10b981;
      border-radius: 8px;
      padding: 16px;
    }

    /* Step 5: Layout fixing rule for breaking long text overflow */
    .fixed-url {
      overflow-wrap: break-word;
      word-break: break-all;
    }
  </style>
</head>
<body>
  <h1>Assignment 6.3 Submission</h1>
  
  <h2>Step 3: Overflow Property Demonstrations</h2>
  <div class="overflow-container visible-box">
    <strong>Visible:</strong> Cascading Style Sheets allow developers to format layout structures...
  </div>
  
  <div class="overflow-container hidden-box">
    <strong>Hidden:</strong> Cascading Style Sheets allow developers to format layout structures...
  </div>
  
  <div class="overflow-container auto-box">
    <strong>Auto:</strong> Cascading Style Sheets allow developers to format layout structures...
  </div>
  
  <div class="overflow-container scroll-box">
    <strong>Scroll:</strong> Cascading Style Sheets allow developers to format layout structures...
  </div>

  <h2>Step 4: Dedicated Auto Scrollable Box</h2>
  <div class="dedicated-scroll-box">
    <p>This box demonstrates overflow: auto. Scrollbars render dynamically whenever text exceeds 200px.</p>
  </div>
</body>
</html>`;

            // Standard ExecCommand copy fallback for safe sandbox execution
            const dummy = document.createElement("textarea");
            document.body.appendChild(dummy);
            dummy.value = rawCode;
            dummy.select();
            document.execCommand("copy");
            document.body.removeChild(dummy);

            // Toast UI feedback
            const toast = document.getElementById('toast');
            toast.classList.remove('translate-y-20', 'opacity-0');
            toast.classList.add('translate-y-0', 'opacity-100');

            setTimeout(() => {
                toast.classList.remove('translate-y-0', 'opacity-100');
                toast.classList.add('translate-y-20', 'opacity-0');
            }, 3000);
        }
    </script>
</body>
</html>

Key Features Included:
Interactive Overflow Testbench (Steps 1–3): Side-by-side comparative cards with live toggle filters for overflow: visible, overflow: hidden, overflow: auto, and overflow: scroll operating on fixed height: 160px containers containing overflowing text.

Dedicated overflow: auto Showcase (Step 4): A featured interactive component with dynamic scroll percentage tracking, custom WebKit scrollbar styling, and a content length toggle to demonstrate dynamic scrollbar behavior.

Layout Issue Diagnosis & Repair Simulator (Step 5): An interactive simulator demonstrating a broken card layout caused by unhandled long URL text and bio overflow, with a live toggle to show the corrected, clean layout using overflow-wrap: break-word and overflow: auto.

Submission & Code Export Section: Formatted code snippets ready to copy or submit directly for assignment cred