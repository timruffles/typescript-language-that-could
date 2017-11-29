## What's it like?
{class:'title'}

## Extending

## A superset of modern JS

![img](src/img/superset.png)

## JS today

```javascript
class Queue {
  async flush() {
    let item;
    while(item = await this.next()) {
      this.act(item, ({ id }) => {
        console.log(\`${id} done\`);
      });
    }
  }
}
```

## Some JS

```javascript
function getHostname(url) {
  const a = document.createElement("a");
  a.href = url;
  return a.hostname;
}
```

## Some TS

```javascript
function getHostname(url: string): string {
  const a: HTMLAnchorElement =
     document.createElement("a");
  a.href = url;
  return a.hostname;
}
```

## Types!

```javascript
function...(url: string): string ...
  const a: HTMLAnchorElement ...
  // ...
}
```

## Where do you want the bugs to show up?

## Without types

```javascript
const parent = el.parentElement;
parent.setAttribute("src", imageLocation);
```

## boom
{class:'notitle'}

```javascript
const parent = el.parentElement;

// Error: Cannot read property 
//    'setAttribute' of undefined
parent.setAttribute("src", imageLocation);
```

## VS...

```javascript
const parent = el.parentElement;
// object is possibly null
parent.setAttribute("src", imageLocation);
```

## TypeScript feels familiar

## e.g vs Coffeescript

```coffeescript
getHostname = (url) =>
  a = document.createElement "a"
  a.href = url
  a.hostname
```

## Especially when compiled

```sh
tsc example.ts
```

```javascript
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



## Same runtime semantics

- i.e, not PureScript (Haskell-ish)

## And, of course, same platform APIs

## And same VMs

## So... JS with types

## Highlights

- inference
- structual typing
- generics
- type unions
- mapped types


## It's not dumb
{class:'notitle'}

![dumb](src/img/static-types.jpg)

## Inference

```java
// Java gave static types a bad name
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
    // control-flow analysis:
    // clear this is a HTMLElement,
    // rather than a plain Element
    return node.offsetParent;
  }
} 
```

## Embraces dynamic idioms

## e.g
{class:'notitle'}

```javascript
// we know this is a list of names, 
// string[], but can TypeScript?
const names = _.pick([
  {name: "c#"}, 
  {name: "f#"},
  {name: "d"}
], "name");
```

## Can be typed

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
## Tagged unions

## Tagged unions
{class:'notitle'}

```typescript
interface Sms {
  kind: 'sms';
  number: string;
}
interface Email {
  kind: 'email';
  address: string;
}

type Destination = Sms | Email;
```

## Unions
{class:'notitle'}

```javascript
function formatRecipient(dest: Destination) {
  switch(dest.kind) {
    case 'sms':
      return \`Via text message to ${dest.number}\`;
    case 'email':
      return \`Via email to ${dest.address}\`;
  }
}
```

## Safe?

```javascript
function formatRecipient(dest: Destination) {
  switch(dest.kind) {
    case 'sms':
      return \`Via text message to ${dest.number}\`;
  }
}
```

## Exhaustiveness checking

```javascript
// error: not all code paths return a value
function formatRecipient(dest: Destination) {
  switch(dest.kind) {
    case 'sms':
      return \`Via text message to ${dest.number}\`;
  }
}
```

## Niceties

## Property handling

## Property handling
{class:'notitle'}
```javascript
// immutable record type
class PhoneNumber {
  readonly kind: 'phoneNumber'

  constructor(
    readonly country: number,
    readonly area: number,
    readonly number: number,
  ) {}
}
```

## Structual typing

## Structual typing
{class:'notitle'}

```javascript
// structual typing, classes as interfaces
const number: PhoneNumber = {
  country: 44,
  code: 1225,
  number: 733221,
};
```

