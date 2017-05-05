.. Процесс выполнения лабораторной. Кроме команды на запуск контейнера и выводов к работе

Список файлов в каталоге work в подробном формате
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Команда: **ls -l**

.. code-block:: text

    total 28
    -rwxrwxrwx 1 root root  277 May  5 05:05 Makefile
    drwxrwxrwx 2 root root 4096 May  5 05:05 bin
    -rwxrwxrwx 1 root root  384 May  5 05:05 lab04.txt
    -rwxrwxrwx 1 root root  573 May  5 05:05 lab4.c
    -rwxrwxrwx 1 root root  122 May  5 05:05 lab4.h
    -rwxrwxrwx 1 root root   39 May  5 05:05 pr_a.c
    -rwxrwxrwx 1 root root   40 May  5 05:05 pr_b.c


Содержимое файлов исходных текстов программ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Файл **lab4.c**

.. code-block:: c

    #include <sys/types.h>
    #include <unistd.h>
    #include <stdio.h>

    #include "lab4.h"

    int main(){
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
            printf("Child My pid = %d, my ppid = %d, result a = %d, result b = %d\n",(int)pid,(int)ppid,a,b);
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


Список файлов в каталоге work/bin в подробном формате
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Переход в каталог **bin**.

Команда: **cd bin**

2. Список файлов в каталоге **bin**. Команда: **ls -l**

.. code-block:: text

    total 16
    -rwxrwxr-x 1 student student 8792 May  5 05:34 lab4
    -rwxrwxrwx 1 root    root    1019 May  5 05:05 source.tar.bz2


Очистка каталога work от вспомогательных файлов
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Возврат в каталог **work**.

Команда: **cd ..**

2. Удаление вспомогательных файлов.

Команда: **make clean**

.. code-block:: text

    rm -f lab4 lab4.o pr_a.o pr_b.o


Список файлов в каталоге work после очистки
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Команда: **ls -l**

.. code-block:: text

    total 28
    -rwxrwxrwx 1 root root  277 May  5 05:05 Makefile
    drwxrwxrwx 2 root root 4096 May  5 05:34 bin
    -rwxrwxrwx 1 root root  384 May  5 05:05 lab04.txt
    -rwxrwxrwx 1 root root  573 May  5 05:05 lab4.c
    -rwxrwxrwx 1 root root  122 May  5 05:05 lab4.h
    -rwxrwxrwx 1 root root   39 May  5 05:05 pr_a.c
    -rwxrwxrwx 1 root root   40 May  5 05:05 pr_b.c


Запуск программы
^^^^^^^^^^^^^^^^

Команда: **bin/lab4**

.. code-block:: text

    Parent My pid = 66, my ppid = 39,result a = 0,result b = 101
    Child My pid = 66, my ppid = 39, result a = 1, result b = 100
    Parent My pid = 67, my ppid = 66,result a = 0,result b = 101
    Parent My pid = 67, my ppid = 66,result a = 0,result b = 101
    Child My pid = 67, my ppid = 66, result a = 1, result b = 100
    Parent My pid = 66, my ppid = 39,result a = 0,result b = 101
    Child My pid = 67, my ppid = 66, result a = 1, result b = 100
    Child My pid = 66, my ppid = 39, result a = 1, result b = 100

