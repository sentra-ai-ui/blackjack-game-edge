# Blackjack Game - AI Edge Gallery Skill

An interactive Blackjack card game skill for the [AI Edge Gallery](https://ai.google.dev/gallery) app.

## Features

- Play classic Blackjack against the dealer
- Visual card table rendered in the chat via webview
- Text fallback also shown in chat
- Automatic ace optimization (1 or 11)
- Blackjack detection (3:2 payout)
- Dealer AI follows standard casino rules

## How to Install

1. Open the AI Edge Gallery app
2. Go to Agent Skills
3. Tap the "Skills" chip to open Skill Manager
4. Tap the (+) button and select "Load skill from URL"
5. Enter: `https://sentra-ai-ui.github.io/blackjack-game-edge`

## How to Play

- **new_game**: Start a fresh round
- **hit**: Draw another card
- **stand**: Keep your hand and let the dealer play

## Rules

- Get closer to 21 than the dealer without going over
- Number cards = face value, Face cards = 10, Aces = 1 or 11
- Dealer hits on 16 or less, stands on 17+
- Blackjack (Ace + 10-value) beats regular 21

## Development

This skill uses:
- `SKILL.md` - Skill metadata and instructions
- `scripts/index.html` - Game logic, state management, passes state to webview
- `assets/webview.html` - Visual card table rendered in chat

## License

MIT
