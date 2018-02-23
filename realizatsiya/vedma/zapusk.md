Мы готовы для запуска игры. Запустим ее с несколькими игроками - Алисой, Бобом, Кэролом и Дэйвом:

```py
from witch_game import WitchGame
from witch_player import WitchHuman, WitchRandomComputer

if __name__ == "__main__":
  WitchGame([
    WitchRandomComputer("Alice"),
    WitchRandomComputer("Bob"),
    WitchRandomComputer("Carol"),
    WitchRandomComputer("Dave")
  ]).play()
```



