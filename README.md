# inject-computed-issue

A most simple example display of a typing issue with Vue3 using the inject/provide composition API.

## Problem description

As you'll find annotated in the files in [/src/componetns/] this project serves to example to a problem of wrapping and unwrapping types
using inject/provide in the new Vue3 composition API. When providing a computed property with `provide` the inferred type is ComputedRef<T>.
That type will also be inferred to the injected property returned by `inject`, although the value is automatically unwrapped at this point.

Now I am searching for answers how to fix this typing issue, potentially submitting a PR to the vue docs if there is a solution.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
