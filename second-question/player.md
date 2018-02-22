Приступим к нписанию класса игрока. Хотя мы и говорили, что игроки должны, в первую очередь, отвечать за принятие решений, но без выбора конкретной игры нельзя указать даже названий соответствующих методов, поэтому данный класс останется довольно пустым. Реализуем, дополнительно, к нему двух потомков: компьютерного игрока \(ИИ\) и живого игрока \(человека\).

```py
class Player(object):
  def __init__(self, name):
    self.name = name
  def __eq__(self, other):
    return self.name == other.name
  def __nq__(self, other):
    return self.name != other.name
  def __str__(self):
    return "Player %s" % (self.name)
  def __repr__(self):
    return "Player %s" % (self.name)

class Computer(Player):
  pass

class Human(Player):
  pass
```



