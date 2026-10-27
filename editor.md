# <a name="getting-started"></a>Getting Started

## <a name="getting-started-overview"></a>Overview

Spck Editor is a mobile code editing solution with multiple variants designed for developers.

### Versions

#### Spck Editor (Free)

- Basic mobile code editing functionality
- Native Git integration on Android and iOS; browser Git via isomorphic-git

#### Spck Editor Lite

**Price**: One-time payment
**Features**:

- Custom Snippets
- Predictive Keyboard
- Exclusive Neon Theme
- Enhanced Git Integration

Lite includes pull request management and commit file diffs for local projects with no subscription or Spck account required. It also supports **Remote Projects** on your desktop or a public VM, which require a **Spck account and an active Spck subscription**. This subscription helps cover the ongoing cost of running and maintaining the servers. See [Spck Editor Lite](./editor-lite) for the included tools and [Remote Projects](./editor-lite#remote-projects) for details.

#### Spck for NodeJS

**Platform**: Android exclusive
**Key Feature**: Integrated terminal with NodeJS support

Enhanced Git Integration is included with an active Node subscription or permanently unlocked with the terminal lifetime purchase. Sign in to use either option.

#### Browser Version

- Embeddable on any website
- Lightweight code editing interface

See [Embedding the Editor](/en/editor-embed) for iframe setup, project management, and the JavaScript API.

### Key Features

- Mobile-first design
- [Git support and limitations](./git-support)
- Cross-platform compatibility
- [Screen reader support (Experimental)](./screen-reader-support)

### <a name="git-credentials"></a>Git credentials and pull requests

<a name="pull-request-management"></a>

See [Git Support](./git-support) for [provider token setup](./git-support#git-credentials), [pull request management](./git-support#pull-request-management), and [Enhanced Git Integration](./git-support#enhanced-git-integration).

### Recommended Use

- On-the-go code editing
- Quick project modifications
- Learning and prototyping

## <a name="getting-started-terminology"></a>Terminology

| Term             | Description                                                                                                              |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Navigation Menu  | Refers to the First Tab on the side menu on mobile devices, this menu is not available on Browser version or Tablet mode |
| Files Menu       | Refers to the _File_ Tab on the side menu or side bar                                                                    |
| Extra Keyboard   | On mobile devices there exists an extra keyboard with commonly used coding symbols for quick insertion                   |
| Touch Keyboard   | Generally this refers to the row of keys containing the arrow keys, the tab key and more                                 |
| Touch Action Bar | This is the floating menu that pops up above the cursor when text is selected on mobile/touch device                     |
| Touch Cursors    | The on-screen cursors that appear on mobile/touch device when text is selected or cursor is active                       |
| Tablet Mode      | This refers to a setting that can be turned on in larger touch devices like a tablet                                     |
| ⌘ Key            | This symbol on the Touch Keyboard is the same as the Ctrl key on Windows or the Command Key on Mac                       |
| ⌥ Key            | This symbol on the Touch Keyboard is the same as the Alt key on Windows or the Option Key on Mac                         |

&nbsp;

&nbsp;

# <a name="screen-reader-support"></a>Screen Reader Support (Experimental)

Screen reader support is **experimental**. See the [Screen Reader Support guide](./screen-reader-support) for activation, document editing, keyboard navigation, current limitations, and [feedback](./screen-reader-support#screen-reader-feedback).

&nbsp;

&nbsp;

# <a name="keyboard-shortcuts"></a>Keyboard Shortcuts

## <a name="keyboard-shortcuts-overview"></a>Overview

Unlock lightning-fast efficiency with these handy keyboard shortcuts! While not a complete catalog, these gems will supercharge your productivity and make navigation a breeze.

### Key Highlights

- **Not exhaustive**: A curated selection of the most practical shortcuts
- **Purpose**: Boost your workflow with quick, intuitive commands
- **Benefit**: Save time and reduce mouse dependency

> 💡 **Pro Tip**: Memorize these shortcuts, and watch your productivity soar! 🌟

You can view the complete list of shortcuts by going to `Settings > Editor > Keyboard Shortcuts`

For keyboard focus, menu activation, and accessible document editing, see [Screen Reader Support (Experimental)](./screen-reader-support).

> Premium users can also access Keyboard Shortcuts directly from the Extra Keyboard or using the shortcut `⌘ K`

> Enable the Ctrl/Command Key (⌘) and Alt/Options key by turning on `Settings > Touch > Show ⌘ Key` and `Settings > Touch > Show ⌥ Key`

## <a name="keyboard-shortcuts-editor"></a>Editor

| Shortcut | Action                               |
| -------- | ------------------------------------ |
| ⌘ A      | Select All                           |
| ⌘ C      | Copy                                 |
| ⌘ V      | Paste                                |
| ⌘ X      | Cut                                  |
| ⌘ Z      | Undo                                 |
| ⌘ ⇧ Z    | Redo                                 |
| ⌘ D      | Duplicate Line                       |
| ⌘ /      | Comment/Uncomment Line               |
| ⌥ F      | Format Code                          |
| ⌘ F      | Find                                 |
| ⌘ G      | Find Next (Works with selected text) |
| ⌘ ⇧ G    | Find Prev                            |
| ⌘ L      | Jump to Line                         |

## <a name="keyboard-shortcuts-quick-actions"></a>Quick Actions

| Shortcut | Action                              |
| -------- | ----------------------------------- |
| ⌘ ⇧ C    | Git Commit                          |
| ⌘ O      | Open Recent Files                   |
| ⌘ ⇧ P    | Launch Project Preview              |
| ⌘ P      | Toggle File Preview (SVG, Markdown) |
| ⌘ K      | **Supporter+**: Open Shortcuts      |

&nbsp;

&nbsp;

# <a name="touch-settings"></a>Touch Settings

## <a name="touch-settings-extra"></a>Extra Keyboard

- The Extra Keyboard is a symbols keyboard designed for Touch Devices.
- Additional Keys/Symbols can be accessed by press-hold the keys which opens up a menu of options.
- You can enable or disable it in the `Settings > Touch > Extra Keyboard` menu.

> 💡 **Pro Tip**: See _**Advanced Editing**_ for tips on surrounding text which is compatible with the Extra keyboard.

## <a name="touch-settings-touch"></a>Touch Keyboard

- Touch Keys consist of a row of keys including Arrow Keys, Command Key, and other frequently used keys.
- This feature is available on Touch Devices.
- You can toggle it on or off in the `Settings > Touch > Touch Keyboard` section.

> 💡 **Pro Tip**: You can customize individual keys on this keyboard by adjusting settings.

## <a name="touch-settings-action-bar"></a>Touch Action Bar

- An action bar will appear with Copy, Cut, and Paste options when text is selected.
- This feature can be enabled or disabled in `Settings > Touch > Touch Action Bar`.

## <a name="touch-settings-cursors"></a>Touch Cursors

- On-screen cursors that appear when text is selected or cursor is active.
- This feature can be enabled or disabled in `Settings > Touch > Touch Cursors`.

> 💡 **Pro Tip**: It is not recommended to disable this feature unless you have a mouse/pointing device paired with the mobile device. Disabling the touch cursors can improve screen visibility when editing and improve the editing experience when using external pointing devices.

## <a name="touch-settings-predictive"></a>Predictive Keys

- Predictive Keys is a premium feature that supersedes the standard Extra Keyboard.
- Offers one-touch symbol input rather than having to hold-press and select in the regular Extra Keyboard
- Keys are ordered by statistical frequency of symbols appearing in a specific position in the file.
- It can be turned on or off in `Settings > Touch > Predictive Keyboard`.

> 💡 **Pro Tip**: Predictive Keys replaces the regular Extra Keyboard which some users may prefer. Predictive Keys is a default option in the **Lite** version of the editor, and can be turned off to get back the regular Extra Keyboard.

&nbsp;

&nbsp;

# <a name="file-navigation"></a>File Navigation

## <a name="file-navigation-overview"></a>Overview

- There are multiple methods to navigate between files
- You can navigate through files using the Files in Side menu
- You can use the breadcrumb to navigate files starting from the current file directory
- You can open up Recent Files `Ctrl-O` to quickly search for files
- You can use the "Locate" icon in the Files side menu to quickly pinpoint the current files
- The Source Control and Search side menus also offer unique ways to navigate between files

## <a name="file-navigation-tabs"></a>File Tab Management

### Tab Behavior

- Files are automatically unpinned when initially opened
- Tabs become pinned when edits are made

### Tab Sorting Options

Files can be sorted by:

- Alphabetical order
- File extension
- File path

### Alternative Navigation Channels

- **Source Control Menu**: Navigate files through version control context
- **Search Menu**: Find and access files based on search criteria

> 💡 **Pro Tip**: File Tabs can be turned off from view in `Settings > Appearance > Show File Tabs`. See _Zen Mode_ for maximizing screen space on smaller devices.

&nbsp;

&nbsp;

# <a name="advanced-editing"></a>Advanced Editing

## Using the Predictive keyboard efficiently

### Basic Selection

- Double-tap to select a word or text block

### Surrounding Text

Quickly surround selected text using bracket or quote pairs:

- Parentheses: `( )`
- Square brackets: `[ ]`
- Curly braces: `{ }`
- Single quotes: `' '`
- Double quotes: `" "`

### Navigation and Editing

#### Text Search

- `⌘ G`: Find next instance
- `⌘ ⇧ G`: Find previous instance

#### Indentation

- Select a text block
- Press Tab to indent

&nbsp;

## <a name="multiple-cursors"></a>Multiple Cursors

### Quick Setup

- Enable multiple cursors with the Alt/Option key! ✨
- Navigate to `Settings > Touch > Show ⌥ Key` to activate

### How to Use

1. Select both ⌥ and ⌘ keys
2. Click to place cursors exactly where you want them
3. Edit multiple lines simultaneously with ease! 💻

> 💡 **Pro Tip**: Multi-cursor editing = lightning-fast code transformation! ⚡️
> It is also possible to add multi-cursors using the command palette command `Add Cursor Above` and `Add Cursor Below` which would add a cursor directly above or below the current cursor position.

&nbsp;

&nbsp;

# <a name="enhanced-git-integration"></a>Git Support

See the [Git Support guide](./git-support) for provider credentials, pull request management, commit inspection, and Enhanced Git Integration access.

<a name="merge-conflict-resolution"></a>

Basic Git includes [merge conflict resolution](./git-support#merge-conflict-resolution) in the diff viewer, with **Accept Current**, **Accept Incoming**, **Accept Both**, and **Resolve** actions.

## <a name="git-limitations"></a>Git Limitations

<a name="git-limitations-overview"></a>
<a name="git-limitations-memory"></a>
<a name="git-limitations-symlinks"></a>
<a name="git-limitations-cli"></a>

Android and iOS use native libgit2 for local projects; the browser uses isomorphic-git, and remote projects use the host's Git binary. See [Git Limitations](./git-support#git-limitations) for storage requirements, memory constraints, symlinks, and remote alternatives.

&nbsp;

&nbsp;

# <a name="zen-mode"></a>🌟 Zen Mode

## Overview

Zen Mode is a delightful, space-maximizing editor configuration designed to transform your coding experience on compact displays.

Zen mode consists of:

- Turning off `Show Line Numbers` in the settings
- Turning off `Show File Tab`
- Turning off `Touch Action Bar`

### Key Features

#### 🧘‍♀️ Maximized Screen Real Estate

- **Line Numbers Be Gone!**
  - Free up precious horizontal space
  - Prevent text from feeling cramped
  - Embrace the clean, minimalist look

#### 🎨 Streamlined Interface

- **Action Bar Minimization**
  - Say goodbye to cluttered toolbars
  - Utilize alternative input methods:
    - Extra keyboard paste/cut buttons
    - Keyboard shortcuts (`Ctrl-C/Ctrl-V`)

#### 📂 Simplified Navigation

- **File Tab Elimination**
  - `Ctrl-O` becomes your new navigation bestie
  - Cleaner workspace
  - Faster context switching

> 💡 **Pro Tip**: Not everyone's coding style is the same! We recommend experimenting with Zen Mode to see if it resonates with your workflow. Your perfect coding environment is just a few toggles away! 🌈✨
