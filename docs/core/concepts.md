---
id: concepts
title: Konzepte - Aufbau einer Angular Anwendung
sidebar_label: Konzepte
---
## 1. Componenten

Angular-Anwendungen bestehen aus Komponenten - den Haupt-Bausteinen. Eine
Komponente ist eine Codeklasse dekoriert als ```Component``` mit einem
zugeordneten HTML-Template und optional einem Selektor in den Metadaten.

## 2. Module

Damit eine Komponente benutzt werden kann, muss sie in einem Modul deklariert
werden.

Ein Modul ist eine Codeklasse dekoriert als ```NgModule```. Im Dekorator
wird definiert:

* Komponenten, die dieses Modul deklariert
* Importierte Module, die von diesem Modul benutzt werden
* Komponenten, die dieses Modul zur Verwendung in anderen Modulen exportiert
* Bootstrap-Komponenten (die zum Anwendungsstart benötigt werden)

Der Anwendungsstart erfolgt, indem ein Hauptmodul von der jeweiligen
Angular-Plattform gebootstrapt wird. Dieses Hauptmodul definiert die
Bootstrap-Komponente, die von Angular in der ```index.html``` gerendert wird.

## 3. Templates

Templates sind HTML-Vorlagen gespickt mit Bindungsanweisungen an die Daten
und Methoden der Komponente, der dieses Template zugeordnet wurde. Dabei
können neben den Techniken des Property- und Eventbindings auch weitere
Komponenenten eingesetzt werden, die dem Modul der Komponente bekannt sind.
Also entweder in diesem Modul auch deklariert werden oder in einem anderen
importierten Modul deklariert und exportiert wurden.

## 4. Direktiven

Direktiven sind Codeklassen dekoriert als ```Directive``` mit einem
Selektor. Direktiven haben kein Template, sondern manipulieren den DOM des
Elementes (der Komponente), auf das sie angewendet wurden. Auch Direktiven
müssen in Modulen deklariert werden bevor sie angewendet werden können. Und
natürlich exportiert werden, falls sie von anderen Modulen aus genutzt werden
können. Das Module ```CommonModule``` aus dem Paket ```@angular/common```
definiert die wichtigsten Direktiven, die fast in jedem Angular-Template
eingesetzt werden (```ngClass```, ```ngIf```, ```ngFor```, ...).

## 5. Pipes

Auch Pipes (Input-Output-Filter) können in Templates eingesetzt werden.
Eine Pipe ist eine Codeklasse dekoriert als ```Pipe```, die zusätzlich
das ```PipeTransform```-Interface implementiert. Wiederum gilt, dass Pipes
in Modulen registriert (deklariert) werden müssen. Die wichtigsten
vordefinierten Pipes (```date```, ```decimal```, ...) sind ebenfalls
im ```CommonModule``` registriert.

## 6. Komponenten-Interaktion

Kommunikation zwischen Komponenten zum Austausch von Daten kann zwischen
Eltern/Kind-Komponenten (die Eltern-Komponente setzt im Template die 
Kind-Komponente ein) über ```@Input```- und ```@Output```-Properties des
Kindes erfolgen. Alternativen dazu sind ```@ViewChild``` und 
Template-Referenz-Variablen in der Elternkomponente, die jeweils Zugriff
auf die Kind-Komponente ermöglichen.

Jegliche über die *Eltern-Kind-Beziehung* hinausgehende Komponenten-Interaktion
geschieht über Dienste.

## 7. Services

Services (Dienste) sind Codeklassen von denen Komponenten eine Instanz 
(meißt als Singleton) vom Dependency-Injection Container *anfordern*. Die
Injizierung erfolgt über den Konstruktor der Komponente (der Direktiven,
der Pipe).

Dienste müssen bereitgestellt werden (*provided*). In früheren 
Angular-Versionen vor Angular 6 wurden die Provider in Modulen (für globale
Dienste, die in der ganzen Anwendung als Singleton bereitgestellt werden) oder
Komponenten (für *lokale* Dienste, deren Instanz nur der Komponente und ihren
Kindern zur Verfügung steht) im Dekorator definiert.

Seit Angular 6 ist es best-practice Dienste *self-providing* zu deklarieren
- im ```@Injectable```-Dekorator der Dienst-Codeklasse.

Dienstklassen übernehmen oft die Kommunikation mit der Außenwelt (Http,
WebSockets, Storage-API), stellen globale Funktionalität bereit
(Authentifizierung, Authorisierung, Translations-Dienste, aufwändige
Algorithmik, ...) oder halten den Anwendungs-State - also die Daten die allen
Komponenten zur Verfügung stehen - vor.
