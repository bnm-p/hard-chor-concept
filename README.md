# Technisches Konzept: Hard-Chor Website-Relaunch & CMS-Migration

## 1. Bestandsaufnahme & Analyse der Altseite

Bevor mit dem Relaunch begonnen wird, analysieren wir die bestehende WordPress-Website im Detail:

- **Content-Inventur**: Erfassung aller Seiten, Beiträge, Medienelemente, Downloads, Menüs, Widgets und benutzerdefinierten Inhaltstypen.
- **Strukturierte vs. manuell gepflegte Daten**: Welche Inhalte können automatisiert exportiert werden, welche benötigen manuelle Überarbeitung?
- **Technische Abhängigkeiten**: Dokumentation eingesetzter Plugins, Formulare, Benutzerrollen und Spezialfunktionen wie Kalender, Newsletter oder Mehrsprachigkeit.
- **Sonderlösungen erkennen**: Alles, was nicht dem WordPress-Standard entspricht, wird identifiziert und gezielt für die Migration geplant.

## 2. Zielsystem definieren: PayloadCMS als moderne Headless-Lösung

Für das neue System setzen wir auf **PayloadCMS**, ein leistungsstarkes, Headless CMS auf Basis von Node.js und MongoDB. Die Entscheidung basiert auf folgenden Kriterien:

- **Benutzerfreundlichkeit** durch eine moderne, intuitive Admin-Oberfläche  
- **Hohe Wartbarkeit** durch klare Strukturen und Entwicklerfokus  
- **Sicherheit** durch ein reduziertes Angriffsprofil ohne unnötige Plugins oder PHP-Abhängigkeiten  
- **Herausragende Performance** durch Headless-Architektur und API-First-Ansatz  
- **Erweiterbarkeit & Anpassbarkeit** durch vollständige Codekontrolle (Open Source, komplett via JavaScript/TypeScript anpassbar)  

## 3. Migrationsstrategie entwickeln

Die Migration erfolgt in zwei Stufen:

- **Automatisierter Import (wo möglich)**: Inhalte wie Beiträge, Seiten und Medienelemente (Bilder, PDFs) werden via Export/Import (z. B. JSON, XML, CSV) in das neue System überführt.
- **Manuelle Überarbeitung bei komplexen Inhalten**: Inhaltstypen mit individueller Logik oder Spezialfeldern (z. B. Eventsysteme, verschachtelte Layouts) werden händisch migriert, um Struktur, Qualität und Semantik optimal zu übernehmen.
- **URL-Mapping & Weiterleitungen**: Permalinks der alten Seite werden analysiert und über 301-Redirects korrekt auf neue Pfade umgeleitet.
- **Menüstruktur & Informationsarchitektur**: Das neue System bildet alle wichtigen Navigationspunkte ab – ggf. verbessert im Sinne von UX und SEO.

## 4. Technische Umsetzung & Setup

### Server-Einrichtung auf Contabo (Shared CPU)

Der neue Server wird von Grund auf neu aufgesetzt. Dazu gehören:

- Sicherheitskonfiguration (Firewall, SSH Hardening, Fail2Ban, automatische Updates)
- Node.js-Umgebung und PayloadCMS-Deployment (inkl. PM2 oder Docker)
- HTTPS-Absicherung via Let's Encrypt
- Datenbank (MongoDB) Konfiguration
- Caching & Performance-Optimierungen (z. B. nginx Reverse Proxy)

### PayloadCMS-Projekt aufsetzen

- Einrichtung der Datenstruktur (Collections, Globals, Media Uploads etc.)
- Entwicklung maßgeschneiderter Templates & Frontend-Komponenten (z. B. via Next.js oder Astro)
- Aufbau der Seitenstruktur und Integration aller Inhalte & Medien

## 5. Qualitätssicherung (QA)

Vor dem Livegang wird die neue Seite umfassend geprüft:

- **Funktionstests** (Formulare, Suche, dynamische Inhalte)
- **Responsive Verhalten** auf mobilen Geräten
- **Performance** (Ladezeiten, API-Antwortzeiten)
- **Kompatibilität** in allen gängigen Browsern
- **Barrierefreiheit & technische SEO**
- **Redirect-Check** (301 Weiterleitungen) und Linkprüfung

## 6. Go-Live & Monitoring

- **Umstellung der Domain** auf das neue System (inkl. DNS-Konfiguration und SSL)
- **Technisches Setup für Live-Betrieb**:
  - Backup-Routinen
  - Caching-Strategien (z. B. SSR-/ISR-Mechaniken oder CDN)
  - Sicherheitsmaßnahmen (u. a. Firewall, Security Header, Rate Limiting)
  - Server-Monitoring (Uptime, Ressourcenlast, Fehlererkennung)

- **Begleitendes Monitoring** in den ersten Wochen nach Launch:
  - Logging & Fehlererkennung
  - Nutzerverhalten & Ladezeiten beobachten

- **Nach erfolgreichem finalen Check (QA)**:
  - Aktualisierung der **Sitemap** und Einreichung bei **Google Search Console**
  - Kontrolle der Indexierung und der neuen Seitenstruktur
  - Umsetzung einer **Reindexierung wichtiger Seiten** (ggf. manuell beschleunigt)
  - Prüfung und Pflege der Snippets, Metadaten und Social Previews

---

## Warum PayloadCMS statt WordPress?

### Sicherheit  
Keine klassische Angriffsfläche wie bei WordPress (z. B. keine PHP-Plugins, keine SQL-Injection-Risiken).

### Performance  
Durch Headless-Architektur werden Inhalte über eine optimierte API ausgeliefert – ideal für moderne Frameworks wie Next.js, Nuxt oder Astro.

### Wartbarkeit & Erweiterbarkeit  
Keine Blackbox-Plugins: Payload ist komplett offen und entwicklerfreundlich. Erweiterungen, Integrationen und Automatisierungen sind sauber im Code steuerbar.

### Content-Struktur  
Statt unübersichtlicher Plugin-Logik bietet Payload strukturierte Collections mit sauberen Datenmodellen und Relationen – ideal für langfristige Skalierung und Qualitätssicherung.

### Developer Experience  
Modernes Stack (Node.js, MongoDB, TypeScript, REST/GraphQL API). Entwickler behalten die volle Kontrolle, wodurch langfristig weniger Wartungskosten und mehr Flexibilität entstehen.

### Bessere Zukunftsfähigkeit  
Headless bedeutet: Frontend und Backend sind entkoppelt. Das erlaubt zukunftssichere Weiterentwicklungen, z. B. PWA, Mobile Apps oder Multi-Channel-Lösungen.
