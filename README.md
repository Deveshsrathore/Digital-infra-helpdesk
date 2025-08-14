# Digital-infra-helpdesk
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Digital Infra Helpdesk – Search</title>
  <meta name="description" content="Google‑style search powered by Google Programmable Search Engine (CSE)." />
  <style>
    :root {
      --accent: #1a73e8; /* Google-ish blue */
      --text: #202124;
      --muted: #5f6368;
      --bg: #ffffff;
    }
    * { box-sizing: border-box; }
    html, body { height: 100%; }
    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      color: var(--text);
      background: var(--bg);
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    /* Header */
    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 18px;
    }
    .brand {
      display: inline-flex; align-items: center; gap: 10px;
      font-weight: 700; font-size: 18px; letter-spacing: .2px;
    }
    .brand-dot { width: 10px; height: 10px; border-radius: 50%; background: var(--accent); display: inline-block; }
    .nav a { color: var(--muted); text-decoration: none; margin-left: 14px; font-size: 14px; }
    .nav a:hover { text-decoration: underline; }

    /* Hero (home mode) */
    .hero {
      display: grid;
      place-items: center;
      text-align: center;
      padding: 8vh 16px 24px;
    }
    .logo {
      font-size: clamp(28px, 5vw, 64px);
      font-weight: 800;
      letter-spacing: -0.5px;
      margin: 20px 0 18px;
    }
    .logo span { color: var(--accent); }
    .tagline { color: var(--muted); font-size: 14px; margin-bottom: 16px; }

    /* Search */
    .search-wrap {
      width: min(720px, 92vw);
      position: relative;
    }
    .searchbox {
      width: 100%;
      display: flex;
      align-items: center;
      gap: 10px;
      background: #fff;
      border: 1px solid #dadce0;
      border-radius: 24px;
      padding: 10px 14px;
      box-shadow: 0 1px 2px rgba(0,0,0,.04);
    }
    .searchbox:hover { box-shadow: 0 1px 6px rgba(0,0,0,.1); }
    .searchbox input[type="text"] {
      flex: 1;
      border: none;
      outline: none;
      font-size: 16px;
      color: var(--text);
      background: transparent;
    }
    .btns { margin-top: 18px; display: flex; gap: 10px; justify-content: center; }
    .btn {
      border: 1px solid transparent;
      padding: 8px 14px; border-radius: 6px; cursor: pointer;
      background: #f8f9fa; color: #3c4043; font-size: 14px;
    }
    .btn:hover { border-color: #dadce0; }

    /* Results layout */
    .results-layout { display: none; }
    .results-header {
      padding: 10px 18px; border-bottom: 1px solid #eee; display: flex; align-items: center; gap: 14px;
    }
    .results-header .mini-logo { font-weight: 800; color: var(--accent); }
    .results-container { width: min(900px, 92vw); margin: 14px auto 80px; }
    .stat { color: var(--muted); font-size: 12px; margin: 8px 2px 16px; }

    .result-item { margin: 0 0 24px; }
    .result-item a.title { font-size: 18px; color: #1a0dab; text-decoration: none; }
    .result-item a.title:hover { text-decoration: underline; }
    .result-item .link { color: #006621; font-size: 12px; margin: 3px 0; overflow-wrap: anywhere; }
    .result-item .snippet { color: #3c4043; font-size: 14px; }

    .pagination { display: flex; gap: 6px; flex-wrap: wrap; margin: 24px 0; }
    .page-btn { padding: 6px 10px; border: 1px solid #dadce0; background: #fff; border-radius: 6px; cursor: pointer; font-size: 14px; }
    .page-btn.active { background: var(--accent); color: #fff; border-color: var(--accent); }

    footer { margin-top: auto; padding: 16px; text-align: center; color: var(--muted); border-top: 1px solid #eee; }
    .fine { font-size: 12px; color: var(--muted); }

    @media (min-width: 900px) {
      .hero { padding-top: 14vh; }
    }
  </style>
</head>
<body>
  <header>
    <div class="brand" onclick="goHome()" style="cursor:pointer">
      <span class="brand-dot"></span>
      <span>Digital Infra Helpdesk</span>
    </div>
    <nav class="nav">
      <a href="#services" onclick="scrollToServices(event)">Services</a>
      <a href="#contact" onclick="scrollToContact(event)">Contact</a>
      <a href="#" onclick="openForm(event)">Client Form</a>
    </nav>
  </header>

  <!-- Home (Google-like) -->
  <main id="home">
    <div class="hero">
      <div class="logo">Digital <span>Infra</span> Helpdesk</div>
      <div class="tagline">Google‑style search powered by CSE • Minimal • Fast</div>
      <form class="search-wrap" id="homeSearchForm">
        <div class="searchbox">
          <input id="qHome" type="text" placeholder="Search the web…" aria-label="Search" autocomplete="off" />
        </div>
        <div class="btns">
          <button class="btn" type="submit">Search</button>
          <button class="btn" type="button" onclick="feelingLucky()">I'm Feeling Lucky</button>
        </div>
      </form>

      <!-- Optional quick links area -->
      <div style="margin-top:26px; color:var(--muted); font-size:13px;">
        Quick: <a href="#" onclick="prefill('SAP MM vendor creation')">SAP MM</a> ·
        <a href="#" onclick="prefill('construction material rates Lucknow')">Material Rates</a> ·
        <a href="#" onclick="prefill('Ariba SLP onboarding steps')">Ariba SLP</a>
      </div>
    </div>
  </main>

  <!-- Results Mode -->
  <section id="resultsMode" class="results-layout">
    <div class="results-header">
      <div class="mini-logo">DIH</div>
      <form id="topSearchForm" style="flex:1">
        <div class="searchbox" style="border-radius: 8px;">
          <input id="qTop" type="text" placeholder="Search the web…" aria-label="Searc
