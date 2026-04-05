---
name: blackjack-game
description: Play Blackjack against the dealer with split, win/loss tracking, and interactive buttons. Use "new_game", "hit", "stand", or "split".
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following field:
  - action: String. One of: "new_game", "hit", "stand", or "split"

## Game Rules

- Goal: Beat the dealer by getting closer to 21 without going over.
- Number cards = face value. Face cards (J, Q, K) = 10. Aces = 1 or 11 (optimized automatically).
- If your hand exceeds 21, you bust and lose.
- Dealer hits on 16 or less, stands on 17+.
- Blackjack (Ace + 10-value on initial deal) beats regular 21 and pays 3:2.

## Split

- Available when your first two cards have the same rank (e.g., two 8s, two Kings).
- Splits the hand into two separate hands, each with one original card + a new card.
- Same bet is placed on the second hand automatically.
- Each hand is played independently.
- You can split again if the new hand also has matching ranks (up to 3 hands max).

## Actions

**new_game**: Start a fresh round. Resets the table.

**hit**: Draw another card for the current hand. If you bust, auto-moves to next hand (if split).

**stand**: Keep current hand. Auto-plays remaining hands and then dealer draws.

**split**: Split your current hand into two (only available with two cards of same rank).

## Session Tracking

Win/Loss/Push counter persists across the session:
- W = hands won
- L = hands lost  
- P = pushes (ties)

## Output

Returns both:
- Text summary showing all hands, dealer card, totals, and session score
- Interactive webview with visual card table and buttons for all actions

## Tips

- Split 8s and Aces is generally recommended strategy
- Don't split 10s or face cards (already strong hand)
- Watch the dealer's upcard to decide: hit on low totals, stand on high
