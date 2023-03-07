# 🌈 nest-css
Simple tool to help me write nested css. Transpiles to proper css. With the help of: https://github.com/multiprocessio/cssplus

# 📄 Instructions
Just place the nest-css.js file where your .scss files are located and the run ```node ./nest-css``` to start it. It will watch for any changes in your .scss files and then generates a corresponding .css file in the same directory.

# 🫤 Quirks 

## Pseudo Selectors 
Currently the transformer can't parse pseudo selectors properly so I had to make some workarounds.

Conventional:
```css
    ul {
        li {
            &:hover {
                zoom: 1
            }
            &::before {
                content: '';
            }
        }
    }
    
    a:hover {
        color: green;
    }

```

How we should write it so that the transformer can understand:
```css
    ul {
        li {
            [-hover] {
                zoom: 1
            }
            [--before] {
                content: '';
            }
        }
    }
    
    /* Need to nest the hover selector inside */
    a {
        [-hover] {
            color: green;
        }
    }

```
It's a faff but I had to do it.

## Empty Selectors
The transformer also considers empty selector as errors. So be careful, maybe just comment it out if its empty.
```css
    .container {
        span { // <-- This will cause a parsing error.
            
        }
    }
```

## Self Selector
The transformer has a different way of referrencing the current selector.

Standard way
```css
    a {
        &.active {
            color: green;
        }
    }
```

nest-css way 
```css
    a {
        [SELF].active {
            color: green;
        }
    }
```
