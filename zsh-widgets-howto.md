---
title: ZSH widgets - basic usage
tags: zsh
---

Key combinations and events are not bound to functions but to *widgets*.

**Bind a custom function to a key**

```zsh
# Register widget `my_widget' which calls function `my_fuction' upon execution
# The function need not be defined yet.
zle -N my_widget my_function

# Bind the widget to a key
bindkey '^r' my_widget

# Define the function.
function my_function {
  echo "hello world"
}
```

**Bind a built-in function to a key**

```zsh
# Make the built-in function available with `autoload'.
autoload -U edit-command-line

# Register the widget with the function. If the widget shall inherit the
# function's name only the latter needs to be specified.
zle -N edit-command-line

# Bind the widget to a key.
bindkey -M vicmd '^e' edit-command-line
```
