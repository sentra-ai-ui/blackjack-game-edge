---
name: blackjack-game
description: Play a classic game of Blackjack against the dealer. Uses "new_game", "hit", or "stand" as actions to play.
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following field:
  - action: String. Use "new_game" to start a fresh game, "hit" to draw another card, or "stand" to let the dealer play.

## Game Rules

- The goal is to beat the dealer by having a hand value closer to 21 without going over.
- Number cards (2-10) are worth their face value. Face cards (J, Q, K) are worth 10. Aces are worth 11 or 1 (automatically optimized to your advantage).
- If your hand exceeds 21, you bust and lose immediately.
- The dealer must hit on 16 or less and stand on 17 or more.
- A "blackjack" (Ace + 10-value card on initial deal) beats a regular 21.
- Blackjack pays 3:2.

## Actions

**new_game**: Starts a new round. Shuffles the deck, deals 2 cards to player and dealer (one dealer card face down). Returns the player's cards, the dealer's visible card, and the player's hand total.

**hit**: Draws one additional card for the player. Returns updated player hand and total. If total exceeds 21, player busts and the round ends.

**stand**: Player ends their turn. Dealer reveals hidden card and draws until reaching 17+. Determines winner and returns final results.

## Output

The skill returns a JSON object with a `result` field containing a rendered HTML representation of the game state showing:
- Dealer's hand with one card hidden until round ends
- Player's full hand
- Hand totals
- Game status message
- Instructions for next action

## Tips

- Start with "new_game" to begin
- Say "hit" to get more cards, but be careful not to bust (go over 21)
- Say "stand" when you're satisfied with your hand
- Watch the dealer's visible card to make strategic decisions
