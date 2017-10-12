---
layout: post
title: Глоссарий разработчика
---

Термины и определения для однозначной интерпретации различных понятий и использования в рабочей группе. 


### Инкапсуляция  
закрытие от внешней программы. Говорят что содержание объекта инкапсулировано, 
т.е. изменение состояния объекта возможно только через его методы.

[wikipedia](https://ru.wikipedia.org/wiki/Инкапсуляция_(программирование))

### Экземпляр класса
Говорят, что объект является экземпляром класса

### Сигнатура операции
Имя операции, параметры и значение возвращаемое операцией

### Интерфейс
Множество сигнатур всех определенных для объекта операций. Интерфейс объекта ничего не говорит о его реализации. 
Разные объекты вправе реализовывать разные параметры по-разному

### Тип
Имя используемое для обозначения конкретного интерфейса. Говорят, что объект имеет тип Window, 
если он готов принимать запросы на выполнение любых операций, определенных в интерфейсе с именем Window

### Динамическое связывание
Ассоциация запроса с объектом и одной из его операций во время выполнения. Означает, 
что отправка запроса не определяет конкретной реализации до его выполнения

### Полиморфизм
Возможность во время выполнения подставить вместо одного объекта другой, если он имеет точно такой же интерфейс

### Класс
Спецификация внутренних данных объекта и его представление, а также  операций, которые он может выполнять

### Подкласс
Когда некий класс наследует другой класс говорят, что он является подклассом, 
при этом тот класс от которого происходит наследование именуется **Родительским**

### Абстрактный класс
Предназначен для определения общего интерфейса  для всех своих подклассов. Делегирует реализацию частично или полностью 
всем своим подклассам. У такого класса не может быть экземпляров.

### Композиция объектов
Альтернатива наследованию класса, когда новая функциональность получается путем объединения или композиции объектов (black box reuse)



