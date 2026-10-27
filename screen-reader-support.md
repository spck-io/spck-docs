# <a name="screen-reader-support"></a>Screen Reader Support (Experimental)

Screen reader support is **experimental** and covers core editor workflows. Compatibility can vary with the device, operating system, and screen reader; some controls and advanced editing workflows may still need improvement.

## <a name="screen-reader-activation"></a>Enabling screen reader editing

Enable your screen reader in your device's accessibility settings. On mobile builds that report the screen reader state, Spck automatically switches the active document to an accessible text field. There is no separate editor setting to turn this mode on.

The text field exposes the document contents and filename for reading, selecting, and editing text. Changes use the editor's normal autosave behavior, selection stays in sync with the document, and undo and redo remain available. Switching files updates the contents and filename; read-only documents remain read-only. Turning off the screen reader restores the usual editor on supported builds.

## <a name="screen-reader-navigation"></a>Navigation and controls

Supported workflows include:

- Labels for icon buttons, navigation tabs, file tabs, search controls, and source control actions, using the selected interface language.
- File and project rows that can be activated with a screen reader or keyboard. Folder rows expose their expanded state; with a physical keyboard, use the right and left arrow keys to expand and collapse folders.
- File tabs that expose the active file, and Git status letters that supplement filename colors.
- Settings controls with associated labels and states, and form fields that expose validation errors.
- Named dialogs that keep keyboard focus inside while open and return it to the triggering control when closed. Action menus move focus to their contents and return it when dismissed with Escape.

With a physical keyboard, use **Tab** to move through focusable controls, **Enter** or **Space** to activate buttons, and **Escape** to dismiss action menus. You can also use your screen reader's usual navigation and activation gestures.

## <a name="screen-reader-limitations"></a>Current limitations

- Accessible document editing depends on the mobile app reporting that a screen reader is enabled. The browser and embedded editor do not automatically activate this mode.
- Support currently covers the core workflows above. Advanced editor interactions and other app features may not work equally well with every screen reader.
- Screen reader behavior can vary across app versions, operating systems, and devices. Please report controls that cannot be reached or activated, unexpected focus changes, and issues reading or editing documents.

See [Keyboard Shortcuts](./editor#keyboard-shortcuts) for editing commands and [Git Support and Limitations](./git-support#git-limitations) for the differences between mobile, browser, and remote Git.

## <a name="screen-reader-feedback"></a>Feedback

Please [submit feedback to support@spck.io](mailto:support@spck.io) if a control is unnamed, focus is lost, or reading or editing does not work as expected. Include your Spck app version, device and operating system, screen reader name, and the steps to reproduce the issue.
