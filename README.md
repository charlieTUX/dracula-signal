# Dracula for [Signal desktop](https://signal.org)

> A dark theme for [Signal desktop](https://signal.org).

inspired of [Catppuccin themes](https://github.com/CalfMoon/signal-desktop)

## Install
### Windows
1. Install 7-zip and its asar7z plugin.
2. Open `C:\Users\user_name\AppData\Local\Programs\signal-desktop\resources\app.asar` with 7zip.
3. Go into stylesheets directory.
4. Copy the theme you want to use into the directory.
5. Right click and edit `manifest.css` file and add import statement at the top. `@import "themes.css";` 
Save and close your editor.
6. Enjoy!
### linux 
#### nix flake 

add on input
```nix 
dracula.url = "github:charlieTUX/dracula-signal";
```
and add overlays with 
```
overlays = [
        inputs.dracula.overlays
];
```

#### other linux
Install @electron/asar from npm, i.e. with: 
```bash
npm install -g @electron/asar
```
add variable 
```bash
TEMP=$(mktemp -d) SIGNAL_DIR="/usr/lib/signal-desktop/resources"
```
  > [!NOTE]
  > If using the Flatpak version the Signal directory should be:
  > 
  > `SIGNAL_DIR="/var/lib/flatpak/app/org.signal.Signal/current/active/files/Signal/resources"`

Extract asar into the temporary directory
```bash
asar e "${SIGNAL_DIR}/app.asar" ${TEMP}
```

Download the theme file from this repository
```bash
https://raw.githubusercontent.com/charlieTUX/dracula-signal/refs/heads/main/themes.css" -o "${TEMP}/stylesheets/themes.css"
```

Add import for the Dracula theme to the start of `manifest.css`
```bash
sed -i "1i @import \"themes.css\";" "${TEMP}/stylesheets/manifest.css"
```

Pack the new theme into a new `app.asar` (needs `sudo` in order to write to `/usr/lib`)
```bash
sudo asar p ${TEMP} "${SIGNAL_DIR}/app.asar"
```

## Team

This theme is maintained by the following person(s) and a bunch of [awesome contributors](https://github.com/dracula/foobar/graphs/contributors).

| [![CharlieTUX](https://github.com/charlieTUX.png?size=100)](https://github.com/charlieTUX) | 
| ------------------------------------------------------------------------------------------ | 
| [CharlieTUX](https://github.com/charlieTUX)                                                | 

## Community

- [Twitter](https://twitter.com/draculatheme) - Best for getting updates about themes and new stuff.
- [GitHub](https://github.com/dracula/dracula-theme/discussions) - Best for asking questions and discussing issues.
- [Discord](https://draculatheme.com/discord-invite) - Best for hanging out with the community.

## License

[MIT License](./LICENSE)
