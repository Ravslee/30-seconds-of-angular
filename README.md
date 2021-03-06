[![Logo 30 Seconds of Angular](/config/logo.png)](https://github.com/nycJSorg/30-seconds-of-angular)


[![Build Status](https://travis-ci.com/nycJSorg/30-seconds-of-angular.svg?branch=master)](https://travis-ci.com/nycJSorg/30-seconds-of-angular) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

> Curated collection of useful Angular snippets that you can understand in 30 seconds or less.



* Use <kbd>Ctrl</kbd> + <kbd>F</kbd> or <kbd>command</kbd> + <kbd>F</kbd> to search for a snippet.
* Snippets are written in Angular 7.2.8+.

# 30 Seconds Of Angular

## Table of contents

Beginner snippets

* [Accessing Enums in template](#accessing-enums-in-template)
* [Default ViewEncapsulation value](#default-viewencapsulation-value)
* [trackBy in for loops](#trackby-in-for-loops)
	
Intermediate snippets

* [Adding keyboard shortcuts to elements](#adding-keyboard-shortcuts-to-elements)
* [Bind to host properties with host binding](#bind-to-host-properties-with-host-binding)
* [Global event listeners](#global-event-listeners)
* [Injecting document](#injecting-document)
* [Reusing code in template](#reusing-code-in-template)
* [Style bindings](#style-bindings)
* [Window Location injection](#window-location-injection)
	
Advanced snippets

* [Getting components of different types with ViewChild](#getting-components-of-different-types-with-viewchild)
	


## Beginner snippets

### Accessing Enums in template
Enums are great but they are not visible in Angular templates by default. 
With this little trick you can make them accessible.

```typescript
enum Animals {
  DOG,
  CAT,
  DOLPHIN
}

@Component({
  ...
})
export class AppComponent {
  animalsEnum: typeof Animals = Animals;
}
```



<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/accessing-enums-in-template) | [⬆ Back to top](#table-of-contents) | tags: [enums](https://codelab-next.firebaseapp.com/30/angular/tag/enums) [templates](https://codelab-next.firebaseapp.com/30/angular/tag/templates)  
<br><br>
### Default ViewEncapsulation value
If you're using `ViewEncapsulation` value which is different than default, it might be daunting to set the value manually for every component. 

Luckily you can configure it globally when bootstrapping your app:

```TypeScript
platformBrowserDynamic().bootstrapModule(AppModule, [
    {
        // NOTE: Use ViewEncapsulation.None only if you know what you're doing.
        defaultEncapsulation: ViewEncapsulation.None
    }
]);
```



<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/default-viewencapsulation-value) | [⬆ Back to top](#table-of-contents) | tags: [configuration](https://codelab-next.firebaseapp.com/30/angular/tag/configuration) [styling](https://codelab-next.firebaseapp.com/30/angular/tag/styling)  
<br><br>
### trackBy in for loops
To avoid the expensive operations, we can help Angular to track which items added or removed i.e. customize the default tracking algorithm by providing a trackBy option to NgForOf.

So you can provide your custom trackBy function that will return unique identifier for each iterated item. 
For example, some key value of the item. If this key value matches the previous one, then Angular won't detect changes.

**trackBy** takes a function that has _index_ and _item_ args. 

```typescript
@Component({
  selector: 'my-app',
  template: `<ul>
      <li *ngFor="let item of items; trackBy: trackByFn">{{item.id}}</li>
    </ul>`,
})
export class AppComponent { 
  trackByFn(index, item) {
    return item.id;
  }
}
```
If trackBy is given, Angular tracks changes by the return value of the function. 

Now when you change the collection, Angular can track which items have been added or removed according to the unique identifier and create/destroy only changed items.


#### Links
https://angular.io/api/common/NgForOf
https://angular.io/api/core/TrackByFunction

<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/trackby-in-for-loops) | [⬆ Back to top](#table-of-contents) | tags: [good-to-know](https://codelab-next.firebaseapp.com/30/angular/tag/good-to-know) [tips](https://codelab-next.firebaseapp.com/30/angular/tag/tips) [components](https://codelab-next.firebaseapp.com/30/angular/tag/components) [performance](https://codelab-next.firebaseapp.com/30/angular/tag/performance)  
<br><br>

## Intermediate snippets

### Adding keyboard shortcuts to elements
It's really easy to add keyboard shortcuts in the template: 
```html
<textarea (keydown.ctrl.enter)="doSomething()"></textarea>
```

<details>
<summary>Bonus</summary>

```html
<input (keydown.enter)="...">
<input (keydown.a)="...">
<input (keydown.esc)="...">
<input (keydown.shift.esc)="...">
<input (keydown.control)="...">
<input (keydown.alt)="...">
<input (keydown.meta)="...">
<input (keydown.9)="...">
<input (keydown.tab)="...">
<input (keydown.backspace)="...">
<input (keydown.arrowup)="...">
<input (keydown.shift.arrowdown)="...">
<input (keydown.shift.control.z)="...">
<input (keydown.f4)="...">
```
</details>

#### Links
https://alligator.io/angular/binding-keyup-keydown-events

<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/adding-keyboard-shortcuts-to-elements) | [⬆ Back to top](#table-of-contents) | tags: [tips](https://codelab-next.firebaseapp.com/30/angular/tag/tips) [good-to-know](https://codelab-next.firebaseapp.com/30/angular/tag/good-to-know)  
<br><br>
### Bind to host properties with host binding
Every rendered angular component is wrapped in a host element (which is the same as component's selector).

It is possible to bind properties and attributes of host element using @HostBinding decorators, e.g. 

```typescript
import { Component, HostBinding } from '@angular/core';

@Component({
   selector: 'my-app', 
   template: `
  <div>Use the input below  to select host background-color:</div>
  <input type="color" [(ngModel)]="color"> 
`,
  styles:[`:host { display: block; height: 100px; }`]
  },
  
)
export class AppComponent {
  @HostBinding('style.background') color = '#ff9900';
}
```



<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/bind-to-host-properties-with-host-binding) | [⬆ Back to top](#table-of-contents) | tags: [components](https://codelab-next.firebaseapp.com/30/angular/tag/components)  
<br><br>
### Global event listeners
It is possible to add global event listeners in your Components/Directives with `HostListener`. Angular will take care of unsubscribing once your directive is destroyed.

```typescript
@Directive({
  selector: '[rightClicker]'
})
export class ShortcutsDirective {
  @HostListener('window:keydown.ArrowRight')
  doImportantThings() {
    console.log('You pressed right');
  }
```

<details>
<summary>Bonus</summary>

You can have multiple bindings:

```typescript
  @HostListener('window:keydown.ArrowRight')
  @HostListener('window:keydown.PageDown')
  next() {
    console.log('Next')
  }
```

You can also pass params:

```typescript
  @HostListener('window:keydown.ArrowRight', '$event.target')
  next(target) {
    console.log('Pressed right on this element: ' + target)
  }
```
</details>


<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/global-event-listeners) | [⬆ Back to top](#table-of-contents) | tags: [events](https://codelab-next.firebaseapp.com/30/angular/tag/events) [components](https://codelab-next.firebaseapp.com/30/angular/tag/components)  
<br><br>
### Injecting document
Sometimes you need to get access to global `document`. 

To simplify unit-testing, Angular provides it through dependency injection:

```typescript
import { DOCUMENT } from '@angular/common';
import { Inject } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `<h1>Edit me </h1>`
})
export class AppComponent {
    constructor(@Inject(DOCUMENT) private document: Document) {
        // Word with document.location, or other things here....
    }
}
````


#### Links
https://angular.io/api/common/DOCUMENT

<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/injecting-document) | [⬆ Back to top](#table-of-contents) | tags: [dependency injection](https://codelab-next.firebaseapp.com/30/angular/tag/dependency injection)  
<br><br>
### Reusing code in template
While the best way of reusing your code is creating a component, it's also possible to do it in a template.

To do this you can use `ng-template` along with `*ngTemplateOutlet` directive.

```html
  <p>
    <ng-container *ngTemplateOutlet="fancyGreeting"></ng-container>
  </p>

  <button>
    <ng-container *ngTemplateOutlet="fancyGreeting"></ng-container>    
  </button>
  
  <ng-template #fancyGreeting>
    Hello <b>{{name}}!</b>
  </ng-template>
```


#### Links
https://angular.io/api/common/NgTemplateOutlet
https://angular.io/guide/structural-directives#the-ng-template

<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/reusing-code-in-template) | [⬆ Back to top](#table-of-contents) | tags: [templates](https://codelab-next.firebaseapp.com/30/angular/tag/templates)  
<br><br>
### Style bindings
You can use advanced property bindings to set specific style values based on component property values: 

```html
<p [style.background-color]="'green'">
  I am in green background
</p>

<p [style.font-size.px]="isImportant ? '30' : '16'">
  May be important text.
</p>

```

<details>
<summary>Bonus</summary>

```html
<!-- Width in pixels -->
<div [style.width.px]="pxWidth"></div>

<!-- Font size in percentage relative to the parent -->
<div [style.font-size.%]="percentageSize">...</div>

<!-- Height relative to the viewport height -->
<div [style.height.vh]="vwHeight"></div>
```
</details>


<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/style-bindings) | [⬆ Back to top](#table-of-contents) | tags: [styles](https://codelab-next.firebaseapp.com/30/angular/tag/styles)  
<br><br>
### Window Location injection
For testing purposes you might want to inject `window.location` object in your component.
You can achieve this with custom `InjectionToken` mechanism provided by Angular.

```typescript
export const LOCATION_TOKEN = new InjectionToken<Location>('Window location object');

@NgModule({
  providers: [
    { provide: LOCATION_TOKEN, useValue: window.location }
  ]
})
export class SharedModule {}

//...

@Component({
})
export class AppComponent {
  constructor(
    @Inject(LOCATION_TOKEN) public location: Location
  ) {}
}
```


#### Links
https://itnext.io/testing-browser-window-location-in-angular-application-e4e8388508ff
https://angular.io/guide/dependency-injection

<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/window-location-injection) | [⬆ Back to top](#table-of-contents) | tags: [dependency-injection](https://codelab-next.firebaseapp.com/30/angular/tag/dependency-injection) [testing](https://codelab-next.firebaseapp.com/30/angular/tag/testing)  
<br><br>

## Advanced snippets

### Getting components of different types with ViewChild
It's possible to use `@ViewChild` (also `@ViewChildren` and `@ContentChild/Children`) to query for components of different types using dependency injection. 

In the example below we can use `@ViewChildren(Base)` to get instances of `Foo` and `Bar`.

```typescript
abstract class Base {}

@Component({
  selector: 'foo',
  providers: [{ provide: Base, useExisting: Foo }]
})
class Foo extends Base {}

@Component({
  selector: 'bar',
  providers: [{ provide: Base, useExisting: Bar }]
})
class Bar extends Base {}

// Now we can require both types of components using Base.
@Component({ template: `<foo></foo><bar></bar>` })
class AppComponent {
  @ViewChildren(Base) components: QueryList<Base>;
}
```


#### Links
https://www.youtube.com/watch?v=PRRgo6F0cjs

<br>[⭐ Interactive demo of this snippet](https://codelab-next.firebaseapp.com/30/angular/getting-components-of-different-types-with-viewchild) | [⬆ Back to top](#table-of-contents) | tags: [good-to-know](https://codelab-next.firebaseapp.com/30/angular/tag/good-to-know) [tips](https://codelab-next.firebaseapp.com/30/angular/tag/tips) [components](https://codelab-next.firebaseapp.com/30/angular/tag/components) [dependency-injection](https://codelab-next.firebaseapp.com/30/angular/tag/dependency-injection)  
<br><br>
