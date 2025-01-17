# Удаление вирусов с компьютера с помощью ERDC

## 

### **Программный комплекс ERD  Commander** 

**ERD  Commander \(ERDC\)** – набор системных утилит, с помощью которых можно восстановить компьютер даже при очень серьезном сбое. Образ диска есть в сети, его следует скачать, потом записать на CD. С помощью ERDC можно восстановить ПК, например, в случае заражения вирусом-блокировщиком. Во многих ситуациях помогает загрузка в безопасном режиме с поддержкой командной строки, но иногда ПК не загружается даже в таком варианте. В этом случае пригодится ERDC.  
При старте выберите загрузку с компакт-диска, это можно сделать в BIOS или через вызов меню – чаще всего это кнопка F12. После начала загрузки ERDC выберите в появившемся стартовом диалоге вашу версию ОС. Если у вас стоит «семерка», дополнительно ответьте утвердительно на вопрос о переназначении букв дисков так, чтобы они соответствовали дискам ОС. Также выберите русскую раскладку клавиатуры, нажмите ОК.  
После загрузки у вас появится рабочий стол, похожий на рабочий стол Windows. Откройте меню, далее раздел **Administrative Tools** – редактор реестра Registry Editor. Необходимо найти и удалить ключи запуска вируса. Для этого следует просмотреть некоторые ветки реестра. Прежде всего, откройте ветку: HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\WindowsNT\ CurrentVersion\Winlogon. Проверьте, что записано в параметре Shell, отвечающем за загрузку рабочего стола. Он должен иметь значение Explorer.exe. Если записано что-то другое, то это запись вируса. Удалите ее, впишите правильное значение. Также обратите внимание на параметр Userinit – должно стоять значение C:\WINDOWS\system32\userinit.exe, и параметр UIHost – его правильное значение logonui.exe.  
Далее откройте ветку HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows\ CurrentVersion\Run. Здесь находятся программы, автоматически запускаемые при старте. Необходимо внимательно просмотреть список и удалить подозрительные ключи. Для выявления ключей нужен некоторый опыт. Также следует проверить ветку HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Windows, ее параметр AppInit\_DLLs должен не иметь никакого значения \(строка пустая\).  
После этого закройте редактор реестра, проверьте папку автозагрузки: Start - Administrative Tools – Autoruns. Все подозрительные записи из нее следует удалить. Далее перезагрузите ПК, операционная система должна запуститься.

## Ручные и автоматические средства удаления вирусов Windows 

Если на вашем компьютере шпионские программы и другие потенциально нежелательные программы, следует использовать инструмент поиска и удаления шпионских программ, чтобы попытаться их удалить.  
Также можно попробовать удалить шпионские программы вручную. Возможно, нужно будет использовать оба метода несколько раз, чтобы полностью удалить шпионские программы и другие потенциально нежелательные программы.  


### Инструменты поиска и удаления шпионских программ 

Программа Windows Defender – встроенное средство Windows, которая помогает предотвратить заражение компьютера шпионским и другим потенциально нежелательным программным обеспечением  
Если программа Windows Defender запущена, она будет предупреждать о попытках [шпионского и другого потенциально нежелательного](https://windows-school.ru/publ/winfaq/zkov/kak_proverit_zarazhen_li_kompjuter_shpionskoj_programmoj/9-1-0-89) ПО установить и запустить себя на компьютере. Каждый выявленный элемент можно игнорировать, поместить в карантин \(переместить в другое место на компьютере, где программа не сможет запуститься\) или удалить.  
**Средства поиска шпионов** часто добавляются к [антивирусным программам](https://windows-school.ru/blog/populjarnye_besplatnye_antivirusnye_programmy/2013-01-02-28). Если антивирус уже установлен, проверьте, имеет ли она функции защиты от шпионского программного обеспечения. Регулярно сканируйте свой компьютер!  


### Удаление шпионских программ вручную 

Иногда шпионские программы трудно удалить. Если антишпионская программа сообщает, что удалить шпионские программы не удается, следуйте инструкциям предоставленным антишпионской программой.  


### Если это не помогло, попробуйте выполнить следующие действия: 

* Попробуйте установить другую антивирусную или антишпионскую программу. Многие антивирусы поставляются с модулем антишпионской защиты.
* Найдите в разделе Программы и компоненты элементы, которые не принадлежат компьютеру.
  * Откройте «Программы и компоненты» панели управления.

    _Этот метод следует использовать очень осторожно! В панели управления появится много программ, большинство из которых не являются шпионскими. Многие шпионские программы устанавливаются таким образом, чтобы не появляться в разделе «Программы и компоненты». Но, иногда, шпионская программа может иметь параметры удаления, в таком случае ее можно удалить этим методом. Удаляйте только те программы, которые действительно шпионские, и не удаляйте программы, которые могут понадобиться, даже если они используются очень редко._
* Переустановите Windows

  _Некоторые шпионские программы прячутся так надежно, что **их невозможно удалить**. Если при попытке удаления шпионского программного обеспечения оно вновь появляется, возможно, нужно переустановить систему Windows и остальные программ._

**Внимание!** [**Переустановка Windows**](https://windows-school.ru/publ/winfaq/inakt/kak_pereustanovit_windows_7/3-1-0-40) **удалит шпионские программы вместе с другими файлами и программами. Если необходимо переустановить Windows, убедитесь, что создана резервная копия документов и файлов, а также у вас есть все установочные диски для переустановки программ.**

