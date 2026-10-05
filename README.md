# Student-s-Study-Desk

<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Study desk</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Atkinson+Hyperlegible:wght@400;700&family=Sora:wght@600;800&display=swap" rel="stylesheet">
<style>
:root {
  box-sizing: border-box;
  padding-top: env(safe-area-inset-top, 0px);
  padding-bottom: env(safe-area-inset-bottom, 0px);
  color-scheme: light dark;
  --bg: #f4f5fa;
  --surface: #ffffff;
  --field: #ffffff;
  --ink: #171a2b;
  --muted: #565b76;
  --line: #d8dbea;
  --edge: #858aa6;
  --danger: #b42318;
  --ok: #1a7f4b;
}
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --bg: #12131a;
    --surface: #1c1e29;
    --field: #12131a;
    --ink: #eceef8;
    --muted: #a3a8c3;
    --line: #343850;
    --edge: #6c7190;
    --danger: #ff8a80;
    --ok: #6dd39b;
  }
}
:root[data-theme="dark"] {
  --bg: #12131a;
  --surface: #1c1e29;
  --field: #12131a;
  --ink: #eceef8;
  --muted: #a3a8c3;
  --line: #343850;
  --edge: #6c7190;
  --danger: #ff8a80;
  --ok: #6dd39b;
}
html { scroll-padding-top: env(safe-area-inset-top, 0px); }
*, *::before, *::after { box-sizing: inherit; }
[hidden] { display: none !important; }

body {
  margin: 0;
  background: var(--bg);
  color: var(--ink);
  font-family: "Atkinson Hyperlegible", system-ui, -apple-system, "Segoe UI", Arial, sans-serif;
  font-size: 1.0625rem;
  line-height: 1.5;
}
h1, h2, h3, .display { font-family: "Sora", "Atkinson Hyperlegible", system-ui, sans-serif; }
button, input, select { font: inherit; color: inherit; }
:focus-visible { outline: 3px solid var(--ink); outline-offset: 2px; }
.sr-only {
  position: absolute; width: 1px; height: 1px; overflow: hidden;
  clip: rect(0 0 0 0); white-space: nowrap;
}

/* Each tool has its own colour, like tabs in a binder */
[data-area="focus"]  { --accent: #e5484d; --on: #ffffff; }
[data-area="work"]   { --accent: #3e63dd; --on: #ffffff; }
[data-area="schedule"] { --accent: #218358; --on: #ffffff; }
[data-area="cards"]  { --accent: #f5b72e; --on: #1a1a1a; }

.wrap { max-width: 780px; margin: 0 auto; padding: 40px 20px 56px; }

header h1 {
  margin: 0;
  font-size: clamp(2.2rem, 7vw, 3.4rem);
  font-weight: 800;
  line-height: 1.05;
  letter-spacing: -0.03em;
}
header p { margin: 10px 0 28px; max-width: 52ch; color: var(--muted); }

/* ---------- Tabs ---------- */
[role="tablist"] {
  display: flex; gap: 6px;
  padding: 0 12px;
  overflow-x: auto;
  margin-bottom: -1px;
}
[role="tab"] {
  flex: none;
  position: relative;
  padding: 12px 18px 10px;
  background: transparent;
  border: 1px solid var(--line);
  border-top: 5px solid var(--accent);
  border-radius: 10px 10px 0 0;
  color: var(--muted);
  font-weight: 700;
  cursor: pointer;
}
[role="tab"]:hover { color: var(--ink); }
[role="tab"][aria-selected="true"] {
  background: var(--surface);
  color: var(--ink);
  border-bottom-color: var(--surface);
  z-index: 1;
}

.panel {
  background: var(--surface);
  border: 1px solid var(--line);
  border-radius: 12px;
  padding: 28px;
}
.panel h2 { margin: 0 0 4px; font-size: 1.4rem; letter-spacing: -0.01em; }
.panel h3 { margin: 32px 0 4px; font-size: 1.1rem; }
.hint { margin: 0 0 20px; color: var(--muted); max-width: 60ch; }

/* ---------- Controls ---------- */
.btn {
  padding: 11px 20px;
  background: var(--accent);
  color: var(--on);
  border: 2px solid var(--accent);
  border-radius: 8px;
  font-weight: 700;
  cursor: pointer;
}
.btn:hover { filter: brightness(0.93); }
.btn.quiet {
  background: transparent;
  color: var(--ink);
  border-color: var(--edge);
}
.btn.quiet:hover { background: var(--bg); filter: none; }
.link-btn {
  padding: 4px 2px;
  background: none; border: 0;
  color: var(--muted);
  cursor: pointer;
  text-decoration: underline;
}
.link-btn:hover { color: var(--danger); }

input[type="text"], input[type="number"], input[type="date"], select {
  width: 100%;
  min-width: 0;
  padding: 10px 12px;
  background: var(--field);
  border: 1.5px solid var(--edge);
  border-radius: 8px;
}
input[type="checkbox"] { width: 22px; height: 22px; accent-color: var(--accent); flex: none; cursor: pointer; }

.field { display: flex; flex-direction: column; gap: 6px; font-weight: 700; font-size: 0.92rem; min-width: 0; }
.form-row { display: flex; flex-wrap: wrap; gap: 12px; align-items: flex-end; }
.form-row .grow { flex: 2 1 200px; }
.form-row .mid { flex: 1 1 140px; }

.empty { margin: 20px 0 0; color: var(--muted); }
.msg { min-height: 1.5em; margin: 12px 0 0; font-weight: 700; }

/* ---------- Focus timer ---------- */
.timer { display: flex; flex-wrap: wrap; gap: 28px 40px; align-items: center; margin-top: 8px; }
.ring { position: relative; width: 220px; height: 220px; flex: none; }
.ring svg { width: 100%; height: 100%; transform: rotate(-90deg); }
.ring circle { fill: none; stroke-width: 10; }
.ring .track { stroke: var(--line); }
.ring .bar { stroke: var(--accent); stroke-linecap: round; transition: stroke-dashoffset 0.25s linear; }
.ring .readout {
  position: absolute; inset: 0;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
}
.readout .display { font-size: 3.2rem; font-weight: 800; letter-spacing: -0.03em; font-variant-numeric: tabular-nums; line-height: 1; }
.readout span { margin-top: 6px; color: var(--muted); font-weight: 700; }
.timer-side { display: flex; flex-direction: column; gap: 18px; flex: 1 1 240px; }
.seg { display: flex; flex-wrap: wrap; gap: 8px; }
.seg button {
  padding: 8px 14px;
  background: transparent;
  border: 2px solid var(--edge);
  border-radius: 999px;
  font-weight: 700;
  cursor: pointer;
}
.seg button[aria-pressed="true"] { background: var(--accent); border-color: var(--accent); color: var(--on); }
.actions { display: flex; gap: 10px; flex-wrap: wrap; }
.length { max-width: 200px; }
.stat { margin: 0; color: var(--muted); }
.stat strong { color: var(--ink); }

/* ---------- Assignments ---------- */
#a-list { list-style: none; margin: 24px 0 0; padding: 0; border-top: 1px solid var(--line); }
#a-list li { display: flex; align-items: center; gap: 14px; padding: 14px 0; border-bottom: 1px solid var(--line); }
.a-body { flex: 1; min-width: 0; }
.a-title { overflow-wrap: anywhere; font-weight: 700; }
.a-meta { font-size: 0.92rem; color: var(--muted); }
.a-meta.late { color: var(--danger); font-weight: 700; }
li.done .a-title { text-decoration: line-through; color: var(--muted); font-weight: 400; }

/* ---------- Schedule ---------- */
fieldset.days { border: 0; margin: 18px 0; padding: 0; min-width: 0; }
.days legend { padding: 0; margin-bottom: 8px; font-weight: 700; font-size: 0.92rem; }
.chips { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 8px; }
.chip { position: relative; }
.chip input { position: absolute; inset: 0; width: 100%; height: 100%; margin: 0; opacity: 0; cursor: pointer; }
.chip span { display: block; padding: 8px 14px; border: 2px solid var(--edge); border-radius: 999px; font-weight: 700; }
.chip input:checked + span { background: var(--accent); border-color: var(--accent); color: var(--on); }
.chip input:checked + span::before { content: "\2713\00a0"; }
.chip input:focus-visible + span { outline: 3px solid var(--ink); outline-offset: 2px; }
.link-btn.plain:hover { color: var(--ink); }
.now {
  margin: 18px 0 0;
  padding: 14px 16px;
  border-left: 6px solid var(--accent);
  background: var(--bg);
  border-radius: 0 8px 8px 0;
  font-weight: 700;
}
.day { margin-top: 24px; }
.day.today { border-left: 6px solid var(--accent); padding-left: 14px; }
.day h3 { margin: 0 0 6px; font-size: 1.05rem; display: flex; gap: 10px; align-items: baseline; }
.day .tag { padding: 1px 10px; border-radius: 999px; background: var(--accent); color: var(--on); font-family: "Atkinson Hyperlegible", system-ui, sans-serif; font-size: 0.85rem; }
.day ul { list-style: none; margin: 0; padding: 0; border-top: 1px solid var(--line); }
.day li { display: flex; gap: 14px; align-items: baseline; padding: 10px 0; border-bottom: 1px solid var(--line); }
.s-time { flex: none; width: 11rem; font-variant-numeric: tabular-nums; color: var(--muted); }
.s-main { flex: 1; min-width: 0; overflow-wrap: anywhere; }
.s-place { color: var(--muted); font-size: 0.92rem; }
.free { margin: 0; padding: 10px 0; color: var(--muted); border-top: 1px solid var(--line); }

/* ---------- Flashcards ---------- */
.stage { margin-top: 24px; }
.card { perspective: 1000px; width: 100%; height: 230px; padding: 0; background: none; border: 0; cursor: pointer; display: block; }
.card .inner { display: block; position: relative; width: 100%; height: 100%; transform-style: preserve-3d; transition: transform 0.45s ease; }
.card.flipped .inner { transform: rotateY(180deg); }
.face {
  position: absolute; inset: 0;
  display: flex; align-items: center; justify-content: center;
  padding: 24px;
  text-align: center;
  font-size: 1.4rem;
  overflow: auto;
  border: 2px solid var(--ink);
  border-radius: 12px;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  overflow-wrap: anywhere;
}
.face.front { background: var(--surface); }
.face.back { background: var(--accent); color: var(--on); transform: rotateY(180deg); font-weight: 700; }
.face small { position: absolute; top: 10px; left: 14px; font-size: 0.8rem; font-weight: 700; opacity: 0.75; }
.pager { display: flex; flex-wrap: wrap; gap: 10px; align-items: center; margin-top: 14px; }
.pager .count { margin-right: auto; color: var(--muted); font-weight: 700; }
#c-list { list-style: none; margin: 28px 0 0; padding: 0; border-top: 1px solid var(--line); }
#c-list li { display: flex; gap: 14px; align-items: baseline; padding: 10px 0; border-bottom: 1px solid var(--line); }
.c-term { flex: 1; font-weight: 700; overflow-wrap: anywhere; }
.c-def { flex: 2; color: var(--muted); overflow-wrap: anywhere; }

/* ---------- Relax game ---------- */
[data-area="calm"] { --accent: #0e8174; --on: #ffffff; }
.ttt-wrap {
  display: grid; gap: 18px; justify-items: center; margin-top: 10px;
}
.ttt-board {
  display: grid; grid-template-columns: repeat(3, minmax(72px, 1fr));
  gap: 10px; width: min(100%, 300px); aspect-ratio: 1;
  padding: 10px; border-radius: 18px; background: var(--bg); border: 2px solid var(--line);
}
.ttt-cell {
  border: 2px solid var(--edge); border-radius: 14px; background: var(--surface);
  color: var(--ink); font-size: clamp(2rem, 7vw, 3.2rem); font-weight: 800;
  cursor: pointer; transition: transform 0.15s ease, border-color 0.15s ease;
}
.ttt-cell:hover:not(:disabled) {
  border-color: var(--accent); transform: translateY(-1px);
}
.ttt-cell:disabled {
  cursor: default; color: var(--ink);
}
.ttt-controls {
  display: flex; flex-wrap: wrap; align-items: center; justify-content: center; gap: 12px;
}
.ttt-status { margin: 0; font-weight: 700; }

footer { margin-top: 20px; color: var(--muted); font-size: 0.92rem; }

@media (max-width: 520px) {
  .wrap { padding-top: 28px; }
  .panel { padding: 20px 16px; }
  .day li { flex-direction: column; gap: 2px; }
  .s-time { width: auto; }
  .face { font-size: 1.15rem; }
  #c-list li { flex-direction: column; gap: 2px; }
}
@media (prefers-reduced-motion: reduce) {
  .card .inner, .ring .bar { transition: none; }
}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <h1>Study desk</h1>
    <p>A focus timer, assignment list, class schedule, and flashcards in one place.</p>
  </header>

  <div role="tablist" aria-label="Study tools">
    <button role="tab" id="tab-focus" data-area="focus" aria-selected="true" aria-controls="panel-focus">Focus</button>
    <button role="tab" id="tab-work" data-area="work" aria-selected="false" aria-controls="panel-work" tabindex="-1">Assignments</button>
    <button role="tab" id="tab-schedule" data-area="schedule" aria-selected="false" aria-controls="panel-schedule" tabindex="-1">Schedule</button>
    <button role="tab" id="tab-cards" data-area="cards" aria-selected="false" aria-controls="panel-cards" tabindex="-1">Flashcards</button>
    <button role="tab" id="tab-calm" data-area="calm" aria-selected="false" aria-controls="panel-calm" tabindex="-1">Relax</button>
  </div>

  <!-- ===== Focus ===== -->
  <section class="panel" id="panel-focus" data-area="focus" role="tabpanel" aria-labelledby="tab-focus">
    <h2>Focus timer</h2>
    <p class="hint">Work in short, timed blocks and rest in between. Pick a mode, then press Start.</p>
    <div class="timer">
      <div class="ring" role="timer" aria-label="Time remaining">
        <svg viewBox="0 0 220 220" aria-hidden="true">
          <circle class="track" cx="110" cy="110" r="100"></circle>
          <circle class="bar" id="ring-bar" cx="110" cy="110" r="100"></circle>
        </svg>
        <div class="readout">
          <div class="display" id="time">25:00</div>
          <span id="mode-label">Focus</span>
        </div>
      </div>
      <div class="timer-side">
        <div class="seg" role="group" aria-label="Timer mode">
          <button type="button" data-mode="focus" aria-pressed="true">Focus</button>
          <button type="button" data-mode="short" aria-pressed="false">Short break</button>
          <button type="button" data-mode="long" aria-pressed="false">Long break</button>
        </div>
        <div class="actions">
          <button type="button" class="btn" id="t-start">Start</button>
          <button type="button" class="btn quiet" id="t-reset">Reset</button>
        </div>
        <label class="field length">Focus length (minutes)
          <input type="number" id="focus-min" min="1" max="120" value="25" inputmode="numeric">
        </label>
        <p class="stat">Focus sessions finished today: <strong id="sessions">0</strong></p>
      </div>
    </div>
    <p class="msg" id="t-msg" role="status" aria-live="polite"></p>
  </section>

  <!-- ===== Assignments ===== -->
  <section class="panel" id="panel-work" data-area="work" role="tabpanel" aria-labelledby="tab-work" hidden>
    <h2>Assignments</h2>
    <p class="hint" id="a-summary">Add what's due and the list sorts itself by date.</p>
    <div class="form-row">
      <label class="field grow">Assignment
        <input type="text" id="a-title" maxlength="120" autocomplete="off">
      </label>
      <label class="field mid">Course (optional)
        <input type="text" id="a-course" maxlength="40" autocomplete="off">
      </label>
      <label class="field mid">Due date
        <input type="date" id="a-due">
      </label>
      <button type="button" class="btn" id="a-add">Add assignment</button>
    </div>
    <p class="msg" id="a-msg" role="alert"></p>
    <ul id="a-list"></ul>
    <p class="empty" id="a-empty">No assignments yet. Add one above to see what's due first.</p>
  </section>

  <!-- ===== Schedule ===== -->
  <section class="panel" id="panel-schedule" data-area="schedule" role="tabpanel" aria-labelledby="tab-schedule" hidden>
    <h2>Class schedule</h2>
    <p class="hint">Add each subject once and pick the days it meets. Your week builds itself.</p>
    <div class="form-row">
      <label class="field grow">Subject
        <input type="text" id="s-subject" maxlength="40" autocomplete="off">
      </label>
      <label class="field mid">Room or teacher (optional)
        <input type="text" id="s-place" maxlength="40" autocomplete="off">
      </label>
    </div>
    <fieldset class="days">
      <legend>Days</legend>
      <div class="chips" id="s-days">
        <label class="chip"><input type="checkbox" value="0"><span>Mon</span></label>
        <label class="chip"><input type="checkbox" value="1"><span>Tue</span></label>
        <label class="chip"><input type="checkbox" value="2"><span>Wed</span></label>
        <label class="chip"><input type="checkbox" value="3"><span>Thu</span></label>
        <label class="chip"><input type="checkbox" value="4"><span>Fri</span></label>
        <label class="chip"><input type="checkbox" value="5"><span>Sat</span></label>
        <label class="chip"><input type="checkbox" value="6"><span>Sun</span></label>
      </div>
      <button type="button" class="link-btn plain" id="s-weekdays">Select Monday to Friday</button>
    </fieldset>
    <div class="form-row">
      <label class="field mid">Starts
        <input type="time" id="s-start">
      </label>
      <label class="field mid">Ends
        <input type="time" id="s-end">
      </label>
      <button type="button" class="btn" id="s-add">Add class</button>
    </div>
    <p class="msg" id="s-msg" role="alert"></p>
    <div class="now" id="s-now" role="status" hidden></div>
    <div id="s-week"></div>
    <p class="empty" id="s-empty">No classes yet. Add your first subject above to build your week.</p>
  </section>

  <!-- ===== Flashcards ===== -->
  <section class="panel" id="panel-cards" data-area="cards" role="tabpanel" aria-labelledby="tab-cards" hidden>
    <h2>Flashcards</h2>
    <p class="hint">Add a term and its answer, then test yourself. Click the card to flip it.</p>
    <div class="form-row">
      <label class="field mid">Term or question
        <input type="text" id="c-front" maxlength="200" autocomplete="off">
      </label>
      <label class="field grow">Answer
        <input type="text" id="c-back" maxlength="300" autocomplete="off">
      </label>
      <button type="button" class="btn" id="c-add">Add card</button>
    </div>
    <p class="msg" id="c-msg" role="alert"></p>

    <div class="stage" id="c-stage" hidden>
      <button type="button" class="card" id="card">
        <span class="inner">
          <span class="face front" id="face-front"></span>
          <span class="face back" id="face-back"></span>
        </span>
      </button>
      <div class="sr-only" id="c-live" aria-live="polite"></div>
      <div class="pager">
        <span class="count" id="c-count"></span>
        <button type="button" class="btn quiet" id="c-prev">Previous</button>
        <button type="button" class="btn quiet" id="c-next">Next</button>
        <button type="button" class="btn quiet" id="c-shuffle">Shuffle</button>
      </div>
    </div>
    <p class="empty" id="c-empty">No cards yet. Add a term and its answer to start studying.</p>
    <ul id="c-list"></ul>
  </section>

  <!-- ===== Relax game ===== -->
  <section class="panel" id="panel-calm" data-area="calm" role="tabpanel" aria-labelledby="tab-calm" hidden>
    <h2>Tic-Tac-Toe</h2>
    <p class="hint">Take a quick mental reset. Play a short round of tic-tac-toe before going back to your next study task.</p>
    <div class="ttt-wrap">
      <div class="ttt-board" id="ttt-board" aria-label="Tic-tac-toe board">
        <button type="button" class="ttt-cell" data-index="0" aria-label="Cell 1"></button>
        <button type="button" class="ttt-cell" data-index="1" aria-label="Cell 2"></button>
        <button type="button" class="ttt-cell" data-index="2" aria-label="Cell 3"></button>
        <button type="button" class="ttt-cell" data-index="3" aria-label="Cell 4"></button>
        <button type="button" class="ttt-cell" data-index="4" aria-label="Cell 5"></button>
        <button type="button" class="ttt-cell" data-index="5" aria-label="Cell 6"></button>
        <button type="button" class="ttt-cell" data-index="6" aria-label="Cell 7"></button>
        <button type="button" class="ttt-cell" data-index="7" aria-label="Cell 8"></button>
        <button type="button" class="ttt-cell" data-index="8" aria-label="Cell 9"></button>
      </div>
      <div class="ttt-controls">
        <p class="ttt-status">Turn: <strong id="game-turn">X</strong></p>
        <button type="button" class="btn quiet" id="game-reset">New round</button>
      </div>
      <p class="msg" id="game-msg" role="status" aria-live="polite">Player X starts.</p>
    </div>
  </section>

  <footer>Everything you enter is saved in this browser only, on this device.</footer>
</div>

<script>
(() => {
  "use strict";

  /* ---------- helpers ---------- */
  const $ = (sel) => document.querySelector(sel);

  // Saved data lives in localStorage; fall back to memory if storage is blocked.
  const store = {
    mem: {},
    get(key, fallback) {
      try {
        const raw = localStorage.getItem("studydesk:" + key);
        return raw === null ? fallback : JSON.parse(raw);
      } catch (e) {
        return key in this.mem ? this.mem[key] : fallback;
      }
    },
    set(key, value) {
      this.mem[key] = value;
      try { localStorage.setItem("studydesk:" + key, JSON.stringify(value)); } catch (e) { /* ignore */ }
    }
  };

  // Build DOM nodes without innerHTML so typed text can never run as code.
  function el(tag, props = {}, ...kids) {
    const n = document.createElement(tag);
    for (const [k, v] of Object.entries(props)) {
      if (k === "class") n.className = v;
      else if (k === "text") n.textContent = v;
      else n.setAttribute(k, v);
    }
    kids.flat().forEach((c) => n.append(c));
    return n;
  }
  const uid = () => Date.now().toString(36) + Math.random().toString(36).slice(2, 7);
  const num = (v) => { const n = parseFloat(v); return Number.isFinite(n) ? n : NaN; };
  const clamp = (n, lo, hi) => Math.min(hi, Math.max(lo, n));
  const pad = (n) => String(n).padStart(2, "0");
  const todayKey = () => { const d = new Date(); return `${d.getFullYear()}-${pad(d.getMonth() + 1)}-${pad(d.getDate())}`; };

  /* ---------- tabs ---------- */
  const tabs = [...document.querySelectorAll('[role="tab"]')];
  function selectTab(tab, moveFocus) {
    tabs.forEach((t) => {
      const on = t === tab;
      t.setAttribute("aria-selected", String(on));
      t.tabIndex = on ? 0 : -1;
      $("#" + t.getAttribute("aria-controls")).hidden = !on;
    });
    if (moveFocus) tab.focus();
    store.set("tab", tab.id);
  }
  tabs.forEach((t, i) => {
    t.addEventListener("click", () => selectTab(t));
    t.addEventListener("keydown", (e) => {
      if (e.key === "ArrowRight") { e.preventDefault(); selectTab(tabs[(i + 1) % tabs.length], true); }
      if (e.key === "ArrowLeft") { e.preventDefault(); selectTab(tabs[(i - 1 + tabs.length) % tabs.length], true); }
    });
  });
  const savedTab = tabs.find((t) => t.id === store.get("tab", ""));
  if (savedTab) selectTab(savedTab);

  /* =========================================================
     RELAX GAME - TIC TAC TOE
     ========================================================= */
  const cells = [...document.querySelectorAll(".ttt-cell")];
  const turnLabel = document.getElementById("game-turn");
  const gameMsg = document.getElementById("game-msg");

  let board = Array(9).fill("");
  let currentPlayer = "X";
  let gameActive = true;

  const winningPatterns = [
    [0, 1, 2], [3, 4, 5], [6, 7, 8],
    [0, 3, 6], [1, 4, 7], [2, 5, 8],
    [0, 4, 8], [2, 4, 6]
  ];

  function updateTurn() {
    turnLabel.textContent = currentPlayer;
  }

  function setMessage(text) {
    gameMsg.textContent = text;
  }

  function checkWinner() {
    for (const combo of winningPatterns) {
      const [a, b, c] = combo;
      if (board[a] && board[a] === board[b] && board[a] === board[c]) {
        return board[a];
      }
    }
    return null;
  }

  function finishGame(winner) {
    gameActive = false;
    if (winner) {
      setMessage(`Player ${winner} wins!`);
      cells.forEach((cell) => cell.disabled = true);
    } else {
      setMessage("It's a draw! Try again.");
      cells.forEach((cell) => cell.disabled = true);
    }
  }

  function handleCellClick(event) {
    const cell = event.currentTarget;
    const index = Number(cell.dataset.index);

    if (!gameActive || board[index]) return;

    board[index] = currentPlayer;
    cell.textContent = currentPlayer;
    cell.disabled = true;

    const winner = checkWinner();
    if (winner) {
      finishGame(winner);
      return;
    }

    if (board.every(Boolean)) {
      finishGame(null);
      return;
    }

    currentPlayer = currentPlayer === "X" ? "O" : "X";
    updateTurn();
    setMessage(`Player ${currentPlayer}'s turn.`);
  }

  function resetGame() {
    board = Array(9).fill("");
    currentPlayer = "X";
    gameActive = true;
    cells.forEach((cell) => {
      cell.textContent = "";
      cell.disabled = false;
    });
    updateTurn();
    setMessage("Player X starts.");
  }

  cells.forEach((cell) => cell.addEventListener("click", handleCellClick));
  document.getElementById("game-reset").addEventListener("click", resetGame);
  resetGame();

  /* =========================================================
     FOCUS TIMER
     ========================================================= */
  const MODES = { focus: "Focus", short: "Short break", long: "Long break" };
  const BREAK_MIN = { short: 5, long: 15 };
  const CIRC = 2 * Math.PI * 100;

  let focusMin = clamp(Math.round(num(store.get("focusMin", 25))) || 25, 1, 120);
  let mode = "focus";
  let total = focusMin * 60;
  let remaining = total;
  let endAt = 0;
  let ticker = null;

  const ringBar = $("#ring-bar");
  ringBar.style.strokeDasharray = CIRC;
  $("#focus-min").value = focusMin;

  const minutesFor = (m) => (m === "focus" ? focusMin : BREAK_MIN[m]);
  const sessionsToday = () => { const s = store.get("sessions", null); return s && s.date === todayKey() ? s.count : 0; };

  function paintTimer() {
    const secs = Math.max(0, Math.ceil(remaining));
    const text = `${pad(Math.floor(secs / 60))}:${pad(secs % 60)}`;
    $("#time").textContent = text;
    $("#mode-label").textContent = MODES[mode];
    ringBar.style.strokeDashoffset = CIRC * (1 - remaining / total);
    document.title = ticker ? `${text} - ${MODES[mode]}` : "Study desk";
    $("#t-start").textContent = ticker ? "Pause" : remaining < total ? "Resume" : "Start";
    $("#sessions").textContent = sessionsToday();
    $("#focus-min").disabled = !!ticker;
    document.querySelectorAll("[data-mode]").forEach((b) => b.setAttribute("aria-pressed", String(b.dataset.mode === mode)));
  }

  function stopTicker() { clearInterval(ticker); ticker = null; }

  function setMode(m) {
    stopTicker();
    mode = m;
    total = minutesFor(m) * 60;
    remaining = total;
    paintTimer();
  }

  function beep() {
    try {
      const ctx = new (window.AudioContext || window.webkitAudioContext)();
      const osc = ctx.createOscillator();
      const gain = ctx.createGain();
      osc.frequency.value = 880;
      gain.gain.setValueAtTime(0.0001, ctx.currentTime);
      gain.gain.exponentialRampToValueAtTime(0.25, ctx.currentTime + 0.03);
      gain.gain.exponentialRampToValueAtTime(0.0001, ctx.currentTime + 0.8);
      osc.connect(gain).connect(ctx.destination);
      osc.start();
      osc.stop(ctx.currentTime + 0.8);
    } catch (e) { /* sound is optional */ }
  }

  function finish() {
    const wasFocus = mode === "focus";
    stopTicker();
    beep();
    if (wasFocus) {
      store.set("sessions", { date: todayKey(), count: sessionsToday() + 1 });
      const long = sessionsToday() % 4 === 0;
      setMode(long ? "long" : "short");
      $("#t-msg").textContent = long
        ? "Focus session finished. You've earned a long break."
        : "Focus session finished. Take a short break.";
    } else {
      setMode("focus");
      $("#t-msg").textContent = "Break over. Ready for the next focus session?";
    }
  }

  function tick() {
    remaining = (endAt - Date.now()) / 1000;
    if (remaining <= 0) { remaining = 0; finish(); return; }
    paintTimer();
  }

  $("#t-start").addEventListener("click", () => {
    $("#t-msg").textContent = "";
    if (ticker) { stopTicker(); paintTimer(); return; }
    endAt = Date.now() + remaining * 1000;
    ticker = setInterval(tick, 250);
    paintTimer();
  });
  $("#t-reset").addEventListener("click", () => { $("#t-msg").textContent = ""; setMode(mode); });
  document.querySelectorAll("[data-mode]").forEach((b) =>
    b.addEventListener("click", () => { $("#t-msg").textContent = ""; setMode(b.dataset.mode); })
  );
  $("#focus-min").addEventListener("change", (e) => {
    const v = clamp(Math.round(num(e.target.value)) || 25, 1, 120);
    focusMin = v;
    e.target.value = v;
    store.set("focusMin", v);
    if (mode === "focus") setMode("focus");
  });
  paintTimer();

  /* =========================================================
     ASSIGNMENTS
     ========================================================= */
  let assignments = store.get("assignments", []);
  const saveAssignments = () => store.set("assignments", assignments);

  function daysUntil(dateStr) {
    const due = new Date(dateStr + "T00:00:00");
    const now = new Date(); now.setHours(0, 0, 0, 0);
    return Math.round((due - now) / 86400000);
  }

  function dueInfo(a) {
    if (!a.due) return { text: "No due date", late: false };
    const d = daysUntil(a.due);
    const nice = new Date(a.due + "T00:00:00").toLocaleDateString(undefined, { month: "short", day: "numeric" });
    if (d < 0) return { text: `${-d} day${d === -1 ? "" : "s"} overdue (${nice})`, late: !a.done };
    if (d === 0) return { text: "Due today", late: false };
    if (d === 1) return { text: "Due tomorrow", late: false };
    return { text: `Due in ${d} days (${nice})`, late: false };
  }

  function renderAssignments() {
    const list = $("#a-list");
    list.replaceChildren();
    const sorted = [...assignments].sort((x, y) => {
      if (x.done !== y.done) return x.done ? 1 : -1;
      if (x.due !== y.due) return !x.due ? 1 : !y.due ? -1 : x.due < y.due ? -1 : 1;
      return 0;
    });

    sorted.forEach((a) => {
      const info = dueInfo(a);
      const meta = [a.course, info.text].filter(Boolean).join(", ");
      const box = el("input", { type: "checkbox", "aria-label": `Mark "${a.title}" as done` });
      box.checked = a.done;
      box.addEventListener("change", () => { a.done = box.checked; saveAssignments(); renderAssignments(); });
      const del = el("button", { type: "button", class: "link-btn", text: "Remove", "aria-label": `Remove "${a.title}"` });
      del.addEventListener("click", () => {
        assignments = assignments.filter((x) => x.id !== a.id);
        saveAssignments(); renderAssignments();
      });
      list.append(el("li", { class: a.done ? "done" : "" },
        box,
        el("div", { class: "a-body" },
          el("div", { class: "a-title", text: a.title }),
          el("div", { class: "a-meta" + (info.late ? " late" : ""), text: meta })),
        del));
    });

    const open = assignments.filter((a) => !a.done);
    const late = open.filter((a) => a.due && daysUntil(a.due) < 0).length;
    $("#a-summary").textContent = assignments.length
      ? `${open.length} open${late ? `, ${late} overdue` : ""}. Earliest due date first.`
      : "Add what's due and the list sorts itself by date.";
    $("#a-empty").hidden = assignments.length > 0;
  }

  $("#a-add").addEventListener("click", () => {
    const title = $("#a-title").value.trim();
    if (!title) { $("#a-msg").textContent = "Enter a name for the assignment."; $("#a-title").focus(); return; }
    $("#a-msg").textContent = "";
    assignments.push({ id: uid(), title, course: $("#a-course").value.trim(), due: $("#a-due").value, done: false });
    saveAssignments();
    $("#a-title").value = "";
    $("#a-due").value = "";
    renderAssignments();
    $("#a-title").focus();
  });
  $("#a-title").addEventListener("keydown", (e) => { if (e.key === "Enter") $("#a-add").click(); });
  renderAssignments();

  /* =========================================================
     SCHEDULE
     ========================================================= */
  const DAYS = ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"];
  let classes = store.get("classes", []);
  const saveClasses = () => store.set("classes", classes);

  const toMin = (t) => { const [h, m] = t.split(":").map(Number); return h * 60 + m; };
  const fmtTime = (t) => {
    const [h, m] = t.split(":").map(Number);
    return new Date(2000, 0, 1, h, m).toLocaleTimeString(undefined, { hour: "numeric", minute: "2-digit" });
  };
  const todayIndex = () => (new Date().getDay() + 6) % 7; // Monday = 0
  const classesOn = (day) =>
    classes.filter((c) => c.days.includes(day)).sort((a, b) => toMin(a.start) - toMin(b.start));

  function paintNow() {
    const box = $("#s-now");
    box.hidden = classes.length === 0;
    if (!classes.length) return;
    const now = new Date();
    const mins = now.getHours() * 60 + now.getMinutes();
    const list = classesOn(todayIndex());
    const current = list.find((c) => toMin(c.start) <= mins && mins < toMin(c.end));
    const next = list.find((c) => toMin(c.start) > mins);
    let text;
    if (current) {
      text = `Now: ${current.subject} until ${fmtTime(current.end)}.`;
      if (next) text += ` Next: ${next.subject} at ${fmtTime(next.start)}.`;
    } else if (next) {
      text = `Next today: ${next.subject} at ${fmtTime(next.start)}.`;
    } else {
      text = list.length ? "No more classes today." : "No classes today.";
    }
    box.textContent = text;
  }

  function renderSchedule() {
    const week = $("#s-week");
    week.replaceChildren();
    $("#s-empty").hidden = classes.length > 0;

    if (classes.length) {
      DAYS.forEach((name, d) => {
        const list = classesOn(d);
        const isToday = d === todayIndex();
        const head = el("h3", {}, name, isToday ? el("span", { class: "tag", text: "Today" }) : "");
        const section = el("section", { class: "day" + (isToday ? " today" : "") }, head);

        if (!list.length) {
          section.append(el("p", { class: "free", text: "No classes." }));
        } else {
          const ul = el("ul");
          list.forEach((c) => {
            const del = el("button", { type: "button", class: "link-btn", text: "Remove", "aria-label": `Remove ${c.subject} on ${name}` });
            del.addEventListener("click", () => {
              c.days = c.days.filter((x) => x !== d);
              if (!c.days.length) classes = classes.filter((x) => x.id !== c.id);
              saveClasses(); renderSchedule();
            });
            ul.append(el("li", {},
              el("span", { class: "s-time", text: `${fmtTime(c.start)} to ${fmtTime(c.end)}` }),
              el("span", { class: "s-main" },
                el("strong", { text: c.subject }),
                c.place ? el("div", { class: "s-place", text: c.place }) : ""),
              del));
          });
          section.append(ul);
        }
        week.append(section);
      });
    }
    paintNow();
  }

  $("#s-weekdays").addEventListener("click", () => {
    document.querySelectorAll("#s-days input").forEach((box) => { box.checked = Number(box.value) <= 4; });
  });

  $("#s-add").addEventListener("click", () => {
    const subject = $("#s-subject").value.trim();
    const days = [...document.querySelectorAll("#s-days input:checked")].map((box) => Number(box.value));
    const start = $("#s-start").value;
    const end = $("#s-end").value;
    const msg = $("#s-msg");

    if (!subject) { msg.textContent = "Enter the subject name."; $("#s-subject").focus(); return; }
    if (!days.length) { msg.textContent = "Pick at least one day."; return; }
    if (!start || !end) { msg.textContent = "Set a start time and an end time."; return; }
    if (toMin(end) <= toMin(start)) { msg.textContent = "The end time must be after the start time."; return; }

    msg.textContent = "";
    classes.push({ id: uid(), subject, place: $("#s-place").value.trim(), days, start, end });
    saveClasses();
    $("#s-subject").value = "";
    $("#s-place").value = "";
    $("#s-start").value = "";
    $("#s-end").value = "";
    document.querySelectorAll("#s-days input").forEach((box) => { box.checked = false; });
    renderSchedule();
    $("#s-subject").focus();
  });
  $("#s-subject").addEventListener("keydown", (e) => { if (e.key === "Enter") $("#s-add").click(); });

  let lastDay = todayIndex();
  setInterval(() => {
    paintNow();
    if (todayIndex() !== lastDay) { lastDay = todayIndex(); renderSchedule(); }
  }, 60000);
  renderSchedule();

  /* =========================================================
     FLASHCARDS
     ========================================================= */
  let cards = store.get("cards", []);
  let idx = 0;
  let flipped = false;
  const saveCards = () => store.set("cards", cards);

  function paintCard() {
    $("#card").classList.toggle("flipped", flipped);
    const c = cards[idx];
    if (!c) return;
    $("#face-front").replaceChildren(el("small", { text: "Term" }), c.front);
    $("#face-back").replaceChildren(el("small", { text: "Answer" }), c.back);
    $("#c-count").textContent = `Card ${idx + 1} of ${cards.length}`;
    $("#c-live").textContent = flipped ? `Answer: ${c.back}` : `Term: ${c.front}`;
  }

  function renderCards() {
    idx = clamp(idx, 0, Math.max(0, cards.length - 1));
    $("#c-stage").hidden = cards.length === 0;
    $("#c-empty").hidden = cards.length > 0;
    $("#c-prev").disabled = $("#c-next").disabled = $("#c-shuffle").disabled = cards.length < 2;

    const list = $("#c-list");
    list.replaceChildren();
    cards.forEach((c) => {
      const del = el("button", { type: "button", class: "link-btn", text: "Remove", "aria-label": `Remove card: ${c.front}` });
      del.addEventListener("click", () => {
        cards = cards.filter((x) => x.id !== c.id);
        flipped = false;
        saveCards(); renderCards();
      });
      list.append(el("li", {}, el("span", { class: "c-term", text: c.front }), el("span", { class: "c-def", text: c.back }), del));
    });
    paintCard();
  }

  function go(step) {
    if (cards.length < 2) return;
    idx = (idx + step + cards.length) % cards.length;
    flipped = false;
    paintCard();
  }

  $("#card").addEventListener("click", () => { flipped = !flipped; paintCard(); });
  $("#card").addEventListener("keydown", (e) => {
    if (e.key === "ArrowRight") { e.preventDefault(); go(1); }
    if (e.key === "ArrowLeft") { e.preventDefault(); go(-1); }
  });
  $("#c-next").addEventListener("click", () => go(1));
  $("#c-prev").addEventListener("click", () => go(-1));
  $("#c-shuffle").addEventListener("click", () => {
    for (let i = cards.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [cards[i], cards[j]] = [cards[j], cards[i]];
    }
    idx = 0; flipped = false;
    saveCards(); renderCards();
  });

  $("#c-add").addEventListener("click", () => {
    const front = $("#c-front").value.trim();
    const back = $("#c-back").value.trim();
    if (!front || !back) { $("#c-msg").textContent = "Fill in both the term and the answer."; return; }
    $("#c-msg").textContent = "";
    cards.push({ id: uid(), front, back });
    saveCards();
    $("#c-front").value = "";
    $("#c-back").value = "";
    $("#c-front").focus();
    renderCards();
  });
  $("#c-back").addEventListener("keydown", (e) => { if (e.key === "Enter") $("#c-add").click(); });
  renderCards();
})();
</script>
</body>
</html>
