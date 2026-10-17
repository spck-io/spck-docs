# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Overview

Spck Editor Lite is a one-time purchase version of Spck Editor that unlocks premium editing features without a subscription. It is available as a separate app on both Android and iOS.

Lite includes everything in the free version, plus:

- **Predictive Keyboard** -- context-aware symbol suggestions on the extra keyboard
- **Custom Snippets** -- user-defined code templates with tab-stop placeholders
- **Command Palette** -- find and run editor actions without searching menus
- **Neon Theme** -- an exclusive editor theme
- **Flow Background** -- an exclusive animated background
- **Enhanced Git Integration** -- pull request management, changed-file lists, and read-only commit diffs

Lite keeps these tools unlocked for local projects with a single app purchase, with no Spck account or recurring subscription required. Provider credentials are still needed to access Git remotes and pull requests. Predictive Keyboard, Command Palette, and Enhanced Git Integration are also available with Supporter or Gold in the full app; Custom Snippets requires Gold. Neon and Flow are exclusive to Lite.

## <a name="remote-projects"></a>Remote Projects

Lite also supports **Remote Projects**: edit projects located on your desktop or a public VM through Spck CLI. **Remote Projects require a Spck account and an active Spck subscription**, separate from the one-time Lite app purchase.

Remote connections use Spck's servers, which have ongoing hosting, operation, and maintenance costs. Your subscription helps cover these costs and supports running and maintaining the service.

Run Spck CLI on the computer or VM containing your project, sign in with your subscribed Spck account, and connect from Lite. See [Getting Started with Spck CLI](./cli-start) for setup and [pricing](https://spck.io/pricing) for subscription options. Cloning a Git repository to edit locally is different from editing files on a remote machine; Lite's included local editing and Git tools keep their one-time-purchase access.

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

## <a name="enhanced-git-integration"></a>Enhanced Git Integration

### Pull Request Management

Lite includes the same Premium pull request tools as the full app, with no subscription required:

- **Create pull requests** for GitHub.com, GitLab.com, Bitbucket Cloud, and Azure DevOps repositories.
- **Browse open requests** and check their descriptions, source and target branches, and status.
- **Review changed files** in read-only diffs before deciding whether to merge.
- **Merge or close requests** from the editor, subject to your provider's permissions, reviews, checks, and branch rules.

Save your provider token in **Git menu → Git Credentials**. Use **Git menu → Create PR** for a new request or **Git menu → Pull Requests** to manage existing ones. See [Pull request management](./editor#pull-request-management) for setup and steps. Optional AI drafting requires a configured AI service and is not an AI credit allowance included with Lite.

### Commit File Changes and Diffs

Open **Git > History** and select a commit to see its added, modified, and deleted files. Select a file to view its changes against the commit's first parent in the read-only diff viewer.

Long-press a history entry, or right-click with a mouse, and choose **View Commit** for another way to open it. Reviewing a commit does not change your working files.

Enhanced Git Integration is permanently included with the Lite app purchase, with no login or subscription required. It is also available with an active Supporter, Gold, or Node subscription, or permanently with the Spck for NodeJS terminal lifetime purchase. These options in the full app require login. See [Enhanced Git Integration](./editor#enhanced-git-integration) for details.

## <a name="comparison"></a>Feature Comparison

| Feature | Free | Lite (One-Time) | Full (Subscription) |
| --- | :---: | :---: | :---: |
| Code editing and syntax highlighting | Yes | Yes | Yes |
| Git integration | Yes | Yes | Yes |
| Enhanced Git Integration | -- | Yes | Supporter / Gold / Node |
| Pull request management | -- | Yes | Supporter / Gold / Node |
| Commit file changes and diffs | -- | Yes | Supporter / Gold / Node |
| Merge conflict resolution | Yes | Yes | Yes |
| Extra Keyboard | Yes | Yes | Yes |
| Touch Keyboard and Cursors | Yes | Yes | Yes |
| Project preview | Yes | Yes | Yes |
| Remote Projects (desktop or public VM) | 30 min/day with account | Separate Spck account and subscription | Included within plan limits |
| Predictive Keyboard | -- | Yes | Gold / Supporter |
| Command Palette | -- | Yes | Gold / Supporter |
| Custom Snippets | -- | Yes | Gold |
| Neon Theme | -- | Yes | -- |
| Animated Flow Background | -- | Yes | -- |
| AI Assistant | -- | -- | Yes |
| Cloud sync | -- | -- | Yes |
| Labs / Community projects | -- | -- | Yes |
