---
layout: post
title: Открытие файла в PHPStorm по ссылке.
---


Настраиваем переход к нужному файлу по ссылке из браузера в редакторе phpstorm.

При возникновении какой-то ошибки во время разработки, например

![_fatalerror]({{ site.baseurl }}/images/linkphpstorm/fatal.jpg)

приходится копировать адрес скрипта и открывать его в редакторе, чтобы понять и исправить. Оптимизируем эту процедуру и настроим открытие файлов на нужной строке
простым нажатием на ссылку. Для этого нужно настроить редактор и опрерационную систему.

###1 Настройка PHPStorm

В редакторе phpstorm Tools->Create Command-line Launcher

![_phpstormsettings1]({{ site.baseurl }}/images/linkphpstorm/phpstormsettings.jpg)
![_phpstormsettings2]({{ site.baseurl }}/images/linkphpstorm/phpstormsettings2.jpg)
![_phpstormsettings3]({{ site.baseurl }}/images/linkphpstorm/phpstormsettings3.jpg)

###2 Настройка XDebug

Предполагается что xdebug у вас уже установлен, для правильно формирования ссылки добавьте в конфигурацию вот такую настройку

```bash
xdebug.file_link_format = pstorm://%f:%l
```

###3 Настройка OS X

Для настройки операционной системы, в моем случае OS X необходимо создать приложение, для этого в поиске пишем "Редактор скриптов" и открываем окно редактора

![_scripteditor]({{ site.baseurl }}/images/linkphpstorm/scripteditor.jpg)

Скопируйте следующий код 

```bash
on open location this_URL
set AppleScript's text item delimiters to "pstorm://"
do shell script "open -a phpstorm"
do shell script "/usr/local/bin/pstorm '" & text item 2 of this_URL & "'"
end open location
```

Сохраните скрипт Application->PstormHandler

![_scripteditorsave]({{ site.baseurl }}/images/linkphpstorm/scripteditorsave.jpg)

Перейдите в раздел Application (Программы) и кликом правой кнопки мыши на приложении выберите пункт "Показать содержимое пакета" в контекстном меню
 
![_scripteditorsave]({{ site.baseurl }}/images/linkphpstorm/scriptedit.png) 

Затем найдите файл info.plist в папке Contents и окройте его для редактирования

![_info.plist]({{ site.baseurl }}/images/linkphpstorm/scriptedit2.jpg) 


В самый конец файла непосредственно перед тегами 

```xml
</dict>
</plist>
```

Добавьте следующий код

```xml
<key>LSBackgroundOnly</key>
<true/>
<key>CFBundleIdentifier</key>
<string>com.mycompany.AppleScript.Pstorm</string>
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLName</key>
    <string>Pstorm</string>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>pstorm</string>
    </array>
  </dict>
</array>
```

###Сохраните файл и запустите приложение PstormHandler###

Перезагрузите сервер и теперь при получении ошибки и клике на ссылку на пути к файлу вы перейдете в редактор, в котором откроется нужный файл на указанной строке, также вы самостоятельно можете создавать ссылки
вида 
```html
<a href='pstorm:///absolute/path/to/file'>linkname</a>
```




