.. Процесс выполнения лабораторной. Кроме команды на запуск контейнера и выводов к работе

Список файлов в каталоге work в подробном формате.

Содержимое файлов исходных текстов программ.

.. program:: rm

.. option:: #include <sys/types.h>
.. option:: #include <unistd.h>
.. option:: #include <stdio.h>
.. option:: #include "lab4.h"

.. option:: int main(){
.. option::     pid_t pid, ppid;
.. option::     int a =  0; 
.. option::     int b =  100; 
.. option::     (void)fork();
.. option::     pid = getpid();
.. option::     ppid = getppid();

.. option::     if(fork() == -1){
.. option::         printf("error");
.. option::     } else if (fork() == 0){
.. option::         a = DO_A(a);   
.. option::       printf("Child My pid = %d, my ppid = %d, result a = %d, result b = %d\n",(int)pid,(int)ppid,a,b);
.. option::     } else {
.. option::       b = DO_B(b);
.. option::       printf("Parent My pid = %d, my ppid = %d,result a = %d,result b = %d\n",(int)pid,(int)ppid,a,b);
.. option::     }
.. option::     return 0;
.. option:: }


Компиляция программы и установка её в каталог bin каталога work.

Список файлов в каталоге work/bin в подробном формате.

Очистка каталога work от вспомогательных файлов.

Список файлов в каталоге work после очистки.

Запуск программы.