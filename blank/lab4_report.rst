.. Весь процесс выполнения лабораторной (скриншоты, текст итд). Кроме команды на запуск контейнера и выводов к работе
.. _lab4:

В работе была исследована возможность использования контейнеров Docker
для сборки и запуска программ.

Заранее были подготовлены (и откорректированы) `исходные файлы
<https://github.com/den5509/lab_unix4/tree/master/work>`_
программы, их можно посмотреть по ссылке или ниже.
Далее программа была выполнена в следующей последовательности:
1. Загрузить операционную систему.
2. Войти в виртуальную машину, контейнер или на удаленный сервер приложений (IP адресом XX.XX.XX.254, пользовательspo_<NN>, пароль спросить у преподавателя).
3. Определить домашний (начальный) каталог текущего пользователя.
4. В домашнем каталоге пользователя создать каталог work.
5. Сделать каталог work текущим каталогом.
6. Создать протокол выполнения лабораторной работы lab4.txt в каталоге work.
9. Скомпелировать, установить и проверить работу программы.

.. Процесс выполнения лабораторной. Кроме команды на запуск контейнера и выводов к работе

Список файлов в каталоге work в подробном формате
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. code-block:: text

    Makefile
    bin
    lab4.txt
    lab4.c
    lab4.h
    pr_a.c
    pr_b.c
    pr_a.h
    pr_b.h

Содержимое файлов исходных текстов программ

Файл **lab4.c**

.. code-block:: c

    #include <sys/types.h>
    #include <unistd.h>
    #include <stdio.h>

    #include "lab4.h"

    int main()
    {
        pid_t pid, ppid;
        int a =  0; 
       int b =  100;
        (void)fork(); 
        pid = getpid();
        ppid = getppid();

        if(fork() == -1){
        	printf("error");
        } else if (fork() == 0){
            a = DO_A(a);
         printf("Children My pid = %d, my ppid = %d,result a = %d,result b = %d\n",(int)pid,(int)ppid,a,b);
       } else {
         b = DO_B(b);
         printf("Parent My pid = %d, my ppid = %d,result a = %d,result b = %d\n",(int)pid,(int)ppid,a,b);
        }
        return 0;
    }


Файл **lab4.h**

.. code-block:: c

    #ifndef DO_A
    #define DO_A(X) pr_a(X);

    #endif /*DO_A*/

    #ifndef DO_B
    #define DO_B(X) pr_b(X);

    #endif /*DO_B*/


Файл **pr_a.c**

.. code-block:: c

    int pr_a( int x ){
        return x + 1;
    }


Файл **pr_b.c**

.. code-block:: c

    int pr_b( int x ){
        return x + 1 ;
    }


Файл **pr_a.h**

.. code-block:: c

    int pr_a( int x );


Файл **pr_b.h**

.. code-block:: c

    int pr_b( int x );

Файл **Makefile**

.. code-block:: text

    lab4:	lab4.o pr_a.o pr_b.o lab4.h
    		gcc lab4.o pr_a.o pr_b.o -o lab4 -lm

    pr_a.o: pr_a.c
    		gcc -c pr_a.c

    pr_b.o:	pr_b.c
    		gcc -c pr_b.c

    lab4.o:	lab4.c lab4.h
    		gcc -c lab4.c

    clean:
    		rm -f lab4 lab4.o pr_a.o pr_b.o

    install:
    		cp lab4 bin/lab4

    uninstall:
    		rm -f bin/lab4


Компиляция программы и установка её в каталог bin каталога work
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Трансляция и компановка программы. Команда: **make lab4**

.. code-block:: text

    gcc -c lab4.c
    gcc -c pr_a.c
    gcc -c pr_b.c
    gcc lab4.o pr_a.o pr_b.o -o lab4 -lm


2. Список файлов в каталоге **work**.

.. code-block:: text

    
    Makefile
    bin
    lab4.txt
    lab4
    lab4.c
    lab4.h
    lab4.o
    pr_a.c
    pr_a.o
    pr_a.h
    pr_b.c
    pr_b.o
    pr_b.h


3. Установка программы в каталог **bin**. Команда: **make install**

.. code-block:: text

    cp lab4 bin/lab4


Список файлов в каталоге work/bin в подробном формате
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Переход в каталог **bin**.


2. Список файлов в каталоге **bin**.

.. code-block:: text

    
    lab4
    source.tar.bz2


Очистка каталога work от вспомогательных файлов
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Возврат в каталог **work**.


2. Удаление вспомогательных файлов.

Команда: **make clean**

.. code-block:: text

    rm -f lab4 lab4.o pr_a.o pr_b.o


Список файлов в каталоге work после очистки
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Команда: **ls -l**

.. code-block:: text

    
    Makefile
    bin
    lab4.txt
    lab4.c
    lab4.h
    pr_a.c
    pr_b.c
    pr_a.h
    pr_b.h


Запуск программы
^^^^^^^^^^^^^^^^

Команда: **bin/lab4**

.. code-block:: text

    Parent My pid = 24, my ppid = 7,result a = 0,result b = 101
    Children My pid = 24, my ppid = 7,result a = 1,result b = 100
    Parent My pid = 25, my ppid = 24,result a = 0,result b = 101
    Children My pid = 25, my ppid = 24,result a = 1,result b = 100
    
    Children My pid = 25, my ppid = 24,result a = 1,result b = 100
    Parent My pid = 25, my ppid = 24,result a = 0,result b = 101
    Parent My pid = 24, my ppid = 7,result a = 0,result b = 101
    Children My pid = 24, my ppid = 7,result a = 1,result b = 100





