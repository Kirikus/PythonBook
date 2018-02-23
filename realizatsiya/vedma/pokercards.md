Опишем карты. Так как используется обычная колода карт, то назовем новый класс `PokerCard`.

```py
from card import Card

class PokerCard(Card):
  suits = ["clubs", "diamonds", "hearts", "spades"]
  values = ["A", "2", "3", "4", "5", "6", "7", "8", "9", "10", "J", "Q", "K"]
  @staticmethod
  def all_cards():
      return (PokerCard(v,s) for s in PokerCard.suits for v in PokerCard.values)
  def __init__(self, value, suit):
    if suit not in self.suits or value not in self.values:
      raise Exception("Invalid card: %s of %s" % (value, suit))
    self.suit = suit
    self.value = value
  def __eq__(self, other):
    return self.suit == other.suit and self.value == other.value
  def __str__(self):
    return "Poker card"
  def __repr__(self):
    return "%s of %s" % (self.value, self.suit)
```



