## Not 'killing' JS
{class:'title'}

## Extending

## A superset of modern JS

## Before

```javascript
function getHostname(url) {
  const a = document.createElement("a");
  a.href = url;
  return a.hostname;
}
```

## After

```javascript
function getHostname(url: string): string {
  const a: HTMLAnchorElement = document.createElement("a");
  a.href = url;
  return a.hostname;
}
```

## With types!

```javascript
function...(url: string): string ...
  const a: HTMLAnchorElement ...
  // ...
}
```

## Types

Where do you want the bugs to show up?

## Without types

```javascript
TODO
```

## Errors identified by users 

## VS...

```javascript
TODO
```

## Compiled output

```javascript
// compiler output: boring
function getHostname(url) {
  const a = document.createElement("a");
  a.href = url;
  return a.hostname;
}
```

## Vs...

```haskell
main :: Eff (dom :: DOM) Unit
main =
    render $ fold
      [ h1 (text "Try PureScript!")
      ]
```

```javascript
// ...
var main = render(fold(Data_Foldable.foldableArray)
    (monoidDoc)([h1(text(
        "Try PureScript!"))]));
```

## Or even vs Coffeescript

```coffeescript
getHostname = (url) =>
  a = document.createElement "a"
  a.href = url
  a.hostname
```

## TypeScript feels familiar

## Same runtime semantics

- i.e, not PureScript (Haskell-ish)

## And, of course, same platform APIs

## And same VMs

## So it's "Just Javascript"

## It's not dumb
{class:'subtitle'}

![dumb](src/img/static-types.jpg)

## Inference

```java
String message = "hi";
```

```typescript
// clear that message is a string
let message = "hi";
const double = (x: number) => x * 2;

double(message);
```

## Advanced inference

```typescript
// infers return type: Element | undefined
function getOffset(node: Element) {
  if (node instanceof HTMLElement) {
    // control-flow analysis: clear this is a HTMLElement,
    // rather than a plain Element
    return node.offsetParent;
  }
} 
```

## Embraces current idioms

## e.g underscore/lodash

```javascript
// we know this is a list of names, string[], but can TypeScript?
const names = _.pick([{name: "c#"}, {name: "f#"}, {name: "d"}], "name");
```

## Yes!

```javascript
// mapped types
type Pick<Type, Key extends keyof Type> = {
    [Property in Key]: Type[Property];
}

function pick<
  Type, 
  Key extends keyof Type
>(obj: Type, ...keys: Key[]): Pick<Type, Key>;
```


## Language features TODO

- structual typing
- functional (e.g the rewrite PR to drag drop shim)
- type unions
- primitive enums (strings)
- exhaustiveness checking
- tagged unions

