# raven-color

[![CI](https://github.com/martian56/raven-color/actions/workflows/ci.yml/badge.svg)](https://github.com/martian56/raven-color/actions/workflows/ci.yml)

ANSI colors and text styles for terminal output. Reach for a one-shot function
like `red("...")` when you just need a color, or compose a `Style` with the
builder when you want more than one thing at once. It adds the reset code for
you. No dependencies.

## Install

```toml
[dependencies]
"github.com/martian56/raven-color" = "v0.1.0"
```

## Usage

```rust
import "github.com/martian56/raven-color" { red, green, Style }

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

It always emits the escape codes. If you're writing to a file or a pipe where
you don't want them, keep that output off this path.

## License

MIT
