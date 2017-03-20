---
layout: post
title: Telegram send message.
---


Возникла необходимость сделать отправку уведомлений об ошибках, которые происходят на сайте в канал телеграма, задача на первый взгляд не сложная, но есть некоторые детали, с которыми столкнулся в процессе разработки.

Сначала нужно создать публичный канал в телеграме, именно публичный, в дальнейшем можно будет сделать его приватным

![_config.yml]({{ site.baseurl }}/images/telegram_send_message/create_channel.jpg)

Затем создать бота, если его еще нет, как создать нового бота описано здесь <https://core.telegram.org/bots#6-botfather>

После того как бот будет создан и ему будет задано имя *botfather* вернет токен вида 

**110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw**

Далее необходимо сделать администратором канала, который был создан ранее этого бота, для этого нужно перейти в настройки канала и в разделе администраторов указать имя бота **@botname**

Теперь вы можете отправлять в канал сообщения, чтобы проверить перейдите по ссылке (не забудте подставить в нее токен и название канала)
```php
https://api.telegram.org/bot{{Укажите тут токен бота}}/sendMessage?chat_id={{Укажите название канала}}&text=hello!
```
Рабочая ссылка будет выглядеть примерно так
```php
https://api.telegram.org/bot110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw/sendMessage?chat_id=@channelname&text=hello!
```
Если скопировать эту ссылку в браузер, то в результате получим: 
```php
{
    "ok":true,
    "result":{
        "message_id":12,
        "chat":{
            "id":-1001074775555,
            "title":"channelname",
            "type":"channel"
        },
        "date":1488892694,
        "text":"hello!"
    }
}
```
Параметр  **id** это уникальный идентификатор канала, запомните его

Чтобы сделать канал приватным нужно в его настройках удалить ссылку, а при отправке сообщения в параметр **chat_id** передать значение уникального идентификатора канала 
таким образом ссылка для отправки сообщения будет выглядеть вот так:
```php
https://api.telegram.org/bot110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw/sendMessage?chat_id=-1001074775555&text=hello!
```
На этом настройка на стороне телеграма завершена, если вам нужно отправить сообщение из кода, то можете использовать примерно вот такой код

```php

$ch = curl_init();
$url = 'https://api.telegram.org/bot110201543:AAHdqTcvCH1vGWJxfSeofSAs0K5PALDsaw/sendMessage';
$message = "Сообщение для отправки \n в <b>канал уведомлений</b>";

curl_setopt($ch, CURLOPT_URL, $url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query([
    'text'       => $message,
    'chat_id'    => '-1001074775555',
    'parse_mode' => 'html',
]));

curl_exec($ch);
        
```

Полный список доступных параметров можно рассмотреть здесь <https://core.telegram.org/bots/api#sendmessage> . Для форматирования сообщения можно использовать html и markdown.


Хотелось бы обратить внимание, что в тексте сообщения для переноса строки нужно использовать \n, чтобы он был интерпретирован как перенос
строки необходимо указывать его в двойных кавычках. 