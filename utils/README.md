# Launch Web Apps Using Zen Browser

Follow the steps below to set up Zen Browser for launching web apps seamlessly:

1. **Copy the script** to `~/.local/share/omarchy/bin/` on your system.
2. **Update your keybindings** in `hypr/bindings.conf`:

   * Use `omarchy-launch-webapp-zen` to launch apps.
   * Use `omarchy-launch-or-focus-webapp-zen` to launch or focus an existing app window.
3. **Run the following commands** to configure the Zen WebApp profile:

```bash
zen-browser -P "WebApp" -CreateProfile "WebApp"
```

```bash
WEBAPP_PROFILE=$(find ~/.zen -maxdepth 1 -type d -name '*.WebApp' | head -n 1)
```

```bash
DEFAULT_PROFILE=$(find ~/.zen -maxdepth 1 -type d -name '*.Default*' | head -n 1)
```

```bash
cp -r "$DEFAULT_PROFILE/"* "$WEBAPP_PROFILE/" 2>/dev/null || true
```

```bash
mkdir -p "$WEBAPP_PROFILE/chrome"
```

```bash
cat >> "$WEBAPP_PROFILE/user.js" <<'EOF'
user_pref("toolkit.legacyUserProfileCustomizations.stylesheets", true);
user_pref("browser.tabs.closeWindowWithLastTab", true);
user_pref("browser.sessionstore.resume_session_once", true);
user_pref("browser.fullscreen.autohide", true);
user_pref("mod.sameerasw_zen_compact_sidebar_type", "0");
user_pref("zen.view.compact.enable-at-startup", true);
user_pref("zen.welcome-screen.seen", true);
user_pref("zen.widget.linux.transparency", true);
user_pref("ui.systemUsesDarkTheme", 1);
EOF
```

```bash
cat >> "$WEBAPP_PROFILE/chrome/userChrome.css" <<'EOF'
#TabsToolbar,
#nav-bar,
#PersonalToolbar,
#statuspanel,
#sidebar-box {
  visibility: collapse !important;
}
#titlebar {
  visibility: collapse !important;
}
:root[sizemode="normal"] #toolbar-menubar {
  visibility: collapse !important;
}
#toolbar-menubar[autohide="false"] {
  visibility: visible !important;
}
EOF
```

---
