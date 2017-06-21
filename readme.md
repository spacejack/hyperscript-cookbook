# Hyperscript Cookbook

Below are several examples that might be helpful if you're familiar with Angular templates and are moving to JSX or hyperscrpt (AKA Javascript.)

Hyperscript imlementations vary, but are fairly similar for the most part. In the examples below, the function `h()` represents the hyperscript function. (For example React's `React.createElement()` or Mithril's `m()`.)

### String Interpolation

*Angular:*

```html
<p>Hello, {{user.firstName}}</p>
<p>1 + 1 = {{1 + 1}}</p>
```

*Hyperscript:*

```javascript
h('p', `Hello, ${user.firstName}`),
h('p', `1 + 1 = ${1 + 1}`)
```

### Property Binding

*Angular:*

```html
<img [src]="heroImageUrl">
<button [disabled]="isDisabled">Button Text</button>
```

*Hyperscript:*

```javascript
h('img', {src: heroImageUrl}),
h('button', {disabled: isDisabled}, 'Button Text')
```

### Statements

*Angular:*

```html
<button (click)="deleteHero()">Delete hero</button>
```

*Hyperscript:*

```javascript
h('button', {onclick: deleteHero}, 'Delete hero')
```

###  Iteration

*Angular:*

```html
<div *ngFor="let hero of heroes">{{hero.name}}</div>
```

*Hyperscript:*

```javascript
heroes.map(hero => h('div', hero.name))
```

###  Iteration with index

*Angular:*

```html
<div *ngFor="let hero of heroes; let i=index">{{i + 1}} - {{hero.name}}</div>
```

*Hyperscript:*

```javascript
heroes.map((hero, i) => h('div', `${i + 1} - ${hero.name}`))
```

### `if`

*Angular:*

```html
<hero-detail *ngIf="isActive"></hero-detail>
```

*Javascript:*

```javascript
isActive && h('hero-detail')
```

### `if` ... `else`

*Angular:*

(See `swtich` below.)

*Hyperscript:*

```javascript
h('div', isAlive
	? m('p.green', 'The hero is alive.')
	: h('p.red', 'The hero is dead.')
)
```

### `switch`

*Angular:*

```html
<div [ngSwitch]="currentHero.emotion">
  <happy-hero *ngSwitchCase="'happy'" [hero]="currentHero"></happy-hero>
  <sad-hero *ngSwitchCase="'sad'" [hero]="currentHero"></sad-hero>
  <confused-hero *ngSwitchCase="'confused'" [hero]="currentHero"></confused-hero>
  <unknown-hero *ngSwitchDefault [hero]="currentHero"></unknown-hero>
</div>
```

*Hyperscript:*

```javascript
h('div',
	currentHero.emotion === 'happy' ? h('happy-hero')
	: currentHero.emotion === 'sad' ? h('sad-hero')
	: currentHero.emotion === 'confused' ? h('confused-hero')
	: h('unknown-hero')
)
```

### `null` object testing

*Angular:*

```html
<p>The current hero's name is {{currentHero?.name}}</p>
```

*Hyperscript:*

```javascript
m('p', `The current hero's name is ${currentHero ? currentHero.name : ''}`)
```
