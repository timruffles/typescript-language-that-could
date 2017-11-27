## Wasn't killing JS
{class:'subtitle'}

## Extending

## Before

```javascript
function getHostname(url) {
  var a = document.createElement("a");
  return a.href = url, a.hostname;
}
```

## After

```javascript
function getHostname(url: string): string {
  var a: HTMLAnchorElement = document.createElement("a");
  return a.href = url, a.hostname;
}
```

## Not a GWT

## Nor even a Coffeescript

```coffeescript
getHostname = (url) =>
  a = document.createElement "a"
  a.href = url
  a.hostname
```

## TypeScript felt familiar


  
