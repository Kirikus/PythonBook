В данной игре имеется 2 фазы: фаза взятия из руки другого игрока и фаза сбрасывания карт. Последнюю, для удобства, разобьем на две: начальное сбрасывание карт и сбрасывание пары с картой, которую только что получил с руки другого игрока. Также введем проверку на выход игрока из-за стола как отдельную фазу. Наконец, объеденим все эти фазы, составляющие один раунд игры, как отдельную комплексную фазу. Заметим, что именно в фазах добавлена печать об изменениях состояний. Как и говорилось ранее, желательно было бы реализовать ее отдельным классом, однако сейчас это служит хорошим примером того, как может быть реализована запись истории игры, необходимая для отладки.

```py
from phase import Phase
from card import Card
from witch_game import WitchGame

class DiscardPairs(Phase):
  def __init__(self, player):
    self.player = player
    super(DiscardPairs, self).__init__()
  def play(self):
    while True:
      discard = False
      for i in self.player.hand:
      
        for j in self.player.hand:
          if i == j:
            continue
          if i.value == j.value and i != WitchGame().WITCH_CARD and j != WitchGame().WITCH_CARD:
            print("Player %s discards %s and %s" % (self.player.name, repr(i), repr(j)))
            self.player.hand.remove(i)
            self.player.hand.remove(j)
            discard = True
          if discard:
            break
        if discard:
          break
      if not discard:
        break
    print("Player %s now has %s" % (self.player.name, self.player.hand))
    if len(self.player.hand) == 0:
      print("Player %s has left the table" % (self.player.name))
      WitchGame().players.remove(self.player)

class StealCard(Phase):
  def __init__(self, thief, victim):
    self.thief = thief
    self.victim = victim
    super(StealCard, self).__init__()
  def play(self):
    card = self.thief.card_from_other_hand(self.victim)
    self.victim.hand.remove(card)
    self.thief.hand.add_card(card)
    print("Player %s stole a card from Player %s" % (self.thief.name, self.victim.name))

class MainPhase(Phase):
  def play(self):
    game = WitchGame()
    StealCard(game.current_player, game.players[1])()
    DiscardPairs(game.players[1])()
    DiscardPairs(game.current_player)()
    if len(game.players) == 1:
      game.loser = game.players[0]
      return

```



