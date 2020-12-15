---
id: template-syntax
title: Template Syntax
sidebar_label: Template Syntax
---
## Property Binding

> One-Way: Component-Property -> DOM-Element/Angular-Component Property
bzw. eine Template-Expression

```html
  <element [propertyName]="componentProperty"></element>
```
## Interpolation

> Convenience Syntax für ein Property Binding

```html
  <element propertyName="{{ componentProperty }}"></element>
  <element>{{ componentProperty }}</element>
```

Letzters ist eine Bindung an die Property ```textContent```.
## Event Binding

> DOM-Element/Angular-Component Event ruft Component-Method bzw. führt
Template-Statement aus.

```html
  <element (eventName)="componentMethod()"></element>
```
## Two-Way Binding

> Two-Way: Kombination aus Property- und Event-Binding mit etwas syntaktischem Zucker

```html
  <component-name [prop]="componentProp" (propChange)="componentProp=$event"></component-name>
  <component-name [(prop)]="componentProp"></component-name>
```

## Template Reference Variables

> Definiert lokale Template-Variable. Gesetzt auf DOM-Element oder Component- bzw. Directive-Instanz

```html
  <element #elt></element>
  <component-name #comp></component-name>
```

## Attribute Directives

> Per Attribut angewendete Directive

```html
  <element directiveName></element>
  <element directiveName [directiveProp]="value"></element>
  <element [directiveName]="value"></element>
```
## Structural Directives

> Spezielle Template-Directive mit Mikro-Syntax

```html
  <element *ngIf="true"></element>
  <ul>
    <li *ngFor="let s of ['Eins','Zwei','Drei']">
      {{ s }}
    </li>
  </ul>
```

## Attribute/Class/Style Bindings

> Spezielle Bindungen an HTML-Attribute bzw. syntaktische Vereinfachungen zum Setzen von CSS-Klassen bzw. inline CSS-Styles.

```html
  <element [attr.data-id]="17"></element>
  <element [style.display]="'block"></element>
  <element [class.hidden]="true"></element>
```

## Template Expressions/Statements

> Besonderheiten der Ausdrücke bzw. Statements bei den verschiedenen Bindungsarten.

