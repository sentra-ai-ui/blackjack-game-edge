---
name: blackjack-game
description: Play Blackjack against the dealer. The LLM tracks game state; JS provides randomness.
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## How It Works

The JavaScript provides randomization (shuffle, deal cards). **The LLM tracks all game state** (hands, totals, deck position) in the conversation context.

## JavaScript Actions

Call the `run_js` tool with `script name: index.html` and `data` as a JSON string with:
- `action`: "shuffle" | "deal" | "evaluate" | "dealer_play"
- `seed`: integer (from shuffle response, for consistency)
- `deckPos`: integer (current position in deck, from previous responses)
- `count`: integer (number of cards to deal, for "deal" action)
- `hand`: array of card indices (for "evaluate")
- `playerTotal`: integer (for determining dealer play outcome)

## Actions

**shuffle**: Initializes a new deck. Returns a seed. Use this at game start.

**deal**: Deals `count` cards. Returns card displays and indices. Use for player/dealer initial hands and hits.

**evaluate**: Calculates total for a hand. Returns total, whether it's blackjack, whether bust.

**dealer_play**: Dealer draws until 17+. Returns dealer hand, total, and game outcome.

## Card Indices

Cards are numbered 0-51:
- 0-12: ♥ (A,2,3,4,5,6,7,8,9,10,J,Q)
- 13-25: ♦
- 26-38: ♣
- 39-51: ♠

Card display format: "A♥", "K♠", "10♦"

## Example Play

1. `run_js({action:"shuffle", seed:12345})` → get seed
2. `run_js({action:"deal", count:4, seed:12345, deckPos:0})` → deal 4 cards (2 each)
3. `run_js({action:"evaluate", hand:[0,25], seed:12345})` → check player's hand
4. `run_js({action:"deal", count:1, seed:12345, deckPos:4})` → hit
5. Continue until stand, then `dealer_play`

## Rules

- Goal: Beat dealer by getting closer to 21 without going over.
- Face cards = 10, Aces = 1 or 11.
- Dealer hits on <17, stands on ≥17.
- Blackjack (21 on first 2 cards) beats regular 21.

## Important

The LLM must maintain game state (hands, deck position, totals) in its context. The JS is stateless - it only generates random values.
