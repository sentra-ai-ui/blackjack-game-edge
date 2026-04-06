---
name: blackjack-game
description: Play Blackjack against the dealer. Use "new_game", "hit", or "stand". State is maintained via the game object.
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## How to Play

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with these fields:
  - action: String. One of: "new_game", "hit", or "stand"
  - game: Object (optional, omit on first call). The `game` object from the previous response.

## Example Calls

**First call (new game):**
```json
{"action": "new_game"}
```

**Subsequent calls (include game object):**
```json
{"action": "hit", "game": {"deck": [...], "deckIndex": 4, "playerHand": [...], "dealerHand": [...], "playerStatus": "playing"}}
```

The LLM should include the `game` field from the previous response in all subsequent action calls to maintain game continuity.

## Game Rules

- Goal: Beat the dealer by getting closer to 21 without going over.
- Number cards = face value. Face cards (J, Q, K) = 10. Aces = 1 or 11.
- If your hand exceeds 21, you bust and lose.
- Dealer hits on 16 or less, stands on 17+.
- Blackjack (Ace + 10-value on initial deal) beats regular 21.

## Actions

**new_game**: Start a fresh round.

**hit**: Draw another card. If you reach 21, dealer plays automatically.

**stand**: Keep your hand. Dealer draws until 17+.

## Output

Returns a text summary and an interactive webview with the card table.
