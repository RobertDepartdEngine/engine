<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DEPARTD Engine - Executive Master Deck 2026</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800;900&family=Space+Grotesk:wght@400;600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <style>
        /* CORE RESET & VARS */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        :root {
            --brand: #ff4900;
            --bg-dark: #050505;
            --bg-card: #111111;
            --text-main: #ffffff;
            --text-muted: #888888;
            --font-head: 'Outfit', sans-serif;
            --font-body: 'Space Grotesk', sans-serif;
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-main);
            font-family: var(--font-body);
            overflow: hidden; /* JS handles scrolling */
            width: 100vw;
            height: 100vh;
        }

        /* SLIDER CONTAINER */
        #presentation-container {
            width: 100%;
            height: 100%;
            display: flex;
            transition: transform 0.6s cubic-bezier(0.77, 0, 0.175, 1);
        }

        .slide {
            min-width: 100vw;
            height: 100vh;
            padding: 60px 80px;
            display: flex;
            flex-direction: column;
            position: relative;
            background: radial-gradient(circle at 90% 10%, rgba(255, 73, 0, 0.05) 0%, transparent 60%);
        }

        /* HEADER & FOOTER */
        .header { display: flex; justify-content: space-between; align-items: flex-start; z-index: 10; border-bottom: 1px solid rgba(255,255,255,0.05); padding-bottom: 20px; }
        .logo { font-family: var(--font-head); font-weight: 900; font-size: 24px; letter-spacing: -1px; }
        .logo span { color: var(--brand); }
        .tagline { font-size: 14px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 2px; }
        
        .footer { position: absolute; bottom: 40px; left: 80px; right: 80px; display: flex; justify-content: space-between; align-items: center; border-top: 1px solid rgba(255,255,255,0.05); padding-top: 20px; color: #444; font-size: 14px; z-index: 10; }
        .progress-bar { position: absolute; bottom: 0; left: 0; height: 3px; background: var(--brand); transition: width 0.3s ease; z-index: 20; }

        /* CONTENT LAYOUTS */
        .content { flex-grow: 1; display: flex; align-items: center; gap: 80px; padding: 40px 0 80px 0; z-index: 1; }
        .content.center { justify-content: center; text-align: center; flex-direction: column; }
        .text-side { flex: 1.2; }
        .visual-side { flex: 1; height: 100%; display: flex; flex-direction: column; justify-content: center; position: relative; }

        /* TYPOGRAPHY */
        h1 { font-family: var(--font-head); font-weight: 900; font-size: 72px; line-height: 1; letter-spacing: -2px; margin-bottom: 20px; text-transform: uppercase; }
        h1 span { color: var(--brand); }
        h2 { font-family: var(--font-head); font-weight: 800; font-size: 42px; line-height: 1.1; margin-bottom: 30px; letter-spacing: -1px; border-left: 6px solid var(--brand); padding-left: 20px; }
        h3 { font-family: var(--font-head); font-weight: 600; font-size: 24px; color: var(--brand); margin-bottom: 15px; }
        
        p.subtitle { color: var(--brand); letter-spacing: 4px; font-weight: 700; text-transform: uppercase; margin-bottom: 20px; font-size: 14px; }
        p.lead { font-size: 20px; color: var(--text-muted); line-height: 1.6; margin-bottom: 30px; max-width: 800px; }
        
        ul { list-style: none; }
        li { font-size: 22px; line-height: 1.5; color: #dddddd; margin-bottom: 20px; position: relative; padding-left: 35px; }
        li::before { content: '■'; position: absolute; left: 0; color: var(--brand); font-size: 14px; top: 6px; }

        /* NOTES BLOCK */
        .speaker-notes { background: rgba(255, 73, 0, 0.05); border: 1px dashed rgba(255, 73, 0, 0.3); padding: 20px; border-radius: 8px; margin-top: 40px; }
        .speaker-notes .notes-title { color: var(--brand); font-size: 12px; text-transform: uppercase; letter-spacing: 1px; margin-bottom: 10px; font-weight: bold; }
        .speaker-notes p { font-size: 16px; color: #aaa; line-height: 1.5; font-style: italic; margin: 0; }

        /* COMPONENTS */
        .kpi-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; width: 100%; }
        .kpi-card { background: var(--bg-card); padding: 30px; border-radius: 12px; border: 1px solid #222; text-align: left; }
        .kpi-val { font-family: var(--font-head); font-weight: 900; font-size: 56px; color: var(--brand); line-height: 1; margin-bottom: 5px; }
        .kpi-lbl { font-size: 14px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 1px; font-weight: 600; }
        
        .kpi-card.highlight { background: rgba(255, 73, 0, 0.1); border-color: var(--brand); }
        .kpi-card.highlight .kpi-val { color: #fff; }

        .timeline { display: flex; align-items: flex-start; justify-content: space-between; position: relative; width: 100%; padding-top: 40px; }
        .timeline::before { content: ''; position: absolute; top: 48px; left: 0; width: 100%; height: 2px; background: #333; z-index: 0; }
        .tl-item { flex: 1; text-align: center; position: relative; z-index: 1; padding: 0 10px; }
        .tl-dot { width: 18px; height: 18px; background: var(--bg-dark); border: 4px solid var(--brand); border-radius: 50%; margin: 0 auto 20px auto; }
        .tl-item h4 { font-family: var(--font-head); font-size: 18px; margin-bottom: 10px; }
        .tl-item p { font-size: 14px; color: var(--text-muted); line-height: 1.4; }

        .architecture-box { background: var(--bg-card); border: 1px solid #333; border-radius: 8px; padding: 20px; margin-bottom: 15px; text-align: center; }
        .architecture-box i { font-size: 32px; color: var(--brand); margin-bottom: 10px; }
        .architecture-box span { display: block; font-weight: bold; font-size: 14px; letter-spacing: 1px; }

        .brand-pill-container { display: flex; flex-wrap: wrap; gap: 15px; margin-top: 20px; }
        .brand-pill { background: #1a1a1a; border: 1px solid #333; padding: 10px 20px; border-radius: 30px; font-weight: 600; font-size: 16px; color: #ccc; }

        .controls { position: fixed; bottom: 30px; right: 80px; z-index: 50; display: flex; gap: 10px; }
        .btn-nav { background: #222; border: none; color: #fff; width: 40px; height: 40px; border-radius: 50%; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 16px; transition: 0.2s; }
        .btn-nav:hover { background: var(--brand); }
    </style>
</head>
<body>

    <div id="presentation-container">

        <section class="slide">
            <div class="header">
                <div class="logo">DEPARTD <span>ENGINE</span></div>
                <div class="tagline">Strategic GF Master Deck 2026</div>
            </div>
            <div class="content center">
                <p class="subtitle">Das End-to-End Betriebssystem für Influencer Marketing</p>
                <h1>Systematische <br><span>Dominanz.</span></h1>
                <p class="lead" style="text-align: center;">Wie wir durch radikale Digitalisierung der Wertschöpfungskette das Umsatzwachstum vom Personalaufwand entkoppeln – und Best-in-Class Margen realisieren.</p>
                <div class="speaker-notes" style="text-align: left; max-width: 800px; margin: 40px auto 0 auto;">
                    <div class="notes-title">Sprechernotizen</div>
                    <p>„David, Basti – willkommen. Influencer Marketing im DACH-Raum ist an einem Wendepunkt. Wer Kampagnen heute noch über Excel und WhatsApp steuert, skaliert seine Kosten linear zum Umsatz. Wir haben mit der DEPARTD Engine ein Betriebssystem gebaut, das diesen Flaschenhals sprengt. Wir zeigen euch heute die komplette Architektur, unsere historische Entwicklung und warum diese Software der stärkste Wettbewerbsvorteil (Moat) ist, den diese Agentur besitzt.“</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>01 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">The Status Quo</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Warum manuelles Handling nicht skaliert</h2>
                    <ul>
                        <li><strong>Fragmentierung:</strong> Ein Flickenteppich aus Tools, Excel-Listen und E-Mails führt zu Datenverlust und Chaos.</li>
                        <li><strong>Die Personalfalle:</strong> Doppeltes Kampagnenvolumen erfordert im Marktstandard doppeltes Personal. Die Marge stagniert.</li>
                        <li><strong>Fehlendes Momentum:</strong> Nach Reporting-Abgabe verpufft das Wissen. Es gibt keinen systematischen Aufbau einer eigenen Creator-Datenbasis.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Das klassische Agenturmodell hat einen Webfehler: Manuelle Prozesse fressen den Rohertrag. Wenn wir Hunderte Micro-Creator aktivieren wollen, scheitern wir nicht am Finden der Creator, sondern am administrativen Overhead. Um zu skalieren, mussten wir dieses System von Grund auf neu erfinden.“</p>
                    </div>
                </div>
                <div class="visual-side" style="align-items: center;">
                    <div style="font-size: 180px; color: #1a1a1a;"><i class="fa-solid fa-link-slash"></i></div>
                    <p style="color: var(--brand); font-weight: bold; letter-spacing: 2px; margin-top: 20px;">BROKEN VALUE CHAIN</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>02 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Strategic Vision</div></div>
            <div class="content center">
                <h2>Die Vision: Software-gesteuertes Wachstum</h2>
                <h1 style="font-size: 50px; text-transform: none; color: #fff; margin: 40px 0;">Wir ersetzen repetitive <span style="color: var(--text-muted); text-decoration: line-through;">Fleißarbeit</span> durch <br><span style="color: var(--brand);">System-Intelligenz.</span></h1>
                <div class="kpi-grid" style="max-width: 1000px; margin-top: 20px;">
                    <div class="kpi-card" style="text-align: center;"><h3>Zentralisierung</h3><p style="color: #aaa;">Ein einziges System von Sourcing bis Reporting.</p></div>
                    <div class="kpi-card" style="text-align: center;"><h3>Daten-Monopol</h3><p style="color: #aaa;">Aufbau einer proprietären Asset-Datenbank.</p></div>
                    <div class="kpi-card" style="text-align: center;"><h3>Margen-Hebel</h3><p style="color: #aaa;">Senkung der Handlingkosten pro Creator gen Null.</p></div>
                    <div class="kpi-card" style="text-align: center;"><h3>Transparenz</h3><p style="color: #aaa;">Live-Dashboards für maximales Kundenvertrauen.</p></div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>03 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Development Journey</div></div>
            <div class="content" style="flex-direction: column; align-items: flex-start; justify-content: center;">
                <h2>Die Evolution der Engine</h2>
                <div class="timeline">
                    <div class="tl-item">
                        <div class="tl-dot"></div>
                        <h4>1. Ordnung</h4>
                        <p>Zentrale Datenbank ersetzt verstreute Excels.</p>
                    </div>
                    <div class="tl-item">
                        <div class="tl-dot"></div>
                        <h4>2. Automation</h4>
                        <p>TikTok-Crawl & Monday.com Sync + Farming Bot.</p>
                    </div>
                    <div class="tl-item">
                        <div class="tl-dot"></div>
                        <h4>3. Value</h4>
                        <p>Automatisierte Reports & Multi-Brand Portal.</p>
                    </div>
                    <div class="tl-item">
                        <div class="tl-dot"></div>
                        <h4>4. Intelligence</h4>
                        <p>DEPARTD Lens AI, Sound & Sentiment Scoring.</p>
                    </div>
                    <div class="tl-item" style="opacity: 1;">
                        <div class="tl-dot" style="background: var(--brand);"></div>
                        <h4 style="color: var(--brand);">5. Betriebssystem</h4>
                        <p>Finanz-Integration (Candis/Billomat), RBAC.</p>
                    </div>
                </div>
                <div class="speaker-notes" style="width: 100%;">
                    <div class="notes-title">Sprechernotizen</div>
                    <p>„Wir sind längst aus der Prototyp-Phase heraus. Phase 1 startete als Datenbank. Heute, in Phase 5, ist die Engine das zentrale Nervensystem, das operativ mit unserer ERP-Infrastruktur (Candis, Billomat) verschmolzen ist.“</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>04 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Scale & Growth</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Wachstum 2025 vs. 2026</h2>
                    <p class="lead">Der direkte Beweis für Skalierbarkeit: Wir managen fast doppelt so viele Kampagnen und ein massiv erhöhtes Budget – bei steigender Content-Qualität.</p>
                    <ul>
                        <li><strong>Budget-Explosion:</strong> Steigerung des betreuten Volumens um <strong>+251 %</strong>.</li>
                        <li><strong>Effizienz-Shift:</strong> Weniger Videos pro Kampagne, dafür gezieltere Creator-Auswahl → Engagement-Rate steigt von 0.6% auf 0.8%.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Hier sehen wir den Engine-Effekt schwarz auf weiß. Wir machen 2026 fast doppelt so viele Kampagnen wie 2025 (32 vs 18). Unser Budget schießt um 251% nach oben. Aber wir fluten den Markt nicht blind mit Content – die Engagement-Rate ist signifikant gestiegen. Qualität trotz Masse.“</p>
                    </div>
                </div>
                <div class="visual-side">
                    <div class="kpi-grid">
                        <div class="kpi-card" style="border-color: #333;">
                            <div class="kpi-lbl">Kampagnen</div>
                            <div style="display:flex; justify-content: space-between; align-items: baseline; margin-top: 10px;">
                                <div><span style="font-size:24px; color:#aaa;">25:</span> <span style="font-size:32px; font-weight:bold;">18</span></div>
                                <div><span style="font-size:24px; color:#aaa;">26:</span> <span style="font-size:32px; font-weight:bold; color:var(--brand)">32</span></div>
                            </div>
                        </div>
                        <div class="kpi-card" style="border-color: #333;">
                            <div class="kpi-lbl">Creator Activations</div>
                            <div style="display:flex; justify-content: space-between; align-items: baseline; margin-top: 10px;">
                                <div><span style="font-size:24px; color:#aaa;">25:</span> <span style="font-size:32px; font-weight:bold;">692</span></div>
                                <div><span style="font-size:24px; color:#aaa;">26:</span> <span style="font-size:32px; font-weight:bold; color:var(--brand)">772</span></div>
                            </div>
                        </div>
                        <div class="kpi-card highlight" style="grid-column: span 2;">
                            <div class="kpi-lbl" style="color: rgba(255,255,255,0.7)">Budget-Volumen</div>
                            <div style="display:flex; justify-content: space-between; align-items: baseline; margin-top: 10px;">
                                <div><span style="font-size:24px; color:#fff;">2025:</span> <span style="font-size:42px; font-weight:bold; color:#fff;">247k €</span></div>
                                <div><span style="font-size:24px; color:#fff;">2026:</span> <span style="font-size:42px; font-weight:bold; color:#fff;">870k €</span></div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>05 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Client Portfolio</div></div>
            <div class="content center">
                <h2>Multimarken-Vertrauen</h2>
                <p class="lead" style="text-align: center;">Unsere Engine steuert die Budgets der relevantesten FMCG- und Entertainment-Brands im DACH-Raum.</p>
                
                <div class="brand-pill-container" style="justify-content: center; max-width: 900px; margin-top: 40px;">
                    <div class="brand-pill">Haribo</div>
                    <div class="brand-pill">Kaufland</div>
                    <div class="brand-pill">Storck</div>
                    <div class="brand-pill">Katjes</div>
                    <div class="brand-pill">Rockstar Energy</div>
                    <div class="brand-pill">Almette</div>
                    <div class="brand-pill">Wagner Pizza</div>
                    <div class="brand-pill">Aoste</div>
                    <div class="brand-pill">RTL+</div>
                    <div class="brand-pill">Tobis Films</div>
                    <div class="brand-pill">Super Dickmanns</div>
                </div>

                <div class="speaker-notes" style="width: 800px; text-align: left;">
                    <div class="notes-title">Sprechernotizen</div>
                    <p>„Wir sind nicht von einem Einzelkunden abhängig. Das System bedient reibungslos FMCG-Giganten wie Kaufland, Storck und Haribo parallel. Diese Brands vertrauen uns, weil unser Multi-Brand-Portal ihnen jederzeit absolute Datentransparenz bietet.“</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>06 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">System Architecture</div></div>
            <div class="content center">
                <h2>Die End-to-End Wertschöpfungskette</h2>
                
                <div style="display: flex; width: 100%; justify-content: space-between; gap: 20px; margin-top: 40px;">
                    <div class="architecture-box" style="flex:1;">
                        <i class="fa-solid fa-satellite-dish"></i>
                        <h3 style="font-size:18px; margin:0 0 10px 0; color:#fff;">1. DISCOVERY</h3>
                        <p style="font-size:14px; color:#aaa;">Bot-Farming & Bulk Import in die Supabase</p>
                    </div>
                    <div style="display:flex; align-items:center; color:var(--brand);"><i class="fa-solid fa-arrow-right"></i></div>
                    <div class="architecture-box" style="flex:1;">
                        <i class="fa-solid fa-brain"></i>
                        <h3 style="font-size:18px; margin:0 0 10px 0; color:#fff;">2. INTELLIGENCE</h3>
                        <p style="font-size:14px; color:#aaa;">Risiko-Analyse & Embeddings Scoring</p>
                    </div>
                    <div style="display:flex; align-items:center; color:var(--brand);"><i class="fa-solid fa-arrow-right"></i></div>
                    <div class="architecture-box" style="flex:1;">
                        <i class="fa-solid fa-rocket"></i>
                        <h3 style="font-size:18px; margin:0 0 10px 0; color:#fff;">3. ACTIVATION</h3>
                        <p style="font-size:14px; color:#aaa;">Kanban Outreach & Concept Portal</p>
                    </div>
                    <div style="display:flex; align-items:center; color:var(--brand);"><i class="fa-solid fa-arrow-right"></i></div>
                    <div class="architecture-box" style="flex:1;">
                        <i class="fa-solid fa-chart-line"></i>
                        <h3 style="font-size:18px; margin:0 0 10px 0; color:#fff;">4. MEASUREMENT</h3>
                        <p style="font-size:14px; color:#aaa;">Lens AI Analysis & Automated Reports</p>
                    </div>
                </div>
                <div class="speaker-notes" style="width: 100%; text-align: left; margin-top: 60px;">
                    <div class="notes-title">Sprechernotizen</div>
                    <p>„Dies ist die Architektur unseres Erfolgs. Ein voll integrierter Prozess ohne Systembrüche. Jeder Datenpunkt, der vorne beim Farming generiert wird, fließt automatisch bis in das Live-Dashboard des Kunden am Ende der Kette.“</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>07 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Modul 1: Discovery</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Creator Hub & Automated Farming</h2>
                    <ul>
                        <li><strong>Creator-Farming-Bot:</strong> Automatisierte Crawler suchen 24/7 nach neuen Profilen, bewerten Nischen und füttern die DB.</li>
                        <li><strong>Intelligenter Import:</strong> Bulk-Upload via CSV mit vollautomatischer Dublettenerkennung und Profil-Hintergrund-Analyse.</li>
                        <li><strong>Semantische Suche:</strong> Auffinden von Creatorn nicht nur nach Keywords, sondern nach inhaltlicher Bedeutung.</li>
                    </ul>
                </div>
                <div class="visual-side">
                    <div class="kpi-grid">
                        <div class="kpi-card highlight">
                            <div class="kpi-val">~70k</div>
                            <div class="kpi-lbl" style="color:rgba(255,255,255,0.7)">Profile in Supabase DB</div>
                        </div>
                        <div class="kpi-card" style="border-color: var(--brand);">
                            <div class="kpi-val">1.500</div>
                            <div class="kpi-lbl">Voll Onboarded (Vertrag/Daten)</div>
                        </div>
                    </div>
                    <div class="speaker-notes" style="margin-top: 20px;">
                        <p>„Unsere Datenbank ist das Gold der Agentur. Wir haben knapp 70.000 Profile indexiert und 1.500 Creator voll operativ nutzbar gemacht. Kein Kunde kann diesen Vorsprung intern nachbauen.“</p>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>08 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Modul 2: Outreach</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Aktivierungs-Pipeline & Concept Portal</h2>
                    <ul>
                        <li><strong>Kanban-Steuerung:</strong> Skalierter Workflow (Ansprache → Onboarding → Briefing → Freigabe) in einem Screen.</li>
                        <li><strong>Kollaborativer Editor:</strong> Zentrale Erstellung von Briefings ohne E-Mail-Ping-Pong.</li>
                        <li><strong>Creator Self-Service:</strong> Creator laden Konzepte und Insights-Screenshots eigenständig hoch – OpenAI Vision liest Metriken automatisch aus und mappt sie in Monday.com.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Hier liegt der Effizienz-Hebel. Die Creator arbeiten *in* unserem System. Sie laden ihre Screenshots hoch, und unsere KI liest die Daten aus. Das spart Uljana und dem Team hunderte Stunden an stumpfer Übertragungsarbeit.“</p>
                    </div>
                </div>
                <div class="visual-side" style="align-items: center;">
                    <div style="background: #1a1a1a; border: 1px solid #333; border-radius: 8px; width: 100%; padding: 20px; display: flex; flex-direction: column; gap: 10px;">
                        <div style="display:flex; justify-content:space-between; color:#888; border-bottom: 1px solid #333; padding-bottom: 5px; font-size:12px;"><span>OUTREACH</span><span>REVIEW</span><span>APPROVED</span></div>
                        <div style="background:#222; padding:15px; border-left: 3px solid #666; border-radius:4px;">Profile #1823 <span style="float:right; color:var(--brand);"><i class="fa-solid fa-spinner"></i></span></div>
                        <div style="background:#222; padding:15px; border-left: 3px solid #ffaa00; border-radius:4px; margin-left:33%;">Concept PDF Uploaded</div>
                        <div style="background:#222; padding:15px; border-left: 3px solid #00ff00; border-radius:4px; margin-left:66%;">Ready for Production</div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>09 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Modul 3: Control</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Das Command Center</h2>
                    <ul>
                        <li><strong>Hierarchische Struktur:</strong> Von der Master-Kampagne über dedizierte Creator-Gruppen bis zum Einzel-Posting.</li>
                        <li><strong>Live-Status Checklisten:</strong> Systemseitige Überwachung, ob Verträge, Briefings und Postings fristgerecht erfolgen.</li>
                        <li><strong>Predictive Zuweisung:</strong> System schlägt Creator basierend auf historischem ROI (Concept → Group → Creator) vor.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Wenn wir 32 Kampagnen gleichzeitig fahren, darf nichts durchs Raster fallen. Das Command Center zwingt uns in saubere, fehlerfreie Prozesse und alarmiert das Team bei Bottlenecks automatisch.“</p>
                    </div>
                </div>
                <div class="visual-side" style="align-items: center;">
                    <div style="font-size: 150px; color: rgba(255,73,0,0.1);"><i class="fa-solid fa-network-wired"></i></div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>10 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Modul 4: Analytics</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>DEPARTD Lens AI: Intelligenz als Produkt</h2>
                    <p class="lead">Wir reporten keine Metriken, wir reporten Wahrheiten. Die KI analysiert organische Kampagnen tiefenmedial.</p>
                    <ul>
                        <li><strong>Multimodal:</strong> Jedes Video wird via gpt-4o-transcribe (Audio) und Vision (Bild) sekundengenau gescannt.</li>
                        <li><strong>Content DNA:</strong> Embedding-Mustererkennung deckt auf, welche Hook-Längen und Visuals wirklich konvertieren.</li>
                        <li><strong>Sentiment Core:</strong> Tonalitätsanalyse Hunderter Kommentare extrahiert die echte Markenwahrnehmung.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen (Anti-Fabrication)</div>
                        <p>„Besonders wichtig für Brands: Unsere KI hat strikte Anti-Fabrication-Regeln. Sie darf nichts erfinden. Sie aggregiert reine, statistische Wahrheiten. Das ist Strategieberatung auf McKinsey-Niveau, generiert in Sekunden.“</p>
                    </div>
                </div>
                <div class="visual-side">
                    <div class="kpi-grid">
                        <div class="kpi-card" style="border-color: #333;"><div class="kpi-val" style="font-size:36px; color:#fff;">DNA Extraction</div><p style="font-size:14px; color:#888;">Audio + Vision</p></div>
                        <div class="kpi-card" style="border-color: #333;"><div class="kpi-val" style="font-size:36px; color:#fff;">Sentiment</div><p style="font-size:14px; color:#888;">Community Mood</p></div>
                        <div class="kpi-card" style="border-color: #333;"><div class="kpi-val" style="font-size:36px; color:#fff;">No Fabrication</div><p style="font-size:14px; color:#888;">Strict Truth Rules</p></div>
                        <div class="kpi-card highlight"><div class="kpi-val" style="font-size:36px;">GPT-4o Base</div><p style="font-size:14px; color:#fff;">Enterprise API</p></div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>11 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Modul 4b: Intelligence</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Sound & Trend Intelligence</h2>
                    <ul>
                        <li><strong>Trend-Radar:</strong> Zweistufiges Schwellenwert-System erkennt Hypes (Sounds/Trends), bevor sie den Mainstream erreichen.</li>
                        <li><strong>Reuse Risk Scoring:</strong> Automatisierte Schutzfunktion bewertet das urheberrechtliche Risiko von TikTok-Sounds.</li>
                        <li><strong>Earned Media Filter:</strong> Saubere System-Trennung von organischem, bezahltem und markeneigenem Content.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Wer auf TikTok wachsen will, muss das Sound-Ökosystem verstehen. Wir nutzen Proxies, um das 'Sound Momentum' zu messen. Gleichzeitig schützt unser Risk Scoring Brands vor juristischen Alpträumen.“</p>
                    </div>
                </div>
                <div class="visual-side" style="align-items: center;">
                    <div style="font-size: 150px; color: rgba(255,73,0,0.1);"><i class="fa-solid fa-wave-square"></i></div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>12 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Modul 5: Value</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Multi-Brand Kundenportal</h2>
                    <p class="lead">Daten werden erst dann zum Wettbewerbsvorteil, wenn der Kunde sie spürt.</p>
                    <ul>
                        <li><strong>Self-Service Dashboards:</strong> Kunden-Logins (E-Mail/PW) für Live-Einsicht in alle aktiven und historischen Kampagnen.</li>
                        <li><strong>Automated Reports:</strong> Gebrandete PDF-/Slide-Exporte (Dark-Design) inklusive Lens AI Slides auf Knopfdruck.</li>
                        <li><strong>Paid Ads Sync:</strong> Ganzheitliche Betrachtung über plattformübergreifende Schnittstellen.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Das Portal ist unsere mächtigste Retention-Waffe. Ein Kunde, der sich an Echtzeit-Insights und dieses Premium-Design gewöhnt hat, wechselt nicht zurück zu einer Agentur, die ihm wöchentlich eine unübersichtliche Excel schickt.“</p>
                    </div>
                </div>
                <div class="visual-side">
                    <div style="background: #111; border: 1px solid #333; padding: 20px; border-radius: 8px; box-shadow: 0 10px 30px rgba(0,0,0,0.5);">
                        <div style="border-bottom: 1px solid #333; padding-bottom: 10px; margin-bottom: 10px; display:flex; justify-content:space-between; color:#888;"><span><i class="fa-solid fa-lock"></i> Client.Portal</span><span>Live</span></div>
                        <div style="display:flex; gap: 10px; margin-bottom: 10px;">
                            <div style="flex:1; background:#222; height: 60px; border-radius:4px;"></div>
                            <div style="flex:1; background:#222; height: 60px; border-radius:4px;"></div>
                            <div style="flex:1; background:rgba(255,73,0,0.2); border: 1px solid var(--brand); height: 60px; border-radius:4px;"></div>
                        </div>
                        <div style="width: 100%; height: 120px; background:#222; border-radius:4px;"></div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>13 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Tech Architecture</div></div>
            <div class="content center">
                <h2>Robuste Enterprise Architektur</h2>
                <div class="kpi-grid" style="grid-template-columns: repeat(4, 1fr); max-width: 1100px; margin-top: 20px;">
                    <div class="architecture-box">
                        <i class="fa-brands fa-react"></i><span>FRONTEND</span>
                        <p style="font-size:12px; color:#888; margin-top:10px;">React-SPA (Vite), Wouter, Mobile-First PWA</p>
                    </div>
                    <div class="architecture-box">
                        <i class="fa-solid fa-database"></i><span>BACKEND</span>
                        <p style="font-size:12px; color:#888; margin-top:10px;">Express.js REST, Drizzle ORM, Supabase (PostgreSQL)</p>
                    </div>
                    <div class="architecture-box">
                        <i class="fa-solid fa-plug"></i><span>INTEGRATIONS</span>
                        <p style="font-size:12px; color:#888; margin-top:10px;">TikTok Scraper, Monday GraphQL, OpenAI, Frame.io</p>
                    </div>
                    <div class="architecture-box" style="border-color: var(--brand);">
                        <i class="fa-solid fa-file-invoice-dollar"></i><span>FINANCE OPS</span>
                        <p style="font-size:12px; color:#888; margin-top:10px;">Candis, Billomat, Scoro</p>
                    </div>
                </div>
                <div class="speaker-notes" style="width: 100%; text-align: left; margin-top: 40px;">
                    <div class="notes-title">Sprechernotizen</div>
                    <p>„Die Plattform ist state-of-the-art gebaut. Durch die tiefe API-Verknüpfung mit Candis und Billomat verschmilzt das operative Kampagnengeschäft direkt mit der Agentur-Buchhaltung. Volle Kostenkontrolle, live.“</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>14 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Security & Data Quality</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Datenqualität by Design</h2>
                    <ul>
                        <li><strong>RBAC Berechtigungen:</strong> Granulares 4-Rollen-System (Viewer, Editor, Admin, Super Admin) über 12 Ressourcen-Kategorien (Frontend & Backend).</li>
                        <li><strong>Anti-Loop Validierung:</strong> Mechanismen verhindern Daten-Korruption durch fehlerhafte Hashtag-Schleifen beim Crawling.</li>
                        <li><strong>Exponential Backoff:</strong> Intelligente Retry-Logik verhindert Ausfälle bei API-Rate-Limits der externen Plattformen.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Für große Corporate-Kunden müssen wir ISO-Standards denken. Unser Rechtesystem garantiert, dass kein Datenleck entsteht. Die technischen Sicherheitsnetze sorgen dafür, dass die Zahlen in unseren Reports 100% belastbar sind.“</p>
                    </div>
                </div>
                <div class="visual-side" style="align-items: center;">
                    <div style="font-size: 150px; color: rgba(255,73,0,0.1);"><i class="fa-solid fa-shield-halved"></i></div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>15 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Case Study A</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Almette: Skalierung auf Steroiden</h2>
                    <p class="subtitle">Kampagnen-Volumen im Massenmarkt generieren</p>
                    <p class="lead">Über automatisierte Discovery und die Activation Pipeline haben wir 115 Videos koordiniert – in nur 4 Wochen.</p>
                    <ul>
                        <li>Zeitraum: 19.01. – 19.02.2026</li>
                        <li>Volumen: 115 Content Pieces sauber prozessiert.</li>
                        <li>Ergebnis: Ein massiver Branding-Impact mit <strong>>660k echten Interaktionen</strong>.</li>
                    </ul>
                </div>
                <div class="visual-side">
                    <div class="kpi-grid">
                        <div class="kpi-card highlight" style="grid-column: span 2;">
                            <div class="kpi-val" style="font-size: 72px;">113.3M</div>
                            <div class="kpi-lbl" style="color:#fff;">Generierte Views in 1 Monat</div>
                        </div>
                        <div class="kpi-card"><div class="kpi-val" style="font-size: 32px;">595k</div><div class="kpi-lbl">Likes</div></div>
                        <div class="kpi-card"><div class="kpi-val" style="font-size: 32px;">17.6k</div><div class="kpi-lbl">Shares</div></div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>16 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Case Study B</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Frisia: Aus Daten wird Strategie</h2>
                    <p class="subtitle">DEPARTD Lens AI in Aktion</p>
                    <p class="lead">Quantität allein reicht nicht. Durch KI-gestütztes Sourcing und exakte Content-DNA-Vorgaben haben wir die Benchmark zertrümmert.</p>
                    <ul>
                        <li>Ansatz: 75 gezielte Activations basierend auf historischen Engine-Daten.</li>
                        <li>Native Platzierung in Nischen-Communities.</li>
                        <li>Die Folge: Höchste organische Bindung zum Produkt.</li>
                    </ul>
                </div>
                <div class="visual-side">
                    <div class="kpi-grid">
                        <div class="kpi-card" style="border-color: #333;">
                            <div class="kpi-val" style="font-size: 42px; color: #fff;">75</div>
                            <div class="kpi-lbl">Activations</div>
                        </div>
                        <div class="kpi-card highlight">
                            <div class="kpi-val" style="font-size: 42px;">4.94%</div>
                            <div class="kpi-lbl" style="color:#fff;">Engagement Rate (vs. 3% Target)</div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>17 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">Case Study C</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Overhead-Killer: Reporting</h2>
                    <p class="subtitle">Kundenvertrauen durch Live-Transparenz</p>
                    <p class="lead">Das Account Management war historisch ein massiver Kostenfresser. Die Engine wandelt diese Rüstzeit in reine Projektmarge um.</p>
                    <ul>
                        <li><strong>Vorher:</strong> Mehrere Mitarbeiter investierten wöchentlich Stunden in das manuelle Erstellen von PowerPoints und Screenshot-Collagen.</li>
                        <li><strong>Nachher:</strong> Der Kunde loggt sich ein, oder das System generiert das Deck auf Knopfdruck.</li>
                    </ul>
                </div>
                <div class="visual-side">
                    <div style="display:flex; flex-direction:column; gap: 20px;">
                        <div style="background:#111; padding: 20px; border-radius: 8px; border-left: 4px solid #444;">
                            <p style="color:#888; font-size:14px; text-transform:uppercase;">Historischer Aufwand</p>
                            <h3 style="font-size:32px; color:#fff; margin:0;">Zahlreiche Stunden</h3>
                        </div>
                        <div style="display:flex; justify-content:center; color:var(--brand);"><i class="fa-solid fa-arrow-down"></i></div>
                        <div style="background:rgba(255,73,0,0.1); padding: 20px; border-radius: 8px; border-left: 4px solid var(--brand);">
                            <p style="color:var(--brand); font-size:14px; text-transform:uppercase;">Mit DEPARTD Engine</p>
                            <h3 style="font-size:42px; color:var(--brand); margin:0;">~ 1 Minute</h3>
                        </div>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>18 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">The Bottom Line</div></div>
            <div class="content center">
                <h2>Financial Impact: H1 Performance</h2>
                <p class="lead" style="text-align: center;">Die Kombination aus automatisiertem Handling und datenbasiertem Creator-Einkauf resultiert in einer Marge, die Agentur-Benchmarks (15-25%) pulverisiert.</p>
                
                <div class="kpi-grid" style="grid-template-columns: 1fr 1fr 1fr; max-width: 1000px; margin-top: 20px;">
                    <div class="kpi-card" style="text-align:center; border-color:#333;">
                        <div class="kpi-val" style="font-size:40px; color:#fff;">367.836 €</div>
                        <div class="kpi-lbl">Gesamtbudget H1</div>
                    </div>
                    <div class="kpi-card" style="text-align:center; border-color:#333;">
                        <div class="kpi-val" style="font-size:40px; color:#fff;">~32 %</div>
                        <div class="kpi-lbl">Creator Kosten-Quote</div>
                    </div>
                    <div class="kpi-card highlight" style="text-align:center;">
                        <div class="kpi-val" style="font-size:48px;">47,16 %</div>
                        <div class="kpi-lbl" style="color:#fff;">Operative EBIT-Marge</div>
                    </div>
                </div>
                <div class="speaker-notes" style="width: 100%; text-align: left; margin-top: 40px;">
                    <div class="notes-title">Sprechernotizen</div>
                    <p>„Hier laufen alle Fäden zusammen. Weil das System uns erlaubt, extrem effizient einzukaufen und gleichzeitig die Personalkosten für das Handling drastisch zu senken, bleiben am Ende über 47% operatives EBIT stehen.“</p>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>19 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">H2 2026 Outlook</div></div>
            <div class="content">
                <div class="text-side">
                    <h2>Skalierungs-Setup für H2</h2>
                    <ul>
                        <li><strong>Eingeloggte Pipeline:</strong> Über 502k € Volumen stehen für das zweite Halbjahr fest (inkl. Storck Knoppers/Mamba).</li>
                        <li><strong>Triangel-Setup:</strong> Operative Abwicklung gesichert durch Robert (Lead), Uljana (Camp. Mgmt) und Matthias (ab Juli).</li>
                        <li><strong>Roadmap-Vision:</strong> Ausbau der KI zur vollautomatischen Budget-Allokations-Empfehlung in Pitches.</li>
                    </ul>
                    <div class="speaker-notes">
                        <div class="notes-title">Sprechernotizen</div>
                        <p>„Die Maschine läuft. Mit dem Onboarding von Matthias im Juli haben wir die perfekte Manpower, um das massive H2-Volumen abzuwickeln. Das Setup steht, das System skaliert.“</p>
                    </div>
                </div>
                <div class="visual-side">
                    <div class="kpi-card highlight" style="text-align: center; padding: 60px;">
                        <p style="color: #fff; font-size: 16px; text-transform: uppercase; letter-spacing: 2px;">Secured H2 Pipeline</p>
                        <div class="kpi-val" style="font-size: 80px; margin: 20px 0;">> 502k €</div>
                        <p style="color: #fff; opacity: 0.8;">Bereit zur Prozessierung</p>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>20 / 22</div></div>
        </section>

        <section class="slide">
            <div class="header"><div class="logo">DEPARTD <span>ENGINE</span></div><div class="tagline">The Moat</div></div>
            <div class="content center">
                <h2>Der unkopierbare Wettbewerbsvorteil</h2>
                <div class="kpi-grid" style="grid-template-columns: 1fr 1fr; max-width: 900px; margin-top: 20px;">
                    <div class="kpi-card" style="border-left: 4px solid var(--brand);">
                        <h3 style="color:#fff;">Proprietäre Daten</h3>
                        <p style="color:#aaa; font-size:16px;">Jede Kampagne macht das System klüger. Dieser Datenschatz ist von externen Konkurrenten nicht kaufbar.</p>
                    </div>
                    <div class="kpi-card" style="border-left: 4px solid var(--brand);">
                        <h3 style="color:#fff;">Lock-in Effekt</h3>
                        <p style="color:#aaa; font-size:16px;">Premium-Reporting und Kunden-Portals erzeugen gewaltige Wechselkosten für Brands.</p>
                    </div>
                    <div class="kpi-card" style="border-left: 4px solid var(--brand);">
                        <h3 style="color:#fff;">Kostenführerschaft</h3>
                        <p style="color:#aaa; font-size:16px;">Automatisierung erlaubt uns, bei gleicher Media-Qualität höhere Margen zu fahren als jede klassische Agentur.</p>
                    </div>
                    <div class="kpi-card" style="border-left: 4px solid var(--brand);">
                        <h3 style="color:#fff;">KI mit Substanz</h3>
                        <p style="color:#aaa; font-size:16px;">Kein Buzzword-Bingo. Echte Embedding-Analysen (Content DNA) beweisen dem Kunden unseren strategischen Wert.</p>
                    </div>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>21 / 22</div></div>
        </section>

        <section class="slide" style="background: var(--bg-dark);">
            <div class="content center" style="justify-content: center;">
                <p class="subtitle" style="color: var(--brand);">DEPARTD GmbH | Strategy & Campaigning</p>
                <h1 style="font-size: 90px; margin: 30px 0;">READY TO <br><span style="color: var(--brand);">SCALE.</span></h1>
                <p style="color: var(--text-muted); font-size: 20px;">Fragen & gemeinsame strategische H2-Planung.</p>
                
                <div style="margin-top: 60px; display: flex; gap: 30px; color: #555; font-weight: bold; letter-spacing: 1px;">
                    <span>ROBERT</span> • <span>ULJANA</span> • <span>MATTHIAS</span>
                </div>
            </div>
            <div class="footer"><div>DEPARTD GmbH © 2026</div><div>22 / 22</div></div>
        </section>

    </div>

    <div class="controls">
        <button class="btn-nav" id="prevBtn"><i class="fa-solid fa-chevron-left"></i></button>
        <button class="btn-nav" id="nextBtn"><i class="fa-solid fa-chevron-right"></i></button>
    </div>
    
    <div class="progress-bar" id="progressBar" style="width: 4.54%;"></div>

    <script>
        const container = document.getElementById('presentation-container');
        const slides = document.querySelectorAll('.slide');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const progressBar = document.getElementById('progressBar');
        let currentSlide = 0;
        const totalSlides = slides.length;

        function updateSlide() {
            container.style.transform = `translateX(-${currentSlide * 100}vw)`;
            const progress = ((currentSlide + 1) / totalSlides) * 100;
            progressBar.style.width = `${progress}%`;
        }

        function nextSlide() {
            if (currentSlide < totalSlides - 1) {
                currentSlide++;
                updateSlide();
            }
        }

        function prevSlide() {
            if (currentSlide > 0) {
                currentSlide--;
                updateSlide();
            }
        }

        nextBtn.addEventListener('click', nextSlide);
        prevBtn.addEventListener('click', prevSlide);

        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowRight' || e.key === 'ArrowDown' || e.key === ' ') nextSlide();
            if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') prevSlide();
        });
    </script>

</body>
</html>
