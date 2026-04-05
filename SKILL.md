---
name: blackjack-game
description: Play Blackjack against the dealer with split and win/loss tracking. Use "new_game", "hit", "stand", or "split".
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## IMPORTANT - State Management

This game requires passing state between turns. The response includes `[STATE:xxx]` at the end which must be passed back on the next action.

When calling `run_js`:
- Include `stateEncoded` in data with the value from `[STATE:xxx]` in the previous response

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with these fields:
  - action: String. One of: "new_game", "hit", "stand", or "split"
  - stateEncoded: String. The base64 state from `[STATE:xxx]` in the previous response. For first call, omit or use empty string.

## Example Calls

**First call (new game):**
```json
{"action": "new_game"}
```

**Subsequent calls (include state):**
```json
{"action": "hit", "stateEncoded": "eyJkZWNrIjpb..."}
```

The LLM should parse the [STATE:...] tag from the previous response and include it in the next call.

## Game Rules

- Goal: Beat the dealer by getting closer to 21 without going over.
- Number cards = face value. Face cards (J, Q, K) = 10. Aces = 1 or 11 (optimized automatically).
- If your hand exceeds 21, you bust and lose.
- Dealer hits on 16 or less, stands on 17+.
- Blackjack (Ace + 10-value on initial deal) beats regular 21.

## Split

- Available when your first two cards have the same rank.
- Splits into two hands. Up to 3 hands max.

## Session Tracking

Win/Loss/Push persists via state between turns.

## Output

Returns:
- Text summary with cards, totals, session score
- Visual webview with card table
- [STATE:xxx] tag at end of text (include in next action)
