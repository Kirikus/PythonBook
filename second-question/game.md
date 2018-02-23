Сделаем заготовку класса игры.

Заметим, что потенциально многие различные объекты могут хотеть иметь доступ к целому состоянию игры. Например, игроки для принятия решений или же фазы игры для изменений каких-либо состояний мира. Чтобы не передавать указатель на игру при каждом вызове сделаем ее представителем класса синглтон:

```py
class Singleton(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super(Singleton, cls).__call__(*args, **kwargs)
        return cls._instances[cls]
```

Классы - синглтоны при создании своего первого представителя сохраняют указатель на него, а при каждой последующей попытке создать нового представителя возвращают указатель на первый созданный объект. Вот как выглядит создание класса игры, являющегося синглтоном:

```
from singleton import Singleton

class Game(object):
  __metaclass__ = Singleton
```

Без ограничения общности можно полагать, что любая игра содержит в себе список из участвующих в ней игроков, ведется до определения победителя или проигравшего и передает ход от игрока к игроку. Конкретные игры могут поменять порядок передачи хода или же полностью отказаться от концепции "активного игрока", но большая часть игр удовлетворяет этому критерию.

```py
  def __init__(self, players, phase):
    self.players = players
    self.current_player = players[0]
    self.phase = phase
    self.winner = None
    self.loser = None

  def next_player(self):
    self.current_player = self.players[1]
    self.players = self.players[1:] + self.players[:1]
```

Добавим печать:

```py
  def __repr__(self):
    ret = ""
    for player in self.players:
      ret = ret + repr(player)
    return ret

  def __str__(self):
    ret = ""
    for player in self.players:
      ret = ret + str(player)
    return ret
```

Последним шагом служит добавление основного игрового цикла игры, который позволит запускать игру методом `play`. Можно было, впрочем, не вносить его в данный класс, оставив его исключительно статичным объектом.

```py
  def play(self):
    while True:
      self.phase()()
      if self.loser:
        print ("Player %s has lost a game" % self.loser.name)
        break
      if self.winner:
        print("%s has won!" % self.winner.name)
        break
      self.next_player()
```



