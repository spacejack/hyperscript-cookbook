# Hyperscript Cookbook

Below are several examples that might be helpful if you're familiar with Angular templates and are moving to JSX or hyperscrpt (AKA Javascript.)

Hyperscript imlementations vary, but are fairly similar for the most part. In the examples below, the function `h()` represents the hyperscript function. (For example React's `React.createElement()` or Mithril's `m()`.)

## String Interpolation

*Angular:*

```html
<p>Hello, {{user.firstName}}</p>
<p>1 + 1 = {{1 + 1}}</p>
```

*JSX:*

```
<p>Hello, {user.firstName}</p>
<p>1 + 1 = {1 + 1}</p>
```

*Hyperscript:*

```javascript
h('p', `Hello, ${user.firstName}`),
h('p', `1 + 1 = ${1 + 1}`)
```

## Property Binding

*Angular:*

```html
<img [src]="heroImageUrl">
<button [disabled]="isDisabled">Button Text</button>
```

*JSX:*

```
<img src={heroImageUrl}>
<button disabled={isDisabled}>Button Text</button>
```

*Hyperscript:*

```javascript
h('img', {src: heroImageUrl}),
h('button', {disabled: isDisabled}, 'Button Text')
```

## Inline Style Binding

*Angular:*

```html
<div [style.color]="isSpecial ? 'red' : 'green'">The Hero</div>
```

*JSX:*

```
<div style={color: isSpecial ? 'red' : 'green'}>The Hero</div>
```

*Hyperscript:*

```javascript
h('div', {style: {color: isSpecial ? 'red' : 'green'}}, 'The Hero')
```

## Statements

*Angular:*

```html
<button (click)="deleteHero()">Delete hero</button>
```

*JSX:*

```
<button onclick={deleteHero()}>Delete hero</button>
```

*Hyperscript:*

```javascript
h('button', {onclick: deleteHero}, 'Delete hero')
```

## Iteration

*Angular:*

```html
<div *ngFor="let hero of heroes">{{hero.name}}</div>
```

*JSX:*

```
heroes.map(hero => <div>{hero.name}</div>)
```

*Hyperscript:*

```javascript
heroes.map(hero => h('div', hero.name))
```

## Iteration with index

*Angular:*

```html
<div *ngFor="let hero of heroes; let i=index">{{i + 1}} - {{hero.name}}</div>
```

*JSX:*

```
heroes.map((hero, i) => <div>{i + 1} - {hero.name}</div>)
```

*Hyperscript:*

```javascript
heroes.map((hero, i) => h('div', `${i + 1} - ${hero.name}`))
```

## Components

*Angular:*

```html
<myComponent [name]="Zeke"></myComponent>
```

*JSX:*

```
<myComponent name="Zeke"/>
```

*Hyperscript:*

```javascript
h(myComponent, {name: 'Zeke'})
```

## Nesting Components

*Angular:*

```html
<div>
    <myComponent [name]="Zeke">
        <myChildComponent/>
    </myComponent>
</div>
```

*JSX:*

```
<div>
    <myComponent name="Zeke">
        <myChildComponent/>
    </myComponent>
</div>
```

*Hyperscript:*

```javascript
m('div',
    m(myComponent, {name: 'Zeke'},
        m(myChildComponent)
    )
)
```

## `if`

*Angular:*

```html
<div *ngIf="isActive">Is active</div>
```

*JSX:*

```
isActive && <div>Is active</div>
```

*Hyperscript:*

```javascript
isActive && h('div', 'Is active')
```

## `if` ... `else`

*Angular:*

(See `swtich` below.)

*JSX:*

```
<div>isAlive
    ? <p class="green">The hero is alive.</p>
    : <p class="red">The hero is dead.</p>
</div>
```

*Hyperscript:*

```javascript
h('div', isAlive
    ? m('p.green', 'The hero is alive.')
    : h('p.red', 'The hero is dead.')
)
```

## `switch`

*Angular:*

```html
<div [ngSwitch]="hero.emotion">
    <happy-hero *ngSwitchCase="'happy'" [hero]="hero"></happy-hero>
    <sad-hero *ngSwitchCase="'sad'" [hero]="hero"></sad-hero>
    <confused-hero *ngSwitchCase="'confused'" [hero]="hero"></confused-hero>
    <unknown-hero *ngSwitchDefault [hero]="hero"></unknown-hero>
</div>
```

*JSX:*

```
<div>{
    hero.emotion === 'happy' ? <happyHero hero={hero}/>
    : hero.emotion === 'sad' ? <sadHero hero={hero}/>
    : hero.emotion === 'confused' ? <confusedHero hero={hero}/>
    : <unknownHero hero={hero}/>
}</div>
```

*Hyperscript:*

```javascript
h('div',
    hero.emotion === 'happy' ? h(happyHero, {hero})
    : hero.emotion === 'sad' ? h(sadHero, {hero})
    : hero.emotion === 'confused' ? h(confusedHero, {hero})
    : h(unknownHero, {hero})
)
```

## `null` object testing

*Angular:*

```html
<p>The hero's name is {{hero?.name}}</p>
```

*JSX:*

```
<p>The hero's name is {hero ? hero.name : ''}</p>
```

*Hyperscript:*

```javascript
m('p', `The hero's name is ${hero ? hero.name : ''}`)
```
