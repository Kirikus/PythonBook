S.O.L.I.D. - мнемонический акроним для пяти основных принципов ООП:

1. Принцип единственной ответственности \(The Single Responsibility Principle\)
2. Принцип открытости/закрытости \(The Open Closed Principle\)
3. Принцип подстановки Барбары Лисков \(The Liskov Substitution Principle\)
4. Принцип разделения интерфейса \(The Interface Segregation Principle\)
5. Принцип инверсии зависимостей \(The Dependency Inversion Principle\)

Рассмотрим каждый из них подробнее.

### Принцип единственной ответственности \(The Single Responsibility Principle\)

Данный принцип гласит, что у любого класса должна быть одна и только одна причина изменяться, т.е. у класса должна быть одна единственная задача. Что это означает на практике? Если какой-то класс исполняет несколько функций, то скорее всего его можно разбить на более малые классы, а старый заменить на один класс, наследующийся от новых.

### Принцип открытости/закрытости \(The Open Closed Principle\)

Этот принцип состоит из двух связанных между собой правил: програмные сущности должны быть открыты для расширения, но закрыты для изменения. Первая половина этого принципа означает, что поведение хорошо написанного класса может быть легко расширено или реализовано через наследование, а вторая половина правила предостерегает от изменений, затрагивающий то, как код используется.

### Принцип подстановки Барбары Лисков \(The Liskov Substitution Principle\)

Единствений из принципов, сохранивший в себе название своего автора, данный принцип не позволяет создавать подклассы, которые не могут использоваться в коде вместо родительского класса.

### Принцип разделения интерфейса \(The Interface Segregation Principle\)

Согласно этому принципу, если на каком-то этапе разработки у класса появились методы, не использующиеся им или не имеющиего у него смысла, то где-то на более раннем этапе не произошло разделения на более малые классы.

### Принцип инверсии зависимостей \(The Dependency Inversion Principle\)

Последний из принципов ограничивает то, как модули должны зависеть друг от друга: модули должны зависеть только от абстракций, которые в свою очередь не должны зависеть от деталей. Вместо этого детали должны зависеть от абстракций.



