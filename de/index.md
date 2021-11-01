---
layout: Post
title: Web Vitals
description: Wesentliche Kennzahlen für eine fehlerfreie Website
hero: image/admin/BHaoqqR73jDWe6FL2kfw.png
authors:
  - philipwalton
date: '2020-04-30'
updated: '2020-07-21'
tags:
  - Metriken
  - Leistung
  - web-vitals
---

Die Optimierung der Qualität der Benutzererfahrung ist der Schlüssel zum langfristigen Erfolg jeder Website im Web. Egal, ob Sie Geschäftsinhaber, Vermarkter oder Entwickler sind, Web Vitals kann Ihnen dabei helfen, die Erfahrung Ihrer Website zu quantifizieren und Verbesserungsmöglichkeiten zu identifizieren.

## Überblick

Web Vitals ist eine Initiative von Google, um einheitliche Leitlinien für Qualitätssignale bereitzustellen, die für die Bereitstellung einer großartigen Benutzererfahrung im Web unerlässlich sind.

Google hat im Laufe der Jahre eine Reihe von Tools bereitgestellt, um die Leistung zu messen und zu berichten. Einige Entwickler sind Experten im Umgang mit diesen Tools, während andere es schwierig fanden, mit der Fülle von Tools und Metriken Schritt zu halten.

Websitebesitzer sollten keine Leistungsgurus sein müssen, um die Qualität der Erfahrung zu verstehen, die sie ihren Benutzern bieten. Die Web Vitals-Initiative zielt darauf ab, die Landschaft zu vereinfachen und Websites dabei zu helfen, sich auf die wichtigsten Metriken zu konzentrieren, die **Core Web Vitals** .

## Core Web Vitals

Core Web Vitals sind die Teilmenge der Web Vitals, die für alle Webseiten gelten, von allen Websitebesitzern gemessen werden sollten und in allen Google-Tools angezeigt werden. Jedes der Core Web Vitals repräsentiert eine bestimmte Facette der Benutzererfahrung, ist [im Feld](/user-centric-performance-metrics/#how-metrics-are-measured) messbar und spiegelt die reale Erfahrung eines kritischen [benutzerorientierten](/user-centric-performance-metrics/#how-metrics-are-measured) Ergebnisses wider.

Die Metriken, aus denen Core Web Vitals besteht, werden [sich im](#evolving-web-vitals) Laufe der Zeit weiterentwickeln. Das aktuelle Set für 2020 konzentriert sich auf drei Aspekte der Benutzererfahrung – *Laden* , *Interaktivität* und *visuelle Stabilität* – und umfasst die folgenden Metriken (und ihre jeweiligen Schwellenwerte):

<div class="w-stack w-stack--center w-stack--md">
<img src="lcp_ux.svg" width="400px" height="350px" alt="Größte Empfehlungen für Contentful Paint-Schwellenwerte"><img src="fid_ux.svg" width="400px" height="350px" alt="Empfehlungen zum Schwellenwert für die erste Eingangsverzögerung"><img src="cls_ux.svg" width="400px" height="350px" alt="Empfehlungen für Schwellenwerte für kumulative Layoutverschiebung">
</div>

- **[Größter gehalt Paint (LCP)](/lcp/)** : Maßnahmen *Ladeleistung.* Um eine gute Benutzererfahrung zu bieten, sollte LCP innerhalb von **2,5 Sekunden** nach dem ersten Laden der Seite erfolgen.
- **[First Input Delay (FID)](/fid/)** : misst die *Interaktivität* . Um eine gute Benutzererfahrung zu bieten, sollten Seiten eine FID von weniger als **100 Millisekunden haben** .
- **[Kumulative Layoutverschiebung (CLS)](/cls/)** : misst die *visuelle Stabilität* . Um eine gute Benutzererfahrung zu bieten, sollten Seiten einen CLS von weniger als **0,1 beibehalten.**

Um sicherzustellen, dass Sie für jeden der oben genannten Messwerte das empfohlene Ziel für die meisten Ihrer Nutzer erreichen, ist ein guter Schwellenwert für die Messung das **75. Perzentil** der Seitenladevorgänge, segmentiert auf Mobilgeräte und Desktop-Geräte.

Tools, die die Einhaltung von Core Web Vitals bewerten, sollten eine Seitenübergabe in Betracht ziehen, wenn sie die empfohlenen Ziele im 75. Perzentil für alle der oben genannten drei Metriken erfüllt.

{% Aside %} Weitere Informationen zu Forschung und Methodik dieser Empfehlungen finden Sie unter: [Definieren der Schwellenwerte für die Core Web Vitals-Metriken](/defining-core-web-vitals-thresholds/) {% endAside %}

### Tools zum Messen und Berichten von Core Web Vitals

Google ist der Ansicht, dass die Core Web Vitals für alle Web-Erlebnisse von entscheidender Bedeutung sind. Aus diesem Grund ist es bestrebt, diese Metriken [in all seinen beliebten Tools zu veröffentlichen](/vitals-tools/) . In den folgenden Abschnitten wird beschrieben, welche Tools die Core Web Vitals unterstützen.

#### Feldtools zur Messung von Core Web Vitals

Der[Chrome User Experience Report](https://developers.google.com/web/tools/chrome-user-experience-report) sammelt anonymisierte, echte Nutzermessdaten für jeden Core Web Vital. Diese Daten ermöglichen es Websitebesitzern, ihre Leistung schnell zu bewerten, ohne dass sie Analysen auf ihren Seiten manuell instrumentieren müssen, und unterstützen Tools wie [PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) und den [Core Web Vitals-Bericht der](https://support.google.com/webmasters/answer/9205520) Search Console .

<div class="w-table-wrapper">
  <table>
    <tr>
      <td> </td>
      <td>LCP</td>
      <td>FID</td>
      <td>CLS</td>
    </tr>
    <tr>
      <td><a href="https://developers.google.com/web/tools/chrome-user-experience-report">Bericht zur Chrome-Nutzererfahrung</a></td>
      <td>✔</td>
      <td>✔</td>
      <td>✔</td>
    </tr>
    <tr>
      <td><a href="https://developers.google.com/speed/pagespeed/insights/">PageSpeed-Einblicke</a></td>
      <td>✔</td>
      <td>✔</td>
      <td>✔</td>
    </tr>
    <tr>
      <td><a href="https://support.google.com/webmasters/answer/9205520">Search Console (Core Web Vitals-Bericht)</a></td>
      <td>✔</td>
      <td>✔</td>
      <td>✔</td>
    </tr>
  </table>
</div>

{% Aside %} Eine Anleitung zur Verwendung dieser Tools und das richtige Tool für Ihren Anwendungsfall finden Sie unter: [Erste Schritte mit der Messung von Web Vitals](/vitals-measurement-getting-started/) {% endAside %}

Die vom Chrome User Experience Report bereitgestellten Daten bieten eine schnelle Möglichkeit, die Leistung von Websites zu bewerten, bieten jedoch nicht die detaillierte Telemetrie pro Seitenaufruf, die häufig erforderlich ist, um Regressionen genau zu diagnostizieren, zu überwachen und schnell darauf zu reagieren. Daher empfehlen wir dringend, dass Websites eine eigene Überwachung der realen Benutzer einrichten.

#### Messen Sie Core Web Vitals in JavaScript

Jeder der Core Web Vitals kann in JavaScript mithilfe von Standard-Web-APIs gemessen werden.

Der einfachste Weg, alle Core Web Vitals zu messen, besteht darin, die [JavaScript-Bibliothek web-vitals zu](https://github.com/GoogleChrome/web-vitals) verwenden, einen kleinen, produktionsbereiten Wrapper um die zugrunde liegenden Web-APIs, der jede Metrik so misst, dass sie genau den Berichten aller Oben aufgeführte Google-Tools.

Mit der [Web-Vitals-](https://github.com/GoogleChrome/web-vitals) Bibliothek ist die Messung jeder Metrik so einfach wie das Aufrufen einer einzelnen Funktion (die vollständige [Verwendung](https://github.com/GoogleChrome/web-vitals#usage) und [API-](https://github.com/GoogleChrome/web-vitals#api) Details finden Sie in der Dokumentation):

```js
import {getCLS, getFID, getLCP} from 'web-vitals';

function sendToAnalytics(metric) {
  const body = JSON.stringify(metric);
  // Use `navigator.sendBeacon()` if available, falling back to `fetch()`.
  (navigator.sendBeacon && navigator.sendBeacon('/analytics', body)) ||
      fetch('/analytics', {body, method: 'POST', keepalive: true});
}

getCLS(sendToAnalytics);
getFID(sendToAnalytics);
getLCP(sendToAnalytics);
```

Nachdem Sie Ihre Site so konfiguriert haben, dass sie die [Web-Vitals-](https://github.com/GoogleChrome/web-vitals) Bibliothek verwendet, um Ihre Core Web Vitals-Daten zu messen und an einen Analyseendpunkt zu senden, besteht der nächste Schritt darin, diese Daten zu aggregieren und zu berichten, um zu sehen, ob Ihre Seiten die empfohlenen Schwellenwerte für . erfüllen mindestens 75% der Seitenaufrufe.

Während einige Analyseanbieter eine integrierte Unterstützung für Core Web Vitals-Metriken bieten, sollten selbst diejenigen, die dies nicht tun, grundlegende benutzerdefinierte Metrikfunktionen enthalten, mit denen Sie Core Web Vitals in ihrem Tool messen können.

Ein Beispiel hierfür ist der [Web Vitals Report](https://github.com/GoogleChromeLabs/web-vitals-report) , mit dem Websitebesitzer ihre Core Web Vitals mithilfe von Google Analytics messen können. Eine Anleitung zum Messen von Core Web Vitals mit anderen Analysetools finden Sie unter [Best Practices zum Messen von Web Vitals im Feld](/vitals-field-measurement-best-practices/) .

[Sie können mit der Web Vitals Chrome-Erweiterung](https://github.com/GoogleChrome/web-vitals-extension) auch Berichte zu jedem der Core Web Vitals erstellen, ohne Code zu schreiben. Diese Erweiterung verwendet die [Web-Vitals-](https://github.com/GoogleChrome/web-vitals) Bibliothek, um jede dieser Metriken zu messen und sie den Benutzern beim Surfen im Web anzuzeigen.

Diese Erweiterung kann hilfreich sein, um die Leistung Ihrer eigenen Websites, der Websites Ihrer Mitbewerber und des Webs insgesamt zu verstehen.

<div class="w-table-wrapper">
  <table>
    <thead>
      <tr>
        <th> </th>
        <th>LCP</th>
        <th>FID</th>
        <th>CLS</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><a href="https://github.com/GoogleChrome/web-vitals">web-vitals</a></td>
        <td>✔</td>
        <td>✔</td>
        <td>✔</td>
      </tr>
      <tr>
        <td><a href="https://github.com/GoogleChrome/web-vitals-extension">Web Vitals-Erweiterung</a></td>
        <td>✔</td>
        <td>✔</td>
        <td>✔</td>
      </tr>
    </tbody>
  </table>
</div>

Alternativ können Entwickler, die diese Metriken lieber direkt über die zugrunde liegenden Web-APIs messen möchten, diese Metrikleitfäden für Implementierungsdetails lesen:

- [LCP in JavaScript messen](/lcp/#measure-lcp-in-javascript)
- [FID in JavaScript messen](/fid/#measure-fid-in-javascript)
- [CLS in JavaScript messen](/cls/#measure-cls-in-javascript)

{% Aside %} Weitere Anleitungen zum Messen dieser Metriken mit beliebten Analysediensten (oder Ihren eigenen [internen Analysetools) finden Sie unter: Best Practices zum Messen von Web Vitals im Feld](/vitals-field-measurement-best-practices/) {% endAside %}

#### Labortools zur Messung von Core Web Vitals

Während alle Core Web Vitals in erster Linie Feldmetriken sind, sind viele von ihnen auch im Labor messbar.

Labormessungen sind der beste Weg, um die Leistung von Funktionen während der Entwicklung zu testen – bevor sie für Benutzer freigegeben werden. Dies ist auch der beste Weg, um Leistungsrückgänge zu erkennen, bevor sie auftreten.

Die folgenden Tools können verwendet werden, um die Core Web Vitals in einer Laborumgebung zu messen:

<div class="w-table-wrapper">
  <table>
    <thead>
      <tr>
        <th> </th>
        <th>LCP</th>
        <th>FID</th>
        <th>CLS</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><a href="https://developers.google.com/web/tools/chrome-devtools">Chrome DevTools</a></td>
        <td>✔</td>
        <td>✘ ( <a href="/tbt/">stattdessen TBT</a> verwenden)</td>
        <td>✔</td>
      </tr>
      <tr>
        <td><a href="https://developers.google.com/web/tools/lighthouse">Leuchtturm</a></td>
        <td>✔</td>
        <td>✘ ( <a href="/tbt/">stattdessen TBT</a> verwenden)</td>
        <td>✔</td>
      </tr>
    </tbody>
  </table>
</div>

{% Aside %} Tools wie Lighthouse, die Seiten in einer simulierten Umgebung ohne Benutzer laden, können die FID nicht messen (es gibt keine Benutzereingabe). Die Metrik der Total Blocking Time (TBT) ist jedoch im Labor messbar und ein ausgezeichneter Proxy für FID. Leistungsoptimierungen, die die TBT im Labor verbessern, sollten die FID im Feld verbessern (siehe Leistungsempfehlungen unten). {% endAside %}

Labormessungen sind zwar ein wesentlicher Bestandteil der Bereitstellung großartiger Erfahrungen, ersetzen jedoch nicht die Feldmessungen.

Die Leistung einer Site kann je nach den Gerätefunktionen eines Benutzers, seinen Netzwerkbedingungen, den anderen Prozessen, die möglicherweise auf dem Gerät ausgeführt werden, und der Art und Weise, wie er mit der Seite interagiert, stark variieren. Tatsächlich kann die Bewertung jeder der Core Web Vitals-Metriken durch die Benutzerinteraktion beeinflusst werden. Nur Feldmessungen können das vollständige Bild genau erfassen.

### Empfehlungen zur Verbesserung Ihrer Punktzahl

Nachdem Sie die Core Web Vitals gemessen und verbesserungswürdige Bereiche identifiziert haben, besteht der nächste Schritt in der Optimierung. Die folgenden Leitfäden bieten spezifische Empfehlungen zur Optimierung Ihrer Seiten für jeden der Core Web Vitals:

- [LCP optimieren](/optimize-lcp/)
- [FID optimieren](/optimize-fid/)
- [CLS optimieren](/optimize-cls/)

## Andere Web-Vitals

Während die Core Web Vitals die entscheidenden Metriken für das Verständnis und die Bereitstellung einer großartigen Benutzererfahrung sind, gibt es noch andere wichtige Metriken.

Diese anderen Web Vitals dienen oft als Proxy- oder ergänzende Metriken für die Core Web Vitals, um einen größeren Teil der Erfahrung zu erfassen oder bei der Diagnose eines bestimmten Problems zu helfen.

For example, the metrics [Time to First Byte (TTFB)](/time-to-first-byte/) and [First Contentful Paint (FCP)](/fcp/) are both vital aspects of the *loading* experience, and are both useful in diagnosing issues with LCP (slow [server response times](/overloaded-server/) or [render-blocking resources](/render-blocking-resources/), respectively).

Ebenso sind Metriken wie [Total Blocking Time (TBT)](/tbt/) und [Time to Interactive (TTI)](/tti/) Labormetriken, die für das Erkennen und Diagnostizieren potenzieller *Interaktivitätsprobleme* , die sich auf FID auswirken, von entscheidender Bedeutung sind. Sie sind jedoch nicht Teil des Core Web Vitals-Sets, da sie weder vor Ort messbar sind noch ein [benutzerorientiertes](/user-centric-performance-metrics/#how-metrics-are-measured) Ergebnis widerspiegeln.

## Weiterentwicklung von Web Vitals

Web Vitals und Core Web Vitals stellen die besten verfügbaren Signale dar, die Entwickler heute haben, um die Qualität der Erfahrung im Web zu messen, aber diese Signale sind nicht perfekt und zukünftige Verbesserungen oder Ergänzungen sind zu erwarten.

Die **Core Web Vitals** sind für alle Webseiten relevant und werden in allen relevanten Google-Tools vorgestellt. Änderungen an diesen Metriken werden weitreichende Auswirkungen haben; Daher sollten Entwickler davon ausgehen, dass die Definitionen und Schwellenwerte der Core Web Vitals stabil sind und dass Aktualisierungen im Voraus angekündigt werden und eine vorhersehbare jährliche Häufigkeit aufweisen.

Die anderen Web Vitals sind oft kontext- oder toolspezifisch und können experimenteller als die Core Web Vitals sein. Daher können sich ihre Definitionen und Schwellenwerte häufiger ändern.

Für alle Web Vitals werden Änderungen in diesem öffentlichen [CHANGELOG](http://bit.ly/chrome-speed-metrics-changelog) klar dokumentiert.
