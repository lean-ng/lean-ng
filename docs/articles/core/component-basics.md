---
id: component-basics
title: Component Basics
sidebar_label: Component Basics
---
## Syntax

Components sind TypeScript-Klassen - dekoriert mit einem TypeScript-Decorator.

```typescript title="sample.component.ts"
  @Component({
    selector: 'app-sample',
    template: '<span>Sample Component</span>
  })
  export class SampleComponent {}
```

Im Argument der Decorator-Factory können verschiedene Optionen eingestellt werden.
Die wichtigsten sind der (optionale) Selector über den die Komponente in Templates
eingesetzt wird und die Pflicht-Angabe Template bzw. Template-Url, um das der
Komponente zugerodnete Template festzulegen. Weitere Einstellungen mit Relevanz in
der Praxis sind die Angabe der Komponenten-Styles und die Festlegung der
ChangeDetection-Strategie. Weniger gebräuchlich sind ViewEncapsulation und
Dienst-Provider.

Der Link zur kompletten API: https://angular.io/api/core/Component

## Class Member

Üblicherweise haben Komponenten einen leeren Konstruktor, der lediglich Dienste
anfordert, sowie einfache Properties und Methoden ohne Rückgabe-Typ. Die Properties
werden vom Template verarbeitet bzw. gerendert, die Methoden von Event-Handlern
aufgerufen. Unüblich dagegen sind öffentliche Getter für Properties bzw. Methoden,
die berechnete Werte aus anderen Properties liefern. Beides sollte mit Bedacht
verwendet werden im Hinblick auf mögliche Performance-Einbußen der Anwendung.

```typescript title="counter.component.ts"
  @Component({
    selector: 'app-counter',
    template: `
      <div>
        Counter: {{ count }}
        <button (click)="inc()">Inc</button> 
      </div>`
  })
  export class SampleComponent {
    count = 0;
    inc() {
      ++this.count;
    }
  }
```