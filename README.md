# synth.page

A complete, playable music synthesizer + step sequencer that stores everything in the URL hash. Zero backend. Zero dependencies. Zero libraries. Just raw browser APIs doing heavy creative work.

![synth.page](screenshot.png)

## ✨ Features

### 🎹 Complete Synthesizer
- **Four waveforms**: Sine, Square, Sawtooth, Triangle
- **ADSR Envelope**: Full Attack, Decay, Sustain, Release control
- **Filter**: Low-pass filter with cutoff and resonance
- **Delay Effect**: Feedback delay with time and feedback controls
- **Reverb**: Algorithmically generated impulse response (no audio files!)
- **Master Volume & Compressor**: Clean, professional output

### 🎵 16-Step Sequencer
- 8-row x 16-step grid (pentatonic scale by default)
- Click cells to toggle notes on/off
- Visual playhead animation
- Adjustable BPM (60-200)
- Play/Stop/Loop controls

### 🎹 Interactive Piano
- On-screen piano keyboard (one octave)
- Mouse-clickable keys
- Computer keyboard support:
  - **White keys**: A S D F G H J K
  - **Black keys**: W E T Y U
- Real-time synthesis with current instrument settings

### 🎛️ Custom Knobs
- Drag to adjust all parameters
- Visual feedback with rotating indicators
- All values saved to URL automatically

### 🌐 URL-Based Storage
- **Everything in the hash**: All notes, settings, effects compressed into URL
- **Instant sharing**: Copy URL, share composition
- **No backend**: Everything happens in your browser
- **localStorage backup**: Automatic backup of your work
- **Pattern from textarea.my**: DEFLATE compression + Base64url encoding

### 💾 Progressive Web App
- **Works offline**: Service Worker caching
- **Installable**: Add to home screen on mobile
- **Dynamic favicon**: Pulsing visualization while playing
- **Dynamic title**: Shows BPM and play state

## 🎯 How It Works

### URL Encoding
Every aspect of your composition is serialized into a compact JSON format:

```json
{
  "v": 1,
  "bpm": 120,
  "wave": 0,
  "adsr": [0.01, 0.1, 0.7, 0.3],
  "filter": [2000, 1],
  "delay": [0.25, 0.3],
  "reverb": 0.2,
  "vol": 0.8,
  "scale": 0,
  "grid": "base64-of-bitmask"
}
```

The 16×8 grid is stored as a 128-bit bitmask (only 16 bytes!), then everything is:
1. Compressed with `CompressionStream('deflate-raw')`
2. Base64url-encoded
3. Stored in the URL fragment (`#`)

Result: Entire musical compositions in ~100-200 character URLs!

### Web Audio API Architecture
Built entirely with native browser APIs:

- **Oscillators** → **Filter** → **ADSR Envelope** → **Effects Chain** → **Compressor** → **Master Output**
- Reverb uses mathematically generated impulse response (no audio files needed)
- Delay feedback loop for echo effects
- Dry/wet mixing for reverb

### State Management
- URL hash updates on every change via `history.replaceState()`
- localStorage backup in case of URL issues
- On load: Try URL hash first, fall back to localStorage

## 🚀 Pro Tips

1. **Share Your Music**: Just copy the URL and send it - recipient gets your exact composition
2. **Bookmark Compositions**: Browser bookmarks = your song library
3. **Keyboard Shortcuts**: Use your computer keyboard to play the piano live
4. **Create Patterns**: The 16-step grid is perfect for rhythmic patterns and melodies
5. **Experiment**: Tweak knobs while playing to hear changes in real-time

## 🎨 Design Philosophy

Inspired by both **hardware synthesizers** and **minimal web apps** (like textarea.my):
- Dark theme with monochrome + electric blue accent
- Technical, "studio hardware" aesthetic
- Monospace fonts throughout
- Zero external dependencies
- Single HTML file with embedded CSS/JS
- Everything breathes with generous spacing

## 🛠️ Technical Stack

- **HTML5** + **CSS3** + **Vanilla JavaScript**
- **Web Audio API** for synthesis
- **CompressionStream API** for URL encoding
- **Service Worker API** for offline support
- **PWA Manifest** for installation
- **Zero dependencies** - not a single `npm install`

## 📱 Browser Support

Works in all modern browsers that support:
- Web Audio API
- Compression Streams API
- Service Workers
- ES6+

Tested on: Chrome, Firefox, Safari, Edge (latest versions)

## 🌟 The "Wow" Factor

When someone opens your shared URL:
1. They see a beautiful dark synthesizer interface
2. Browser tab favicon starts pulsing
3. They hit Play and **music comes out** - composed entirely from a URL
4. They realize there's no server, no database, no account
5. They tweak a knob, URL updates silently
6. They share the new URL - their remix is now a link

**This is the "textarea.my for music"** - proving URLs can carry not just text, but entire musical experiences.

## 📄 License

MIT License - Feel free to fork, modify, and share!

---

**Made with ❤️ and Web Audio API**

Live site: [synth.page](https://synth.page)
