### [Signal Desktop](https://signal.org/)

(100% inspired by [catpuccin](https://github.com/CalfMoon/signal-desktop/blob/main/README.md) )

# Usage

# Windows
1. Install 7-zip and its asar7z plugin.
1. Open `C:\Users\user_name\AppData\Local\Programs\signal-desktop\resources\app.asar` with 7zip.
1. Go into stylesheets directory.
1. Copy the theme you want to use into the directory.
1. Right click and edit `manifest.css` file and add import statement at the top. `@import "themes.css";` 
Save and close your editor.
1. Enjoy!

# Linux
1. Install `@electron/asar` from npm, i.e. with:
	```bash
	npm install -g @electron/asar
	```
2. Set required variables for later steps. Replace `<flavor>` with desired Catppuccin flavor (e.g. `mocha`)
	```bash
	TEMP=$(mktemp -d) SIGNAL_DIR="/usr/lib/signal-desktop/resources"
	```
  > [!NOTE]
  > If using the Flatpak version the Signal directory should be:
  > 
  > `SIGNAL_DIR="/var/lib/flatpak/app/org.signal.Signal/current/active/files/Signal/resources"`
3. Extract asar into the temporary directory
	```bash
	asar e "${SIGNAL_DIR}/app.asar" ${TEMP}
	```
4. Download the theme file from this repository
	```bash
	curl "https://raw.githubusercontent.com/charlieTUX/dracula-signal/themes.css" -o "${TEMP}/stylesheets/themes.css"
	```
5. Add import for the Catppuccin theme to the start of `manifest.css`
	```bash
	sed -i "1i @import \"themes.css\";" "${TEMP}/stylesheets/manifest.css"
	```
6. Pack the new theme into a new `app.asar` (needs `sudo` in order to write to `/usr/lib`)
	```bash
	sudo asar p ${TEMP} "${SIGNAL_DIR}/app.asar"
	```
7. Enjoy!

