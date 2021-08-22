---
description: '28.04.2016 http://www.cyberforum.ru/tags/'
---

# Расшифровать текст, найти правильный пароль

## Q

Скажите, пожалуйста, ответ. Сам задачу выполнить не могу, не работает ни одна библиотека\(pycrypto, simplecrypt, simplecripto, crypto, cryptography\) по криптографии. Работает только библиотека RSA, но я не понял, как можно с ее надо применить для этой задачи  
Или другой способ расшифровать данные

```text
Алиса владеет интересной информацией, которую хочет заполучить Боб.
Алиса умна, поэтому она хранит свою информацию в зашифрованном файле.
У Алисы плохая память, поэтому она хранит все свои пароли в открытом виде в текстовом файле.
Бобу удалось завладеть зашифрованным файлом с интересной информацией и файлом с паролями, но он не смог понять какой из паролей ему нужен
```

Помогите ему решить эту проблему.

```text
Алиса зашифровала свою информацию с помощью библиотеки simple-crypt.
Она представила информацию в виде строки, и затем записала в бинарный файл результат работы метода simplecrypt.encrypt.
Вам необходимо установить библиотеку simple-crypt, и с помощью метода simplecrypt.decrypt узнать, какой из паролей служит ключом для расшифровки файла с интересной информацией.
```

## A

Ответом для данной задачи служит расшифрованная интересная информация Алисы.  
  
Файл с информацией : [https://stepic.org/media/attachments/lesson/24466/encrypted.bin](https://stepic.org/media/attachments/lesson/24466/encrypted.bin)  
Файл с паролями : [https://stepic.org/media/attachments/lesson/24466/passwords.txt](https://stepic.org/media/attachments/lesson/24466/passwords.txt)

### Примечание:

  
Для того, чтобы считать все данные из бинарного файла, можно использовать, например, следующий код:

> ```text
> Python
>
> with open("encrypted.bin", "rb") as inp:
>     encrypted = inp.read()
> ```

## Решение

Код

```text
pip install simple-crypt
```

```text
Python

import requests
from simplecrypt import decrypt, DecryptionException
 
code = requests.get('https://stepic.org/media/attachments/lesson/24466/encrypted.bin').content
passes = requests.get('https://stepic.org/media/attachments/lesson/24466/passwords.txt').content
 
for p in passes.split():
    try:
        s = decrypt(p, code)
    except DecryptionException:
        pass
    else:
        print(p, s)
```

Проблема в том, что интерпретатор не видит этот модуль и я не могу им воспользоваться  


