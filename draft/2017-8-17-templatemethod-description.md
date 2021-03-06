---
layout: post
title: Паттерн Шаблонный метод
---

Задает "скелет" алгоритма в методе, оставляя определение реализации некоторых шагов субклассам. Субклассы могут переопределять
некоторые части алгоритма без изменения его структуры

## Задача

Реализовать систему приготовления горячих напитков для кафе. Этапы пригототовления для всех напитков общие, но напитки разные и 
каждый из них может иметь особенности, например добавки.

Этапы производства напитка:

+ Вскипятить воду
+ Приготовить напиток
+ Перелить в чашку
+ Добавить дополнения

Виды напитков:

+ Кофе
+ Чай
+ Какао

## Реализация

Абстрактный класс приготовления напитка с реализацией алгоритма приготовления и общими для всех этапами приготовления

```php
abstract class AbstractBeverage
{
    /**
     * Процесс приготовления напитка
     * Шаблонный метод
     */
    public function prepare()
    {
        $this->beforePrepare();
        $this->boilWater();
        $this->brew();
        $this->pourInCup();
        $this->addCondiments();
    }

    /**
     * Операция зацепка
     */
    public function beforePrepare()
    {
        // .... hook
    }

    public function boilWater()
    {
        echo 'Вскипятить воду';
    }

    public function pourInCup()
    {
        echo 'Перелить в чашку';
    }

    abstract public function brew();

    abstract public function addCondiments();

}
```

Реализация напитков
```php
class Coffee extends AbstractBeverage
{

    public function brew()
    {
        echo 'Заварить кофе';
    }

    public function addCondiments()
    {
        echo 'Добавить молоко и сахар';
    }
}
```
```php
class Tea extends AbstractBeverage
{

    public function brew()
    {
        echo 'Заварить чай';
    }

    public function addCondiments()
    {
        echo 'Добавить лимон';
    }

    public function beforePrepare()
    {
        echo 'Приготовить чайный сервиз';
    }
}
```

[Github](https://github.com/atuzlukov/patterns/tree/dev/src/TemplateMethod/Coffee)


## Принципы

**Голливудский принцип** - не вызывайте нас - мы сами вас вызовем

## Участники

+ Application - абстрактный класс с реализацией шаблонного метода
+ MyApplication - конкретный класс с реализацией примитивных методов и операций зацепок при необходимости

## Использование

Паттерн шаблонный метод следует использовать

+ Чтобы однократно использовать общие части алгоритма, а реализацию изменяющихся частей оставлять для реализации подклассами
+ Для объединения в одном классе поведения из нескольких классов с целью уменьшения дублирования кода
+ Для управления расширениями подклассов (операции зацепки hooks)

## Особенности реализации

+ Шаблонный метод должен быть объявлен как final, чтобы подклассы не смогли изменить алгоритм
+ Примитивыные операции должны быть доступны для вызова только из шаблонного метода
+ Четкое разграничение между операциями зацепками и примитивными операциями, последние объявляются абстрактными, чтобы авторы подкласса
четко понимали что обязательно для реализации, а что нет
+ Можно выделить необходимые для замещения операции при помощи префикса

## Ключевые моменты
+ Играет важную роль в повторном использовании кода
+ Абстрактный класс Шаблонного метода может определять конкретные методы, абстрактные методы и перехватчики
+ Шаблонный метод в классе обычно объявляется как final, чтобы субклассы не могли переопределить алгоритм
+ Абстрактные методы реализуются субклассами
+ Перехватчики не делают ничего или определяют поведение по умолчанию и могут переопределяться в субклассах
+ Голливудский принцип указывает на то, что решения должны приниматься модулями высокого уровня, которые знают, как  и когда обращаться
с вызовами к модулям низкого уровня
+ Паттерны Стратегия и Шаблонный метод инкапсулируют алгоритмы; один использует наследование, а другой - композицию
+ Фабричный метод является специализированной версией Шаблонного метода

## Вопросы

1. Что такое операции зацепки (hooks)
2. Какой принцип используется в паттерне Шаблонный метод
3. Какой вид взаимодействия классов используется в паттерне 

## Задачи

1. Реализовать систему проведения платежей, так, чтобы пользователи могли задать цену 
самостоятельно, а также при необходимости уведомить пользователя о проведенном платеже.












