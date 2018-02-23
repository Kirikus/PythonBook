Следующим классом для реализации будет контейнер для карт - описание одной области для хранения карт. В основе нее положим стандартный список из языка Python, который будет содержаться внутри нашего класса в качестве поля cards. Почему не реализовано прямое наследование от класса list? Потенциально, может потребоваться дополнить при наследовании контейнер вспомогательными полями для карт, которые не будут доступны для большинства действий, и при прямом наследовании было бы сложнее дополнить контейнер такими полями. Примером такого контейнера служит колода карт со сбросом, который замешивается как новая колода при ее конце.

Исходя из этого, определеям инициализацию класса.

```py
class Container(object):
  def __init__(self):
    self.cards = []
```

Теперь реализуем метод `__getattr__` для прямого обращения к методам списка карт как к методам класса контейнера. Метод `__getattr__` зовется при неудачной попытке найти атрибут \(метод по названию\) в классе, и в данном случае должен вызывать стандартный механизм поиска во внутреннем списке карт. Это, в свою очередь, означает необходимость вызова метода `__getattribute__`, инициирущего поиск атрибута:

```py
  def __getattr__(self, name):
    return self.cards.__getattribute__(name)
```

Реализация методов `__len__` и `__getitem__`, позволяющих узнавать количество карт в контейнере при помощи функции len и получать карту по их порядковому номеру в контейнере, формально, не нужна из-за реализации предыдущего метода, однако мы ее все же введем для большей прозрачности написанного кода:

```py
  def __len__(self):
    return len(self.cards)

  def __getitem__(self, pos):
    return self.cards[pos]
```

Далее добавляем печать, как и в классе Card. Повторимся, что непосредственная реализация печати в том же классе не является хорошей практикой.

```py
def __str__(self):
  return "%s with %d cards" % (self.__class__.__name__, len(self))

def __repr__(self):
  r = str(self) + "\n"
  for c in self.cards:
    r+= " %s\n" % repr(c)
  return r
```

Наконец, добавим методы-сокращения для более лаконичного доступа к контейнерам как к полю с картами, а не списку абстрактных объектов. Ими будут, пока, добавление, удаление и взятие карт. При добавлении будет проводиться проверка на то, что добавляемый объект является наследником класса Card. Заметим, что такая провека делает функцию добавления карты более дорогой.

```py
  def add_card(self, card):
    if not isinstance(card, Card):
      raise TypeError("Trying to add class %s to %s" % (type(card), self.__class__.__name__))
    self.cards.append(card)

  def draw(self):
    return self.cards.pop()

  def discard(self, card = None, top = False):
    if card is None:
      if top == False:
        return self.pop(random.choice(self.cards))
      else:
        return self.draw()
    else:
      self.remove(card)
      return card
```

```py

```

Наконец, добавляем функцию перемешивания карт:

```py
  def shuffle(self):
    random.shuffle(self.cards)
    return self
```

И импорты:

```py
import random

from card import Card
```


