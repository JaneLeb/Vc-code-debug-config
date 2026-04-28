<img width="803" height="277" alt="image" src="https://github.com/user-attachments/assets/1f795e50-e9fc-4911-9623-ef780c922283" />

В «Школе 21» mini-verter — это ваш лучший друг перед сдачей проекта. Это локальный скрипт-тестер, который имитирует проверку основного робота (автотеста), чтобы вы не получили 0 за проект из-за какой-нибудь глупой ошибки в Makefile или структуре файлов.
Для запуска такого тестера Docker и Dev Containers — это идеальное решение, потому что робот Вертер работает на Linux (Ubuntu/Alpine), а вы сейчас на Windows.
Как правильно «подружить» проект и mini-verter в VS Code:

Если тестер требует Docker:

Вам нужно создать в папке проекта файл Dockerfile.

В нём обычно прописывается установка компиляторов (gcc, make) и самого тестера.

После этого расширение Dev Containers позволит вам «войти» в это окружение.

Как изменится ваш Makefile для mini-verter:

На Windows мы использовали cl.exe, но Вертер и mini-verter — это про Linux. Ваш Makefile для сдачи в Школу 21 должен выглядеть примерно так (стандартный шаблон):

makefile

    CC = gcc
    CFLAGS = -Wall -Wextra -Werror -std=c11
    SOURCES = main.c
    OBJECTS = $(SOURCES:.c=.o)
    TARGET = s21_program
    
    all: $(TARGET)
    
    $(TARGET): $(OBJECTS)
    	$(CC) $(CFLAGS) $(OBJECTS) -o $(TARGET)
    
    %.o: %.c
    	$(CC) $(CFLAGS) -c $< -o $@
    
    clean:
    	rm -rf $(OBJECTS) $(TARGET)
    
    rebuild: clean all

Почему это важно для mini-verter:

Флаги -Wall -Wextra -Werror: Без них mini-verter может даже не начать тесты. Это требование «Школы 21» к чистоте кода.

Команда rm -rf: На Linux (внутри Docker) для очистки используется именно она, а не del.

Что делать дальше:

Убедитесь, что Docker Desktop запущен у вас в системе.

Если у вас есть папка с mini-verter, положите её в корень вашего проекта.

Обычно запуск тестера в терминале (внутри контейнера) выглядит так: sh mini_verter.sh или через make test.

Вы уже скачали файлы mini-verter? Если да, посмотрите, нет ли там инструкции, какой именно Docker-образ он требует (обычно это указано в README тестера). Это поможет нам настроить Dev Containers так, чтобы тесты проходили с первого раза.


