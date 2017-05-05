.. Процесс выполнения лабораторной. Кроме команды на запуск контейнера и выводов к работе

Список файлов в каталоге work в подробном формате.
--------------------------------------------------

Содержимое файлов исходных текстов программ.
--------------------------------------------


.. topic:: lab4.c

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


.. topic:: lab4.h

    #ifndef DO_A
    
    #define DO_A(X) pr_a(X);
    
    #endif /*DO_A*/
    
    #ifndef DO_B
    
    #define DO_B(X) pr_b(X);
    
    #endif /*DO_B*/


.. topic:: pr_a.c

    int pr_a( int x ){
    
        return x + 1;
        
    }


.. topic:: pr_b.c

    int pr_b( int x ){
    
        return x + 1 ;
        
    }


.. topic:: Makefile

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


Компиляция программы и установка её в каталог bin каталога work.

Список файлов в каталоге work/bin в подробном формате.

Очистка каталога work от вспомогательных файлов.

Список файлов в каталоге work после очистки.

Запуск программы.