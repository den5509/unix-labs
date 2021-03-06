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
        int children = fork();
        if(children == -1) {
            return 1;
        }

        pid = getpid();
        ppid = getppid();
    
        if(children == 0){
            a = DO_A(a);
        } else {
          b = DO_B(b);
        }
         	 printf("My pid = %d, my ppid = %d, result a = %d, result b = %d\n",
    (int) pid, (int) ppid, a, b);
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
        return x - 1 ;
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


Запуск программы в контейнере без автобилда
^^^^^^^^^^^^^^^^

Команда: **bin/lab4**

.. code-block:: text

    My pid = 12489, my ppid = 12462, result a = 0, result b = 99
    My pid = 12490, my ppid = 12489, result a = 1, result b = 100

Запуск программы в контейнере с автобилдом
^^^^^^^^^^^^^^^^

Команда: **bin/lab4**

.. code-block:: text

    My pid = 37, my ppid = 8, result a = 0, result b = 99
    My pid = 38, my ppid = 37, result a = 1, result b = 100







