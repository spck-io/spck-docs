# <a name="git-support"></a>Git Support

Spck supports Git for local projects on Android and iOS, in the browser, and in remote projects through Spck CLI. This guide covers provider credentials, pull requests, commit inspection, merge conflict resolution, and platform limitations.

Basic Git integration, commit history, and merge conflict resolution are available in the free version. [Enhanced Git Integration](#enhanced-git-integration) adds pull request management and commit file diffs.

## <a name="git-credentials"></a>Git credentials and pull requests

Open **Git menu → Git Credentials**, select your provider, and save its access token. The token setup and help links below open in a new tab so you can return to Spck and paste the token.

| Provider | Token setup | Permissions for Git and pull requests |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">Create GitHub token</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Setup guide</a> | Select the repository. The creation link preselects **Contents: Read and write**, **Pull requests: Read and write**, and **Metadata: Read**. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">Create GitLab token</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Setup guide</a> | The creation link preselects the `api` scope for merge requests. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">Create API token</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Setup guide</a> | Choose **Create API token with scopes**, select **Bitbucket**, and manually select `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket`, and `write:pullrequest:bitbucket`. API authentication uses your Atlassian account email. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">Create PAT guide</a> | Open your organization's **User settings → Personal access tokens → New Token**, select the organization, and manually select **Code (Read & write)**. |

To create a pull request, commit and push your source branch, then open **Git menu → Create PR**. Select the remote and credentials, choose a different target branch, and enter a title and description. **Generate with AI** can draft the message from committed changes against the branches' merge base; fetch the target branch first. Review the draft before selecting **Create PR**. GitLab creates a merge request.

Creating and managing pull requests is a **Premium feature**, included with [Enhanced Git Integration](#enhanced-git-integration). Lite includes it with the one-time app purchase. In the full app, sign in with an active Supporter, Gold, or Node subscription, or the account that owns the Spck for NodeJS terminal lifetime unlock.

## <a name="pull-request-management"></a>Pull request management (Premium)

Manage pull requests without leaving the editor. Supported remotes are **GitHub.com, GitLab.com, Bitbucket Cloud, and Azure DevOps**; GitLab calls them merge requests.

1. Open a Git project and add the provider's token in **Git menu → Git Credentials**, using the permissions above.
2. Open **Branches menu → Pull Requests**, then choose the remote and credentials to list open requests.
3. Select a request to see its title, description, author, source and target branches, and status.
4. Select a changed file to inspect its read-only diff. This lets you check the proposed changes before merging.
5. Use **Merge** to merge an eligible request, or **Close** to close it without merging. Required reviews, checks, token permissions, and branch rules still apply; drafts and requests with conflicts cannot be merged from this dialog.

Use **Refresh** to reload the list after changes on the provider. The request details also link to the provider for reviews, checks, and other actions.

To start a new request, use **Git menu → Create PR** as described above. If the source branch needs pushing, the dialog offers **Push** before creation. Optional AI drafting uses your configured AI service and its usage limits; it is separate from the pull request access included with Lite.

If creation fails because of token permissions, use the provider's setup link to create or update the token, save it in **Git Credentials**, and retry. Your PR draft is preserved.

## <a name="enhanced-git-integration"></a>Enhanced Git Integration

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

## <a name="git-limitations"></a>Git Limitations

### <a name="git-limitations-overview"></a>Overview

Git uses a different implementation depending on where the project is stored and which version of Spck you use:

| Environment | Git implementation | Main constraints |
| --- | --- | --- |
| Android and iOS apps, including Lite and Spck for NodeJS | Native compiled **libgit2** for local projects | Requires a project in device storage; device resources and filesystem restrictions still apply. |
| Browser and embedded editor | [isomorphic-git](https://isomorphic-git.org/), running in JavaScript | Browser memory, storage, and network restrictions apply. |
| Remote projects through Spck CLI | The host computer's **Git binary** | Uses the host's resources, filesystem, credentials, and installed Git. |

Current mobile builds use native Git instead of loading the browser Git engine. If a local Git operation reports **Native Git requires a device folder**, move the project to device storage. Projects stored only in the editor's browser database cannot use the mobile native Git client.

Pull request management calls the provider's API directly using the token saved in **Git Credentials**. Browser sign-in cookies are not used for these calls, and API responses are not cached so a refresh can retrieve the latest request status and branch information. See [Git credentials and pull requests](#git-credentials) for token permissions and [Pull request management](#pull-request-management) for supported providers and actions.

### <a name="git-limitations-memory"></a>Memory Constraints

- Native Git on Android and iOS performs repository operations outside the JavaScript Git engine. The browser engine's memory constraints should not be treated as a fixed mobile Git limit.
- Native Git still needs available memory and disk space. Large repositories or pack files can exceed a device's resources and cause operations to fail or the operating system to terminate the app.
- Browser Git remains limited by the browser's JavaScript memory and storage budgets. Processing large pack files can require substantial memory, so cloning or fetching large repositories may fail.

> 💡 **Tip**: For large repositories, use shallow clones where possible, or consider working with a smaller subset of the repository.

### <a name="git-limitations-symlinks"></a>Symlink Compatibility

- Browser storage and the editor's device filesystem layer use an **emulated symlink** representation for repositories containing symbolic links.
- Switching mobile Git to libgit2 does not remove the editor's filesystem restrictions or guarantee real operating-system symlinks.
- Emulated links may behave differently with build tools, package managers, or scripts that expect real filesystem symlinks and resolve targets at runtime.
- For projects that require real symlinks, use a remote project on a host whose filesystem and permissions support them.

### <a name="git-limitations-cli"></a>Using the CLI as an Alternative

For large repositories or workflows that need the host's filesystem and Git tools, use a **remote project through Spck CLI**. Git operations then run with the **Git binary on the host system**, while you edit from Spck:

- Repository operations use the host's memory and disk rather than the mobile device's or browser's resources.
- Symlinks follow the host operating system's filesystem support and permissions.
- Use the host's Git tools for commands beyond those exposed by the editor's Git controls.

See [Getting Started with Spck CLI](./cli-start) to connect a host. Remote projects require a Spck account and are subject to your plan's access limits; see [Remote Projects](./editor-lite#remote-projects) for Lite's subscription requirements. Cloning a repository to device storage still uses the mobile app's native Git client.

## <a name="git-related-guides"></a>Related guides

- [Screen Reader Support (Experimental)](./screen-reader-support): accessible navigation, source control controls, and feedback.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration): the Git tools included with the one-time app purchase.
- [Getting Started with Spck CLI](./cli-start): connect a remote project to use the host computer's Git tools.
