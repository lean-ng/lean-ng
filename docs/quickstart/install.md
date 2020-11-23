---
id: install
title: Installation
sidebar_label: Installation
---
## Angular CLI

Auch wenn ich bei der Demonstration der Angular Konzepte mitunter auf das Angular
CLI verzichte, ist das nicht beste Praxis beim Entwickeln von eigenen Angular
Anwendungen.

Es müssen schon spezielle Anforderungen vorliegen, die einen solchen Verzicht
notwendig machen. In der Regel sollte man auf dem Build-Prozess des CLI seinen
Development-Workflow aufsetzen.

Das CLI wird normalerweise global installiert:

    npm install --global @angular/cli

Oder bei der Benutzung von ```yarn```:

    yarn global add @angular/cli

Und um ein erstes Angular-Projekt jetzt anzulegen (bei eventuellen Fragen des
CLI hier noch einfach die jeweilige Standard-Option übernehmen):

    ng new angular-app

Dabei ist ```angular-app``` der Projektname. Das CLI legt einen Unterordner
gleichen Namens an und entpackt ein Starter-Template in diesen Ordner. Je nach
gesetzten Optionen wird das Projekt konfiguriert, werden die NPM-Abhängigkeiten
installiert und es wird ein Git-Repository initialisiert mit einem initialen
Git-Commit.

Falls das ```ng```-Kommando später übrigens in einem Angular-Projekt ausgeführt
wird, delegiert das globale CLI immer an das lokale CLI des Projektes. Damit
wird sichergestellt, dass eventuelle Versions-Unterschiede zwischen globaler
und lokaler Installation keine Rolle spielen.

Zur weiteren Verwendung und den möglichen Optionen siehe das [CLI-Kapitel](/docs/dev-tooling/cli).

## Powershell

Beim Einsatz der Powershell ist zu beachten, dass die Ausführungsrechte für Scripte konfiguriert sind:

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```