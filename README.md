# raven-color

[![CI](https://github.com/martian56/raven-color/actions/workflows/ci.yml/badge.svg)](https://github.com/martian56/raven-color/actions/workflows/ci.yml)

ANSI colors and text styles for terminal output. Reach for a one-shot function
like `red("...")` when you just need a color, or compose a `Style` with the
builder when you want more than one thing at once. It adds the reset code for
you. No dependencies.

## Install

```toml
[dependencies]
"github.com/martian56/raven-color" = "v0.2.0"
```

## Usage

```rust
from "github.com/martian56/raven-color" import red, green, Style

print(red("error"))
print(green("ok"))

// Chain to combine; apply wraps the text once at the end:
print(Style.new().cyan().bold().underline().apply("a heading"))
print(Style.new().white().on_blue().apply(" badge "))
```

Each builder call returns a new `Style`, so you can keep a base around and branch
off it without the branches affecting each other:

```rust
let heading = Style.new().bold().underline()
print(heading.red().apply("Errors"))
print(heading.green().apply("Passed"))
```

## What's available

Foreground colors are `black`, `red`, `green`, `yellow`, `blue`, `magenta`,
`cyan`, `white`, and `gray`. The backgrounds are the same eight, as `on_black`
through `on_white`. Styles are `bold`, `dim`, `italic`, `underline`, and
`reverse`. The one-shot functions cover the common ones: `red`, `green`,
`yellow`, `blue`, `magenta`, `cyan`, `gray`, `bold`, `dim`, `underline`.

## A note on terminals

Colors switch themselves off when stdout is not a terminal (a pipe or a file)
and when `NO_COLOR` is set, so redirected output stays clean. `FORCE_COLOR`
turns them back on for a pipe, and `set_enabled(true)` or `set_enabled(false)`
decides for the whole program. `enabled()` reports the current choice. This
needs Raven 3.3.0 or newer.

## License

MIT
