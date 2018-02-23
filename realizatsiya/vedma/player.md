Игрок в данной игре обладает рукой, и принимает единственное решение: выбирает карты руки чужого игрока для вытягивания.

```py
import random

from hand import Hand
from player import Player, Computer, Human

class WitchPlayer(Player):
  def __init__(self, name):
    super(WitchPlayer, self).__init__(name)
    self.hand = Hand()
  def card_from_other_hand(self, other):
    return NotImplementedError

class WitchRandomComputer(WitchPlayer, Computer):
  def card_from_other_hand(self, other):
    return random.choice(other.hand)

class WitchHuman(WitchPlayer, Human):
  def card_from_other_hand(self, other):
    while True:
      try:
        print("Choose a card from hand:\n%s\n" % (other.hand))
        chosen = self.hand[int(raw_input())]
        return chosen
      except:
        pass
```





