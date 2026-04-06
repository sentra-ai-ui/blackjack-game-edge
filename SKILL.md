---
name: blackjack-game
description: Play Blackjack against the dealer. Just say "start" to begin.
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

Just say **"start"** or **"new_game"** to begin playing!

## Commands

- **start** / **new_game** - Start a new round
- **hit** - Draw another card
- **stand** - Keep your hand, dealer plays

## Rules

- Beat the dealer by getting closer to 21 without going over
- Face cards = 10, Aces = 1 or 11
- Dealer hits on <17, stands on ≥17
- Blackjack (21 on first 2 cards) beats regular 21

The LLM will automatically call the run_js tool with the correct action.
