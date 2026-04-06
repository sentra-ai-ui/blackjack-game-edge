---
name: blackjack-game
description: Play Blackjack against the dealer. 6-deck shoe, auto-shuffle, interactive UI.
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## How to Play

Say **"start"** or **"new_game"** to begin. Cards are dealt automatically.

## Actions

**start / new_game**: Start a new round with fresh hands.

**hit**: Draw another card.

**stand**: Keep your hand. Dealer plays.

## Features

- 6-deck shoe (standard Vegas rules)
- Auto-reshuffles when running low
- Interactive card table UI
- Shows both hands, totals, and cards remaining

## Rules

- Get closer to 21 than the dealer without going over
- Face cards = 10, Aces = 1 or 11
- Dealer hits on <17, stands on ≥17
- Blackjack (21 on first 2 cards) beats regular 21

## Output

Returns text summary and visual webview with the card table.
