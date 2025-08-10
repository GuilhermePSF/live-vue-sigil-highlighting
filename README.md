# LiveVue sigil syntax highlighting for VS Code

Syntax highlighting for Vue/HTML templates embedded in Elixir `~VUE` sigils.

### What this extension does
- Injects Vue template tokenization into Elixir files inside `~VUE` sigils.
- Uses TextMate injection only; it does not register the `vue` language nor `.vue` files.
- Intentionally omits a Vue language configuration to avoid conflicts with Volar. Volar provides the authoritative Vue configuration and editor behavior.

### Requirements
- VS Code ≥ 1.60 or Cursor (per `package.json`).
- Recommended: install the Volar (Vue Language Features) extension. This extension relies on the Vue grammar provided by Volar, and avoids shipping its own language configuration to prevent conflicts. See Volar's language configuration for reference: [Volar vue-language-configuration.json](https://github.com/lomantig/volar/blob/master/extensions/vscode-vue-language-features/languages/vue-language-configuration.json).

### Supported `~VUE` forms
The following Elixir sigil delimiters are recognized:
- Heredoc triple double quotes: `~VUE""" ... """[a-z]*`
- Double quotes: `~VUE" ... "[a-z]*`
- Parentheses: `~VUE( ... )[a-z]*`
- Square brackets: `~VUE[ ... ][a-z]*`
- Curly braces: `~VUE{ ... }[a-z]*`

### Usage
Place Vue/HTML inside a `~VUE` sigil in Elixir:

```elixir
defmodule MyApp.Component do
  import LiveVue

  def template(assigns) do
    ~VUE"""
    <div :class="{ active: isActive }">
      <MyComponent :prop="count" />
    </div>
    """
  end
end
```

Other delimiters work too:

```elixir
~VUE"<div id=\"one\"></div>"
~VUE(<div id=\"two\"></div>)
~VUE[<div id=\"three\"></div>]
~VUE{<div id=\"four\"></div>}
```

### Notes & limitations
- This extension provides syntax highlighting only. It does not add Vue language features (completion, formatting, diagnostics) inside Elixir strings.
- Editor behaviors like auto-closing pairs and on-enter indentation are governed by the host editor and the active Vue extension; they may differ from plain `.vue` files.

### Development
- The grammar injection lives at `syntaxes/elixir-vue.json`.
- Launch an Extension Development Host from VS Code to test changes.

### License
See `LICENSE.txt`.
