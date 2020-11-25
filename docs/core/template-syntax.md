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
  <componentName [prop]="componentProp" (propChange)="componentProp=$event"></element>
  <componentName [(prop)]="componentProp"></element>
```

## Template Reference Variables

> Definiert lokale Template-Variable. Gesetzt auf DOM-Element oder Component- bzw. Directive-Instanz

## Attribute Directives

> Per Attribut angewendete Directive

## Structural Directives

> Spezielle Template-Directive mit Mikro-Syntax

## Attribute/Class/Style Bindings

> Spezielle Bindungen an HTML-Attribute bzw. syntaktische Vereinfachungen zum Setzen von CSS-Klassen bzw. inline CSS-Styles.

## Template Expressions/Statements

> Besonderheiten der Ausdrücke bzw. Statements bei den verschiedenen Bindungsarten.
