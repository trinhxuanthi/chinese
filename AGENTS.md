# 汉语学习应用 (Chinese Learning App) - Agent Instructions

## Project Overview
This is an interactive Chinese vocabulary learning application built with vanilla HTML/CSS/JavaScript. The app teaches Chinese characters (hanzi) with pinyin pronunciation and tracks user progress through localStorage.

**Key Features:**
- Character/pinyin recognition practice
- Audio pronunciation support
- Two study modes: sequential or weak-word review
- Progress tracking and scoring system
- Vietnamese language UI
- Responsive single-page design

## Architecture

### Files & Responsibilities
- `index.html` - Single-page app markup with mode selector, word card, input field, and controls
- `script.js` - Main application logic (state management, event handlers, rendering)
- `style.css` - Responsive styling with CSS variables for theming
- `data/lesson1.js` - Vocabulary data export (`vocabulary` array with hanzi, pinyin, meaning)

### Data Structure
Each vocabulary entry (lesson1.js):
```javascript
{ 
  hanzi: "你好",          // Chinese character(s)
  pinyin: "ni hao",       // Romanized without tones (for input comparison)
  pinyinTone: "nǐ hǎo",  // Romanized with tone marks (for display)
  meaning: "Xin chào"     // Vietnamese translation
}
```

Extended on first load with score tracking:
```javascript
{ ...entry, score: 0, lastReviewed: 0 }
```

### State Management
Managed in `script.js`:
- `wordList` - Array of vocabulary with scores (persisted to localStorage)
- `currentIndex` - Current position in list
- `isAnswered` - Whether current word is revealed
- `mode` - Study mode: 'sequential' or 'priority' (weak words)
- `autoNextTimeout` - Prevents rapid re-triggering during auto-advance

**Storage Keys:**
- `'chinese_app_lesson1'` - Serialized wordList with progress
- `'chinese_app_mode'` - Selected study mode

## Development Workflow

### Running the App
Use any local web server (no build step required):
```bash
# Python 3
python -m http.server 8000

# Node.js http-server
npx http-server

# VS Code Live Server extension
# Right-click index.html → Open with Live Server
```
Then open http://localhost:8000 (or configured port).

### Adding New Vocabulary
1. Create new lesson file: `data/lesson2.js`, `data/lesson3.js`, etc.
2. Follow the vocabulary array structure from `data/lesson1.js`
3. Update `script.js` imports and storage keys if adding multiple lessons

### Debugging Tips
- Open DevTools (F12) → Application tab → LocalStorage to inspect stored progress
- Check Console for rendering/event errors
- The `renderWord()` function drives all UI updates

## Code Conventions

### CSS
- CSS variables defined in `:root` (colors, spacing)
- BEM-like naming: `.mode-selector`, `.btn-primary`, etc.
- Responsive: single-column layout, max-width 460px

### JavaScript
- Functional programming style, not classes
- DOM elements cached in `DOM` object at load time
- All state in `state` object for easy access
- Event listeners registered in `registerEvents()` function

### HTML
- Semantic structure: header controls, card display, input, buttons
- Vietnamese text for labels (UI language)
- Chinese characters/pinyin/meaning in separate divs for styling

## Browser Compatibility
- Modern browsers (ES6 support required)
- localStorage API required for progress persistence
- No external dependencies or build tools needed

## Common Customizations
- **Add lessons:** Create `data/lesson*.js` and duplicate the state/storage pattern
- **Change theme:** Update CSS variables in `:root`
- **Add features:** Extend state object, add handlers in `registerEvents()`, create new render functions
- **Modify vocabulary:** Edit `data/lesson1.js` entries

---

**For Live Server development:** Use VS Code Live Server extension or `npx http-server` for instant reload on save.
