# MSN Mockup Tweak Guide

This is a single-file browser app that recreates a Windows XP desktop with MSN Messenger windows.

## Start The App

Open `index.html` directly in a browser, or run a tiny local server:

```bash
cd /home/aguan/lilian/msn-mockup
python3 -m http.server 8000
```

Then visit:

```text
http://localhost:8000
```

## Files

- `index.html` contains all HTML, CSS, and JavaScript.
- `reference/windows-wallpaper.jpeg` is the desktop wallpaper.
- `reference/smile-with-tongue-out.png` is the transparent MSN `:P` emoticon used in chat messages.
- `reference/open-mouthed-smile.png` is the transparent MSN `:D` emoticon used in chat messages.
- `README.md` is this handoff guide.

## Good Next-Session Workflow

Tweak one thing at a time:

1. Pick exactly one target, such as the taskbar color, MSN window position, toast shape, or chat box spacing.
2. Edit only the matching CSS block in `index.html`.
3. Refresh the browser.
4. If it looks right, move to the next target.

This keeps visual changes easy to compare and easy to undo.

## Main CSS Knobs

The most useful sections in `index.html`:

- Lines near `:root`: global color variables and `--taskbar-height`.
- `body`: desktop wallpaper image.
- `.desktop-controls`: settings box position and styling.
- `.window`: shared MSN window border, radius, background, and shadow.
- `.titlebar`: glossy blue window header.
- `.messenger`: contact list window size and starting position.
- `.chat`: chat window size and starting position.
- `.toast`: sign-in popup size, position, animation, and background.
- `.toast-accent`: orange/gold top bar on the popup.
- `.taskbar`: XP taskbar background and height.
- `.start-button`: green Start button.

## Layout Values To Change First

Window positions:

```css
.messenger {
  left: 110px;
  top: 74px;
  width: 315px;
}

.chat {
  left: 455px;
  top: 86px;
  width: 390px;
}
```

Settings box position:

```css
.desktop-controls {
  top: 18px;
  right: 18px;
}
```

Taskbar height:

```css
:root {
  --taskbar-height: 38px;
}
```

## Color Values To Change First

Global XP colors:

```css
:root {
  --xp-blue: #245edb;
  --xp-blue-dark: #0d3ca5;
  --xp-blue-light: #5da5ff;
  --window-border: #2b65ce;
  --msn-green: #36a933;
  --msn-orange: #f2a313;
}
```

The app also uses many local gradients. For one-by-one color tuning, start with:

- `.titlebar` for window header blue.
- `.taskbar` for the bottom bar.
- `.start-button` for the Start button green.
- `.toast` and `.toast-accent` for the MSN sign-in popup.
- `.window` and `.window-body` for the MSN client surface.

## Interaction Code

JavaScript starts near the bottom of `index.html`.

Important functions:

- `makeDraggable(windowEl)`: lets the MSN windows drag around.
- `triggerSigninToast()`: replays the sign-in popup animation.
- `updatePartnerName()`: changes the active chat partner name.
- `appendMessage(text)`: adds a sent chat message to the conversation log.
- `updateClock()`: updates the taskbar clock.

## Current Features

- Windows XP desktop with exact local wallpaper image.
- XP-style taskbar with Start button, task buttons, tray icons, and clock.
- MSN sign-in toast that slides up from bottom right.
- Editable sign-in username and replay button.
- Draggable MSN contact list window.
- Draggable chat window.
- Editable active chat partner name.
- Chat input supports Send button and Enter.
- Typing `:P` or `:p` in the chat input renders the original transparent smile-with-tongue-out MSN emoticon.
- Typing `:D` or `:d` renders the original transparent open-mouthed-smile MSN emoticon.
