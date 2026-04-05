---
name: blackjack-game
description: Play Blackjack against the dealer with split and win/loss tracking. Use "new_game", "hit", "stand", or "split".
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## IMPORTANT - State Preservation

This game maintains state between turns. **You MUST include the `state` object from the previous response in every action call.**

When calling the `run_js` tool:
- Include the `state` field from the previous response as `data.state`
- This allows the game to track the current hand, deck, and session score

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with these fields:
  - action: String. One of: "new_game", "hit", "stand", or "split"
  - state: Object. The `state` object from the previous response (to maintain game continuity)

## Example Calls

**First call (new game):**
```json
{"action": "new_game"}
```

**Subsequent calls (hit, stand, split):**
```json
{"action": "hit", "state": <copy the entire state object from previous response>}
```

## Game Rules

- Goal: Beat the dealer by getting closer to 21 without going over.
- Number cards = face value. Face cards (J, Q, K) = 10. Aces = 1 or 11 (optimized automatically).
- If your hand exceeds 21, you bust and lose.
- Dealer hits on 16 or less, stands on 17+.
- Blackjack (Ace + 10-value on initial deal) beats regular 21.

## Split

- Available when your first two cards have the same rank.
- Splits the hand into two separate hands.
- Same bet is placed on the second hand automatically.
- Up to 3 hands max.

## Actions

**new_game**: Start a fresh round.

**hit**: Draw another card for the current hand.

**stand**: Keep current hand. Auto-plays remaining hands and then dealer draws.

**split**: Split your current hand into two (only with matching cards).

## Session Tracking

Win/Loss/Push counter persists across the session via the state object.

## Output

Returns:
- Text summary with cards, totals, session score
- Interactive webview with visual card table
- State object (include in next action call)
