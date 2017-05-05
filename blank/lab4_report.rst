.. Процесс выполнения лабораторной. Кроме команды на запуск контейнера и выводов к работе

Список файлов в каталоге work в подробном формате.

Содержимое файлов исходных текстов программ.


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


Компиляция программы и установка её в каталог bin каталога work.

Список файлов в каталоге work/bin в подробном формате.

Очистка каталога work от вспомогательных файлов.

Список файлов в каталоге work после очистки.

Запуск программы.