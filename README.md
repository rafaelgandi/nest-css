# 🌈 nest-css
Simple tool to help me write nested css. Transpiles to proper css. With the help of: https://github.com/multiprocessio/cssplus

# Instructions
Just place the nest-css.js file where your .scss files are located and the run ```node ./nest-css``` to start it. It will watch for any changes in your .scss files and then generates a corresponding .css file in the same directory.

# Pseudo Selectors 🫤
Currently the transformer can't parse pseudo selectors properly so I had to make some work arouds.

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

```
It's a faff but I had to do it.
