# F&F Brain Duel — Product Requirements Document

**Version:** 2.0
**Date:** 2026-03-13
**Status:** Draft
**[Privacy Policy](https://alexpcosta.github.io/F-F-Brain-Duel/privacy-policy)** 
---

## 1. Overview

**F&F Brain Duel** is a competitive multiplayer brain-training party game for iOS. Players sit around a shared device (phone or tablet) and compete in turn-based rounds, each presenting a unique cognitive or visual puzzle. The first player to collect 5 "brain stars" wins the game.

The app is designed for casual social play — family game nights, friend gatherings, and group entertainment — requiring no external materials or accessories.

---

## 2. Target Audience

- Families and friend groups looking for a shared-device party game
- Ages 8 and up (challenges are visual and intuitive)
- Players who enjoy puzzles, trivia, and competitive games
- Groups of 2 to 4 players

---

## 3. Supported Platforms

| Device | Players |
|--------|---------|
| iPhone | 2       |
| iPad   | Up to 4 |

The app automatically adapts its layout based on the device type — vertical two-player layout on phones, four-corner layout on tablets.

---

## 4. Languages Supported

- English
- Portuguese (pt-PT)
- Spanish (es)

Language can be changed at any time from the setup screen.

---

## 5. Visual Themes

- Light mode
- Dark mode

Theme can be toggled at any time from the setup screen.

---

## 6. App Flow

```
Setup Screen → Game Screen → [Star Celebration] → [Victory Screen]
                  ↑__________________Play Again____________________|
                                                         New Game → Setup Screen
```

---

## 7. Setup Screen

### 7.1 Purpose

Allows players to configure the game before it begins: who is playing and which challenges will appear.

### 7.2 Player Configuration

- Each player taps their zone (top/bottom on phone, corners on tablet) to register
- A modal prompts for a name (up to 12 characters)
- Each player is automatically assigned a unique avatar color
- Players can tap their zone again to edit their name

### 7.3 Challenge Selection

- All challenge types are shown as toggleable cards
- Players can turn individual challenges on or off
- "Select All" and "Deselect All" shortcuts are available
- A counter shows how many challenges are currently selected (e.g., "5 / 15")

### 7.4 Validation

- At least 2 players must be registered
- At least 1 challenge type must be selected
- The "Start Game" button is disabled until both conditions are met

### 7.5 Additional Controls

- **Rules button**: Opens a modal explaining the full game rules
- **Language selector**: Switch between English, Portuguese, and Spanish
- **Theme toggle**: Switch between dark and light mode

---

## 8. Game Screen

### 8.1 Layout — Phone (2 Players)

- Player 1 zone at the top (rotated 180° to face them)
- Player 2 zone at the bottom
- Challenge card centered between players

### 8.2 Layout — Tablet (Up to 4 Players)

- Four corner zones, one per player
- Top-positioned players are rotated 180° so the screen faces them
- Challenge card displayed large in the center

### 8.3 Player Zone

Each player's zone always shows:

- Their avatar (initial + color)
- Their name
- Their current star count (up to 5 stars needed to win)
- Their card inventory (up to 4 colored dots representing held cards)
- A "READY" button that pulses during the buzz-in phase

### 8.4 Timer

- A visual countdown bar is displayed on the screen edges for both players
- 10 seconds per round during the reveal and buzz-in phases
- Timer starts when the card is revealed
- If time expires, the round ends without a correct answer

---

## 9. Round Flow

Each round goes through the following phases:

### Phase 1 — Tease

- The card back is shown to all players (displays challenge type name and icon)
- No timer is running
- A player taps the card to start the round

### Phase 2 — Reveal

- The card flips to show the full challenge content
- The 10-second timer begins
- All eligible players can buzz in

### Phase 3 — Buzz In

- The first player to tap "READY" becomes the active player
- Other players are locked out
- The timer continues counting down

### Phase 4 — Answer

- The active player gives their answer out loud
- The card is tapped again to reveal the correct answer
- The group verifies if the active player was correct

### Phase 5 — Adjudicate

- **Correct answer**: The active player receives a card of the challenge type
  - If they now hold 2 cards of the same type, those cards combine into 1 brain star
  - If their inventory is full (4 cards), they must discard one card before the star is awarded
- **Wrong answer**: The card is discarded, and the player is blocked for the next round (3+ player games only)

---

## 10. Scoring and Win Condition

### Cards (Inventory)

- Correct answers add 1 card to the player's inventory
- Inventory cap: 4 cards maximum
- Cards are color-coded by challenge type

### Brain Stars

- Every time a player holds 2 cards of the same challenge type, those cards convert into 1 brain star
- Stars are permanent — they cannot be lost
- A player can hold a maximum of 5 brain stars

### Winning

- The first player to collect **5 brain stars** wins immediately
- The game transitions to the Victory Screen

### Discard

- If a player wins a card while already holding 4, a discard modal appears
- The player selects 1 card to remove before the new card is added

### Blocking (3–4 Players Only)

- A wrong answer blocks the player for the following round
- They cannot buzz in during the next reveal phase
- They are automatically unblocked at the start of the round after that

---

## 11. Challenge Types

### 11.1 Memory

**Goal:** Remember all the animals shown, then name them from memory.

- 5 animal images are displayed in a circle
- Players study the animals, then the images are hidden
- Players must recall and name all 5 animals (in any order)
- Answer revealed: names appear next to each image

---

### 11.2 Maze

**Goal:** Find which entry point leads to the center of the maze.

- A grid maze is displayed with 4 labeled entries: A, B, C, D
- Only one path connects an entry to the center
- Players must identify the correct entry letter
- Answer revealed: correct entry highlighted in green

---

### 11.3 Color

**Goal:** Find the one word displayed in its matching color.

- A 3×3 grid shows 9 color words (e.g., "Red", "Blue", "Green")
- Each word is displayed in a color — 8 are mismatched, 1 is correct
- Words may be rotated for extra difficulty
- Players must identify which word matches its color
- Answer revealed: the correct cell is outlined in green

---

### 11.4 Duplicates

**Goal:** Identify the animal that appears twice.

- 13 animal images are scattered across the screen
- 12 different animals are used, plus 1 duplicate
- Images are rotated and slightly offset for visual variety
- Players must find which animal appears twice
- Answer revealed: the duplicate animals are highlighted

---

### 11.5 Frequency

**Goal:** Identify which icon appears most often.

- 15–21 icons of 4 different types are scattered across the screen
- Icons include shapes like hearts, gears, lightbulbs, bells, and others
- One icon type appears more frequently than the others
- Players must name the most frequent icon
- Answer revealed: most frequent icon is circled in green

---

### 11.6 Reveal

**Goal:** Identify the hidden animal as it gradually reveals itself.

- An animal image starts blurred and zoomed in, hiding its identity
- Over 10 seconds, the image slowly comes into focus and zooms out
- Players try to identify the animal as early as possible
- The earlier the correct buzz, the more impressive
- Answer revealed: image fully shown with animal name

---

### 11.7 Odd One Out

**Goal:** Find the single item in a 3×3 grid that does not belong.

- 9 animal or icon images are arranged in a 3×3 grid
- 8 items share a common rule or category; 1 is the outlier
- Players must identify which item breaks the pattern
- Answer revealed: the odd item is highlighted and the shared rule is displayed

---

### 11.8 Shadow Match - comming soon

**Goal:** Match a coloured animal image to its correct silhouette.

- A reference animal image is shown in full colour at the top
- Below it, a 2×2 grid shows 4 silhouette options labelled A–D
- One silhouette is the true shadow of the reference; the others are flipped, rotated, or scaled variants
- Players must identify the correct letter
- Answer revealed: correct silhouette cross-fades to the full-colour image with a green border; wrong options dim to 40% opacity
- Difficulty increases across three tiers (easy/medium/hard) based on how similar the distractors are

---

### 11.9 Pattern Sequence - comming soon

**Goal:** Predict the missing shape in a visual sequence.

- A row of 4 coloured shapes is displayed (circles, squares, triangles, or stars), followed by a "?" placeholder
- Three answer options (A, B, C) show candidate shapes
- The sequence follows a hidden rule — shape cycle only (easy), shape + colour alternation (medium), or three-attribute progression (hard)
- Players must select the shape that comes next
- Answer revealed: correct shape slides into the "?" slot; a rule caption explains the pattern

---

### 11.10 Quick Math Splash - comming soon

**Goal:** Compare groups or solve a simple arithmetic challenge.

- Three sub-modes, determined by difficulty tier:
  - **Comparison (easy):** Two groups of icons side by side — players identify which group has more
  - **Addition (medium):** Two icon groups are shown; players pick the correct total from 3 numeric options (A, B, C)
  - **Balance (hard):** A stylised balance scale shows two sides with icons and weights; players identify the heavier side
- Answer revealed: winning side highlighted in green; for addition, correct option turns green

---

### 11.11 Mirror - comming soon

**Goal:** Identify the correct horizontal mirror reflection of an animal image.

- A reference animal image is shown on one side
- A 2×2 option grid (A–D) shows four transformations of the same image: horizontal flip, vertical flip, 180° rotation, and the unchanged original
- Players must identify which option is the true horizontal mirror
- Answer revealed: correct option is highlighted with a green border; a mirror-line animation draws between the reference and the correct answer

---

### 11.12 Rapid Categories - comming soon

**Goal:** Find the one animal in a 2×3 grid that does not belong to the shown category.

- A category label is displayed (e.g., "Mammals", "Can Fly", "Ocean Animals")
- 6 animal images are shown in a 2×3 grid; 5 belong to the category, 1 is the intruder
- Players must identify which animal does NOT belong
- Answer revealed: the 5 matching animals get green borders; the intruder gets a red ✕ overlay
- 10 semantic categories available (Mammals, Birds, Ocean Animals, Insects, Can Fly, Has a Shell, Lives in Water, Has Stripes, Big Animals, Small Animals)

---

### 11.13 Anagram - comming soon

**Goal:** Unscramble the letters to find the hidden word.

- A set of scrambled letter tiles is displayed alongside a category hint (Animals, Food, Sports, Nature, Objects)
- Three complete word options (A, B, C) are shown below
- Only one option is the word formed by the scrambled letters
- Players must select the correct word
- Answer revealed: correct option pulses green; wrong options fade
- Word pools are fully localised per language (English / Portuguese / Spanish), with difficulty tiers based on word length

---

### 11.14 Silhouette Build - comming soon

**Goal:** Identify which set of pieces can assemble the target silhouette.

- A large target silhouette is shown at the top of the card
- A 2×2 grid (A–D) shows four piece-set options; one correctly assembles the silhouette, three are distractors
- Players must select the correct letter
- Answer revealed: correct option cell gains a green border; incorrect options dim to 35% opacity
- Requires hand-authored puzzle assets; minimum 10 puzzles in the initial pool

---

## 12. Brain Star

When a player earns a brain star, a fullscreen celebration overlay appears:

- Player's name and avatar
- Animated star
- "Amazing!" message
- Auto-dismisses after 2.5 seconds (or tap to skip)

---

## 13. Victory 

Displayed when a player reaches 5 brain stars:

- Crown icon with the winner's name and avatar
- "Congratulations" message
- Final standings table showing all players ranked by stars, then by correct answers
- Two action buttons:
  - **Play Again**: Restart the game with the same players and challenge selection
  - **New Game**: Return to the setup screen to start fresh

