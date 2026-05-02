# Chromascope Offline

A static, offline-first camera color scanner, trigger monitor, and palette builder for GitHub Pages.

Live demo: https://shroomtop.github.io/chromascope-offline/

## What it does

Chromascope Offline turns a phone or desktop browser into a local color-analysis field instrument. It uses the device camera, samples a movable region of interest, converts the sampled color into practical color formats, lets you capture palettes, and can fire local visual/audio/vibration alerts when a configured color rule is matched.

Core capabilities:

- Live camera color sampling from a draggable/resizable ROI
- Rear-camera preference on mobile browsers
- HEX, RGB, HSL, HSV, luminance, contrast, and nearest-name readouts
- Stability/confidence feedback for noisy lighting or unstable frames
- Palette capture, editing, persistence, import, and export
- Trigger rules for hue, saturation, value, and luminance
- Red hue wraparound support near 0/360 degrees
- Local event log for trigger activations
- Full-state backup/export/import
- Static deployment with no backend, no build step, no analytics, and no external API dependency

## Privacy and offline model

This app is designed to run locally in the browser.

- Camera frames are processed in the browser.
- Palette, settings, ROI, trigger history, and app state are stored locally.
- There is no analytics code.
- There is no tracking code.
- There is no backend service.
- There are no external API calls required for core functionality.

Camera permission is controlled by the browser and operating system. If permission is denied, the app should remain usable for palette/export/settings workflows and show a clear camera status instead of silently failing.

## How to use

1. Open the live GitHub Pages link.
2. Tap **Start Camera**.
3. Grant camera permission when prompted.
4. Move or resize the ROI over the target color.
5. Watch the live color readout and stability/confidence indicators.
6. Capture colors into the palette as needed.
7. Configure trigger rules if you want an alert when the sampled color enters a target range.
8. Export palette data or full app state from the export panel.

## Main tabs

### Scan

Primary live camera workflow. Use this to start/stop the camera, position the ROI, inspect the sampled color, lock/reset ROI, and monitor quality indicators.

### Trigger

Configure detection rules using hue, saturation, value, and luminance thresholds. Trigger actions are local only: visual alert, optional Web Audio beep, optional vibration on supported mobile browsers, and local history entry.

### Palette

Capture sampled colors, name/edit/delete entries, copy color values, and manage saved colors locally.

### Export

Export palette data or full app state. Supported practical formats include JSON, CSV, CSS variables, and a Tailwind-like color object. Full-state export/import is intended for backup and migration between browsers/devices.

### Settings / Help

Contains onboarding, calibration controls, local-state controls, diagnostics, and usage notes.

## Browser compatibility

Best target:

- Android Chrome / Chromium-based mobile browsers
- Desktop Chrome / Edge
- GitHub Pages over HTTPS

Expected constraints:

- Camera access requires HTTPS or localhost.
- iOS/Safari camera behavior may differ from Chrome.
- Browser vibration support is inconsistent and may be disabled by the OS/browser.
- Web Audio beeps usually require a user gesture before sound can play.
- Camera exposure, white balance, and autofocus are browser/device controlled and can affect readings.

## Known limitations

This is a browser field tool, not a calibrated spectrophotometer.

- Color accuracy depends on camera sensor, lighting, exposure, white balance, screen glare, and target material.
- Flicker/PWM warnings are heuristic, not laboratory measurement.
- Nearest named color is approximate and based on the embedded local color list.
- Calibration controls help normalize readings but cannot fully correct all camera/lighting bias.
- GitHub Pages deployment means this remains a static app with no server-side sync.

## Export formats

Palette export options:

- JSON
- CSV
- CSS custom properties
- Tailwind-like JavaScript object

State export:

- Full app-state JSON backup containing settings, palette, ROI, trigger configuration, and local history where supported.

## Development notes

The project is intentionally static and GitHub-Pages-friendly:

- `index.html` contains the app shell, embedded CSS, and embedded ES6 JavaScript.
- `README.md` documents the current live app behavior.
- No npm install is required.
- No server runtime is required.
- No build artifacts are required.
- Keep future changes compatible with direct static hosting.

Recommended engineering rules for future edits:

- Preserve the local-first privacy model.
- Avoid external dependencies for core camera/color behavior.
- Keep camera lifecycle handling defensive.
- Stop media tracks when the camera is stopped.
- Keep ROI-to-video coordinate mapping correct when the video is letterboxed.
- Test on Android Chrome before release.
- Keep errors visible in the UI.

## Changelog summary

### Current documented release

- Professional offline field-instrument UI
- Mobile-first bottom navigation and dashboard panels
- Camera lifecycle handling with visible status
- Draggable/resizable/lockable ROI workflow
- Live color readouts with multiple color spaces
- Palette capture and export workflows
- Trigger configuration and local event logging
- README expanded from placeholder to full product documentation

## Manual release checklist

Before merging a release branch:

- [ ] App loads on GitHub Pages without console-breaking syntax errors
- [ ] Start Camera requests permission and prefers rear camera on mobile
- [ ] Denied camera permission produces a visible, understandable state
- [ ] ROI drag/resize/lock/reset works on touch and pointer devices
- [ ] Color readouts update from the ROI
- [ ] Palette capture persists after refresh
- [ ] Trigger arm/disarm works
- [ ] Trigger history can be cleared
- [ ] Palette export works
- [ ] Full-state export/import works
- [ ] README matches actual app behavior
