# <a name="getting-started"></a>Getting Started

## <a name="getting-started-overview"></a>Overview

Spck Editor is a mobile code editing solution with multiple variants designed for developers.

### Versions

#### Spck Editor (Free)

- Basic mobile code editing functionality
- Portable git library integration via isomorphic-git

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
- Git integration
- Cross-platform compatibility

### <a name="git-credentials"></a>Git credentials and pull requests

Open **Git menu → Git Credentials**, select your provider, and save its access token. The token setup and help links below open in a new tab so you can return to Spck and paste the token.

| Provider | Token setup | Permissions for Git and pull requests |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">Create GitHub token</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Setup guide</a> | Select the repository. The creation link preselects **Contents: Read and write**, **Pull requests: Read and write**, and **Metadata: Read**. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">Create GitLab token</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Setup guide</a> | The creation link preselects the `api` scope for merge requests. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">Create API token</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Setup guide</a> | Choose **Create API token with scopes**, select **Bitbucket**, and manually select `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket`, and `write:pullrequest:bitbucket`. API authentication uses your Atlassian account email. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">Create PAT guide</a> | Open your organization's **User settings → Personal access tokens → New Token**, select the organization, and manually select **Code (Read & write)**. |

To create a pull request, commit and push your source branch, then open **Git menu → Create PR**. Select the remote and credentials, choose a different target branch, and enter a title and description. **Generate with AI** can draft the message from committed changes against the branches' merge base; fetch the target branch first. Review the draft before selecting **Create PR**. GitLab creates a merge request.

Creating and managing pull requests is a **Premium feature**, included with [Enhanced Git Integration](#enhanced-git-integration). Lite includes it with the one-time app purchase. In the full app, sign in with an active Supporter, Gold, or Node subscription, or the account that owns the Spck for NodeJS terminal lifetime unlock.

### <a name="pull-request-management"></a>Pull request management (Premium)

Manage pull requests without leaving the editor. Supported remotes are **GitHub.com, GitLab.com, Bitbucket Cloud, and Azure DevOps**; GitLab calls them merge requests.

1. Open a Git project and add the provider's token in **Git menu → Git Credentials**, using the permissions above.
2. Open **Git menu → Pull Requests**, then choose the remote and credentials to list open requests.
3. Select a request to see its title, description, author, source and target branches, and status.
4. Select a changed file to inspect its read-only diff. This lets you check the proposed changes before merging.
5. Use **Merge** to merge an eligible request, or **Close** to close it without merging. Required reviews, checks, token permissions, and branch rules still apply; drafts and requests with conflicts cannot be merged from this dialog.

Use **Refresh** to reload the list after changes on the provider. The request details also link to the provider for reviews, checks, and other actions.

To start a new request, use **Git menu → Create PR** as described above. If the source branch needs pushing, the dialog offers **Push** before creation. Optional AI drafting uses your configured AI service and its usage limits; it is separate from the pull request access included with Lite.

If creation fails because of token permissions, use the provider's setup link to create or update the token, save it in **Git Credentials**, and retry. Your PR draft is preserved.

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

# <a name="keyboard-shortcuts"></a>Keyboard Shortcuts

## <a name="keyboard-shortcuts-overview"></a>Overview

Unlock lightning-fast efficiency with these handy keyboard shortcuts! While not a complete catalog, these gems will supercharge your productivity and make navigation a breeze.

### Key Highlights

- **Not exhaustive**: A curated selection of the most practical shortcuts
- **Purpose**: Boost your workflow with quick, intuitive commands
- **Benefit**: Save time and reduce mouse dependency

> 💡 **Pro Tip**: Memorize these shortcuts, and watch your productivity soar! 🌟

You can view the complete list of shortcuts by going to `Settings > Editor > Keyboard Shortcuts`

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

# <a name="enhanced-git-integration"></a>Enhanced Git Integration

Enhanced Git Integration adds two tools for reviewing and sharing changes:

- **Pull request management:** create requests, browse open requests, inspect changed files and diffs, and merge or close requests. See [Pull request management](#pull-request-management) for setup and steps.
- **Commit inspection:** browse the files changed in a commit and inspect their diffs without changing your working files.

Open the Git panel's **History** tab and select a commit to see its added, modified, and deleted files. Select a file to open a read-only diff against the commit's first parent. For the first commit, files are compared with an empty tree. The viewer uses committed versions, so uncommitted edits do not affect the diff. Binary files cannot be displayed as text diffs.

You can also long-press a history entry (or right-click with a mouse) and choose **View Commit**.

Enhanced Git Integration is included with:

- **Spck Editor Lite:** permanently unlocked by the one-time app purchase, with no login required.
- **Spck for NodeJS terminal lifetime purchase:** permanently unlocked for the account that owns the purchase; login is required.
- **Supporter, Gold, or Node subscriptions:** unlocked while the subscription is active; login is required.

Basic Git integration and browsing commit history remain available in the free version. See [pricing](https://spck.io/pricing) for plan details.

## <a name="merge-conflict-resolution"></a>Resolve merge conflicts

The diff viewer also helps resolve conflicts in your working files. This is part of basic Git integration and does not require Premium.

1. Open a conflicted file from the Git changes list.
2. For each conflict, choose **Accept Current**, **Accept Incoming**, or **Accept Both**. You can also edit the file to combine changes manually.
3. Review the result. Once all conflict markers are removed, select **Resolve** in the diff viewer to stage the resolved file.
4. Resolve any remaining files, then commit the merge.

On touch devices, long-press files or Git entries to open their context menus. Git status letters supplement filename colors so changes are easier to identify.

# <a name="git-limitations"></a>Git Limitations

## <a name="git-limitations-overview"></a>Overview

The editor's Git integration is powered by [isomorphic-git](https://isomorphic-git.org/), a pure JavaScript implementation of Git that runs entirely client-side. While this enables Git operations directly in the browser and on mobile devices without a server, it comes with several constraints inherent to running Git in a sandboxed JavaScript environment.

## <a name="git-limitations-memory"></a>Memory Constraints

- Mobile applications are typically limited to around **50MB of memory** by the operating system.
- Git operations on large repositories may exceed this budget and cause the app to be terminated.
- Reading large pack files (`.pack` files in `.git/objects/pack/`) requires loading significant portions into memory at once, which is not feasible on memory-constrained devices.
- As a result, **cloning or operating on large repositories may fail with out-of-memory errors** on mobile.

> 💡 **Tip**: For large repositories, use shallow clones where possible, or consider working with a smaller subset of the repository.

## <a name="git-limitations-symlinks"></a>Symlink Compatibility

- Symbolic links (symlinks) are **not supported natively** in the browser/mobile sandbox for security reasons.
- The editor uses an **emulated symlink** representation as a workaround so that repositories containing symlinks can still be checked out.
- This emulation may have **compatibility issues** with tooling that expects real filesystem symlinks (e.g., some build tools, package managers, or scripts that resolve symlink targets at runtime).
- Repositories that rely heavily on symlinks may not behave identically to a native Git checkout.

## <a name="git-limitations-cli"></a>Using the CLI as an Alternative

These limitations only apply to the in-app Git client. They do **not** affect the **Spck CLI**, which uses the **native Git binary** on the host system:

- No 50MB memory ceiling — Git operations are bounded only by your machine's available memory.
- Large pack files and large repositories are handled natively.
- Real symlinks work as expected, with full compatibility with other tooling.
- All Git features and plumbing commands are available, not just the subset implemented by isomorphic-git.

> 💡 **Pro Tip**: If you frequently work with large repositories or projects that depend on symlinks, using the Spck CLI for Git operations (clone, fetch, push) — while still editing files in the mobile app — gives you the best of both worlds.

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
