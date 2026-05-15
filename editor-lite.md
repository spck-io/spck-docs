# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Overview

Spck Editor Lite is a one-time purchase version of Spck Editor that unlocks premium editing features without a subscription. It is available as a separate app on both Android and iOS.

Lite includes everything in the free version, plus:

- **Predictive Keyboard** -- context-aware symbol suggestions on the extra keyboard
- **Custom Snippets** -- user-defined code templates with tab-stop placeholders
- **Neon Theme** -- an exclusive editor theme

These features are also available in the full version of Spck Editor with an active Gold or Supporter subscription. The Lite app provides the same functionality as a single purchase.

## <a name="predictive-keyboard"></a>Predictive Keyboard

The Predictive Keyboard replaces the standard Extra Keyboard with a row of context-aware symbol keys. Instead of press-holding a key to pick from a menu, the most likely symbols are displayed directly based on where the cursor is in the file.

### How It Works

Predictions are generated from statistical frequency tables built per language. When the cursor moves, the keyboard re-ranks symbols by how often each one appears at that type of position in real-world code. Supported languages include JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown, and plain text.

### Enabling or Disabling

Go to `Settings > Touch > Predictive Keyboard` to toggle the feature. In Lite, the Predictive Keyboard is enabled by default. Turning it off restores the standard Extra Keyboard.

> The Predictive Keyboard is only available on touch devices. It does not appear when using a physical keyboard or in tablet mode with an external keyboard attached.

## <a name="custom-snippets"></a>Custom Snippets

Custom Snippets let you create reusable code templates that appear in the autocomplete list as you type. Each snippet is scoped to a specific language so your JavaScript snippets do not clutter Python files.

### Creating a Snippet

1. Open `Settings > Editor > Custom Snippets`
2. Select the language (e.g. JavaScript, Python, HTML)
3. Tap **Add Snippet**
4. Enter a **trigger** -- the abbreviation you type to invoke the snippet
5. Enter the **body** -- the code that gets inserted

### Tab Stops and Placeholders

Snippets support tab stops so the cursor jumps between editable positions after insertion:

- `$1`, `$2`, `$3` -- numbered tab stops in order of traversal
- `$0` -- final cursor position after all tab stops
- `${1:defaultText}` -- a tab stop with placeholder text that is pre-selected for easy replacement

Example -- a JavaScript `for` loop snippet:

**Trigger:** `forloop`

**Body:**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

Typing `forloop` and selecting it from autocomplete inserts the full loop. Press Tab to jump between `i`, `array`, and the loop body.

### Import and Export

You can export all snippets to a file and import them on another device. This is useful for sharing snippet collections between phones or backing up your configuration.

## <a name="neon-theme"></a>Neon Theme

Lite includes the **Neon** editor theme, a dark theme with vibrant accent colors. It is set as the default theme in Lite and can be changed at any time in `Settings > Appearance > Theme`.

## <a name="comparison"></a>Feature Comparison

| Feature | Free | Lite (One-Time) | Full (Subscription) |
| --- | :---: | :---: | :---: |
| Code editing and syntax highlighting | Yes | Yes | Yes |
| Git integration | Yes | Yes | Yes |
| Extra Keyboard | Yes | Yes | Yes |
| Touch Keyboard and Cursors | Yes | Yes | Yes |
| Project preview | Yes | Yes | Yes |
| Predictive Keyboard | -- | Yes | Gold / Supporter |
| Custom Snippets | -- | Yes | Gold / Supporter |
| Neon Theme | -- | Yes | -- |
| AI Assistant | -- | -- | Yes |
| User accounts and cloud sync | -- | -- | Yes |
| Labs / Community projects | -- | -- | Yes |
