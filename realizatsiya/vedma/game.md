Класс игры содержит в себе стартовую подготовку - создание колоды карт, раздачу ее игрокам и предварительное сбрасывание карт. Обратим внимание на место импорта: имеются импорты внутри методов класса. Это сделано для того, чтобы избежать циклической зависимости при инициализации игры.

```py
from game import Game
from deck import Deck
from card_poker import PokerCard

WITCH_CARD = PokerCard("Q", "spades")
LOST_CARD = PokerCard("Q", "clubs")

class WitchGame(Game):

  def __init__(self, players):
    from witch_phases import MainPhase
    super(WitchGame, self).__init__(phase = MainPhase, players = players)
    deck = Deck.full_deck(PokerCard)
    deck.remove(self.LOST_CARD)
    deck.shuffle()
    for card in deck:
      self.current_player.hand.add_card(card)
      self.next_player()
    from witch_phases import DiscardPairs
    for player in self.players:
      DiscardPairs(player)()
```



