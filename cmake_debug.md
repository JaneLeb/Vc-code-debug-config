Пошаговый гайд для Windows.

1. Установка базовых инструментов
Прежде всего, нужны сами инструменты для сборки кода (компилятор). VS Code сам по себе — это просто текстовый редактор.

Visual Studio Build Tools: Скачайте Visual Studio Installer.
https://visualstudio.microsoft.com/ru/downloads/

При установке выберите рабочую нагрузку «Разработка классических приложений на C++».
Это установит компилятор cl.exe и нужные библиотеки.

CMake: Скачайте и установите CMake (выберите Windows x64 Installer).https://cmake.org/download/
При установке обязательно выберите опцию «Add CMake to the system PATH» (для всех пользователей).

2. Подготовка VS Code
Откройте пустой VS Code и установите два обязательных расширения через иконку «квадратиков» (Extensions):
C/C++ (от Microsoft) — для подсветки кода и дебага.
CMake Tools (от Microsoft) — для автоматизации сборки.


Вот ваш чек-лист для создания нового проекта с нуля, чтобы дебаг работал сразу:

1. Создание папки и кода
Создайте новую пустую папку для проекта.
Откройте её в VS Code (через терминал: code . или через меню File -> Open Folder).
Создайте ваши файлы с кодом (например, main.c).

2. Создание файла CMakeLists.txt
В корне папки создайте файл CMakeLists.txt и вставьте этот стандартный шаблон:

cmake_minimum_required(VERSION 3.10)
project(ИмяВашегоПроекта)

# Перечислите все ваши .c файлы через пробел
add_executable(my_program main.c) 

<img width="956" height="360" alt="cmake1" src="https://github.com/user-attachments/assets/b3861a03-6736-4d2a-8c1d-d045f2378d25" />


3. Первичная настройка (Configure)
Как только вы сохраните CMakeLists.txt, VS Code сам предложит настроить проект. Если нет:
Нажмите Ctrl+Shift+P -> CMake: Configure.

<img width="1036" height="382" alt="image" src="https://github.com/user-attachments/assets/233bb053-c0c8-4b58-802a-bae4e179c3ce" />

Выберите Kit (компилятор): выберите вашу версию Visual Studio (обычно с пометкой amd64 или x86).

5. Проверка режима Debug
Посмотрите на нижнюю синюю полоску. Там должно быть написано CMake: [Debug]: Ready.
Если написано [Release], нажмите на это слово и выберите Debug в выпадающем списке. Без этого точки остановки (breakpoints) не будут работать.
<img width="1370" height="730" alt="image" src="https://github.com/user-attachments/assets/80d95a28-d5ea-49dd-9293-25905dba7458" />

7. Сборка и запуск
Нажмите на кнопку Build в нижней панели (чтобы убедиться, что код компилируется).
Поставьте точку остановки в коде.
Нажмите на иконку "жучка" на нижней синей панели для запуска дебага.

8.Если не запустится — нажмите Ctrl+Shift+P  (выберите там в выпадающем списке "CMake/Build").
<img width="1366" height="742" alt="image" src="https://github.com/user-attachments/assets/ebde142b-e9b4-4138-ae04-160018ac791b" />

Вверху при помощи кнопок со стрелочками "шагайте" построчно - меню слева - все значения переменных на каждом шаге
<img width="1370" height="728" alt="image" src="https://github.com/user-attachments/assets/50b81ae7-77ee-4dfd-b677-bf18238dc011" />



Главные правила, чтобы ничего не ломалось:
Забудьте про папку .vscode: Для CMake-проектов вам больше не нужны файлы launch.json и tasks.json. Если VS Code предложит их создать — отказывайтесь.
Добавление файлов: Если вы создали новый файл (например, utils.c), обязательно допишите его в CMakeLists.txt в строчку add_executable(...) и сохраните файл. CMake сам обновит настройки.
Чистка: Если что-то "глючит", всегда используйте команду Ctrl+Shift+P -> CMake: Delete Cache and Reconfigure. Это лечит 90% проблем.
