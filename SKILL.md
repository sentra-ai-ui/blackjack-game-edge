---
name: blackjack-game
description: Play a classic game of Blackjack against the dealer in an interactive card game. Get dealt cards, decide to hit or stand, and try to beat the dealer without going over 21.
metadata:
  homepage: https://github.com/sentra-ai-ui/blackjack-game-edge
---

# Blackjack Game

## Instructions

Call the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following fields:
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

The skill returns a JSON object with:
- result: String describing the current game state and outcome
- gameState: Object containing:
  - playerCards: Array of card objects {suit, rank, display}
  - dealerCards: Array of card objects (hidden card shown as "??" until round ends)
  - playerTotal: Number (or "blackjack")
  - dealerTotal: Number (or "blackjack", "?" if hidden)
  - status: String (playing/bust/blackjack/dealer_bust/win/lose/push)
  - message: String describing what happened
- webview: An interactive HTML view showing the current cards and action buttons

## Tips

- Start with "new_game" to begin
- "Hit" to get more cards, but be careful not to bust (go over 21)
- "Stand" when you're satisfied with your hand
- Watch the dealer's visible card to make strategic decisions
