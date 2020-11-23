---
id: debugging
title: Debugging
sidebar_label: Debugging
---
> Tipps und Tricks zum Thema Debugging von Angular Anwendungen

## Entwickler-Tools der Browser (F12)

### Allgemeine Utilities unabhängig von Angular

Ein im Elemente-Baum (Elements-Tab im Chrome, Inspector-Tab bei Firefox) ausgewähltes DOM-Element steht auf der Entwickler-Console unter dem Variablen-Namen ```$0``` zur Verfügung.

Im Chrome gilt zudem: nach einer weiteren Selektion eines anderen Elements ist nun natürlich eine Referenz auf das DOM-Objekt dieses neuen Elements in der Variablen ```$0``` abgelegt und zusätzlich das vorherige Element über ```$1``` abrufbar. Das funktioniert für die letzten vier Selektionen (also bis zu ```$4```).

Außerdem stehen mittlerweile in allen Browsern Selektor-Funktionen zur Verfügung über die Namen ```$``` (äquivalent zu ```document.querySelector```) und ```$$``` (ähnlich wie ```document.querySelectorAll```).

Links:
* [Chrome Console Utilities](https://developers.google.com/web/tools/chrome-devtools/console/utilities)
* [Firefox CLI](https://developer.mozilla.org/en-US/docs/Tools/Web_Console/The_command_line_interpreter)

### Angular Utilities

:::caution
Achtung. Mit Angular 10 hat sich die Schnittstelle des globalen ```ng```-Objektes
komplett geändert. Die ```probe```-Methode existiert nicht mehr, stattdessen eine
Reihe von get-Methoden. Noch habe ich keine Dokumentation dazu gefunden und konnte
diese auch noch nicht weiter evaluieren.
:::

Angular stellt das globale Objekt ```ng``` bereit. Die ```probe```-Methode dieses Objektes gibt uns für ein DOM-Element (also zum Beispiel das aktuelle ```$0``` von oben) das DebugElement zurück. Darüber lässt sich
nun die Instanz der zugehörigen Component analysieren (Property ```componentInstance```) oder zum Beispiel
auch ein Event auslösen (Methode ```triggerEventHandler```).

Ein weiteres Debug-Tool ist der Profiler. Es ist bisher das einzige Tool, das über die Methode
```enableDebugTools``` aus dem Browser-Module freigeschaltet werden kann. Das Freischalten geschieht üblicherweise
in der ```main.ts```.

    platformBrowserDynamic().bootstrapModule(AppModule)
      .then(moduleRef => {
        const appRef = moduleRef.injector.get(ApplicationRef);
        const appComponent = appRef.components[0];
        enableDebugTools(appComponent);
      })
      .catch(err => console.error(err));

Siehe dazu: [Tools Doc](https://github.com/angular/angular/blob/master/docs/TOOLS.md)

Über den Profiler lassen sich ChangeDetection-Läufe analysieren und aufzeichnen zur weiteren Analyse in den Performance-Tabs der Browser-Entwicklerconsole.

Einfacher Timing Durchlauf:

    ng.profiler.timeChangeDetection()

Mit Aufzeichnung:

    ng.profiler.timeChangeDetection({record: true})

Letzteres funktioniert zur Zeit weder im Chrome noch im Firefox. Bei ersterem sehe ich gar keine Aufzeichnung, letzterer hält den Analyse-Lauf nicht an.

Natürlich lässt sich über dieses Mittel auch ein ChangeDetection-Lauf auslösen (natürlich etwas teuer), falls
man Daten von Komponenten manuell geändert hat und die Auswirkungen auf den DOM-Baum sehen will. Besser ist es aber über eine Referenz auf die Application die ```tick```-Methode auszurufen.

    appRef = ng.probe($0).injector.get(ng.coreTokens.ApplicationRef);
    appRef.tick();

### Debugging von Source-Code im Browser

Die TypeScript-Sourcen findet man im Webpack-Ordner in den Browser-Developertools (beim Chrome im Sources-Tab - dort noch über den Dot-Knoten zum ```src```-Ordner wechseln, beim Firefox im Debugger-Tab). Jetzt lassen sich ganz normal Haltepunkte setzen, Variablen analysieren und die Methoden im Call-Stack einsehen.

## Augury

Augury ist eine Browser-Erweiterung, die mittlerweile sowohl für Firefox und Chrome bereit steht. Der Link
[augury.angular.io](https://augury.angular.io) leitet direkt weiter zur Entwickler-Seite bei [rangle.io](https://augury.rangle.io/) mit den Links zu den jeweiligen Browser-Addon Stores. Ich selbst nutze Augury produktiv nur noch selten (auch weil es immer wieder einen leichten buggy Eindruck hinterlässt). In meinen Trainings allerdings umso mehr, da man doch recht schön den Component-Tree präsentieren kann (mit State und der Möglichkeit, Events zu triggern), den Router-Tree visualisieren kann sowie die Modul-Abhängikeiten auflösen kann.

Über Augury ausgewählte Elemente im Komponenten-Baum stehen übrigens direkt über die Variable
```$$el``` zur Verfügung (das DebugElement, siehe oben ```ng.probe```). Außerdem kann man sehr einfach über einen Link in der Komponenten-Ansicht zum TypeScript-Sourcecode der Komponente navigieren.

Für Infos zur weiteren Verwendung von Augury verweise ich an dieser Stelle auf die (manchmal leicht veralteteten) [Guides](https://augury.rangle.io/pages/guides/index.html) bzw. auf einschlägige Developer-Blogs (die man sich bitte selbst googelt, da ich zur Zeit selbst keinen aktuellen und guten Beitrag kenne).

Zusatztipp eines Teilnehmers einer meiner letzten Schulungen (Berlin): die Ansicht erneuert sich nicht immer zuverlässig. Bisher habe ich das nur erreicht durch ein komplettes Schließen der Developer Tools und (!) des Browsers. Hier hilft aber ein einfacher Wechsel des Augury Farbschemas (von Hell nach Dunkel und wieder zurück). Top, vielen Dank nochmal an dieser Stelle.

## Debugging über Visual Studio Code

Die Visual Studio Code Erweiterung [Debugger for Chrome](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome). Über diese ist mittlwerweile ein komplett transparentes Debuggen von Angular Anwendungen möglich - auch(!) im Zusammenspiel mit den Debugger-Tools des Browsers. Also Haltepunkte sowie zum Beispiel Einzelschritte von Anweisungen laufen synchron sowohl im Visual Studio Code als auch im Browser mit.

Zur Verwendung in einem Projekt einfach mit F5 den Debug-Lauf starten. Beim ersten Aufruf lässt sich ein Profil für Chrome erzeugen bei dem lediglich die url-Property angepasst werden muss.

    {
        // Use IntelliSense to learn about possible attributes.
        // Hover to view descriptions of existing attributes.
        // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
        "version": "0.2.0",
        "configurations": [
            {
                "type": "chrome",
                "request": "launch",
                "name": "Launch Chrome against localhost",
                "url": "http://localhost:4200",
                "webRoot": "${workspaceFolder}"
            }
        ]
    }

Detailliertere Tipps finden sich bei den [VS Code Recipes](https://github.com/microsoft/vscode-recipes/tree/master/Angular-CLI).
