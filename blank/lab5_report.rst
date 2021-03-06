.. Процесс выполнения лабораторной. Кроме команды на запуск контейнера и выводов к работе

Список файлов в каталоге work в подробном формате
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^


.. code-block:: text

    Makefile
    bin
    lab5.txt
    lab5.c

Содержимое файлов исходных текстов программ
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Файл **lab5.c**

.. code-block:: c

    #include <unistd.h>
    #include <stdio.h>

    int main(int argc, char ** argv, char ** env){
        char ** ptr;
        printf("Main process:\n");
        printf("\tArguments:\n");
        for( ptr = argv; *ptr; ++ptr )
            printf("\t\t%s\n", *ptr);
        printf("\n");
        printf("\tEnvironment:\n");
        for( ptr = env; *ptr; ++ptr )
            printf("\t\t%s\n", *ptr);
        printf("\n");
        switch( fork() ){
            case -1:
                fprintf(stderr, "forkng error\n");
                return 1;
            case 0:
                wait();
                break;
            default:
                printf("Children process:\n");
                printf("\tArguments:\n");
                for( ptr = argv; *ptr; ++ptr )
                    printf("\t\t%s\n", *ptr);
                printf("\n");
                printf("\tEnvironment:\n");
                for( ptr = env; *ptr; ++ptr )
                    printf("\t\t%s\n", *ptr);
                printf("\n");
            break;
        }
        return 0;
    }


Файл **Makefile**

.. code-block:: text

    lab5:	lab5.o
    		gcc lab5.o -o lab5 -lm

    lab5.o:	lab5.c
    		gcc -c lab5.c

    clean:
    		rm -f lab5 lab5.o

    install:
    		cp lab5 bin/lab5

    uninstall:
    		rm -f bin/lab5


Компиляция программы и установка её в каталог bin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. Трансляция и компановка программы.

.. code-block:: text

    gcc -c lab5.c
    gcc lab5.o -o lab5 -lm


2. Установка программы в каталог **bin**.

.. code-block:: text

    cp lab5 bin/lab5


3. Удаление вспомогательных файлов.


.. code-block:: text

    rm -f lab5 lab5.o



Запуск программы
^^^^^^^^^^^^^^^^

Запуск программы с тремя аргументами: arg1, best2 и test3.

Команда: **bin/lab5 arg1 best2 test3**

.. code-block:: text

Main process:
	Arguments:
		bin/lab5
		arg1
		best2
		test3

	Environment:
		HOSTNAME=a3c8239b7321
		TERM=xterm
		OLDPWD=/
		LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.axv=01;35:*.anx=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=01;36:*.au=01;36:*.flac=01;36:*.mid=01;36:*.midi=01;36:*.mka=01;36:*.mp3=01;36:*.mpc=01;36:*.ogg=01;36:*.ra=01;36:*.wav=01;36:*.axa=01;36:*.oga=01;36:*.spx=01;36:*.xspf=01;36:
		PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
		PWD=/home/lab5/work
		HOME=/root
		SHLVL=2
		LESSOPEN=||/usr/bin/lesspipe.sh %s
		container=docker
		_=bin/lab5

Children process:
	Arguments:
		bin/lab5
		arg1
		best2
		test3

	Environment:
		HOSTNAME=a3c8239b7321
		TERM=xterm
		OLDPWD=/
		LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=01;05;37;41:su=37;41:sg=30;43:ca=30;41:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.axv=01;35:*.anx=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=01;36:*.au=01;36:*.flac=01;36:*.mid=01;36:*.midi=01;36:*.mka=01;36:*.mp3=01;36:*.mpc=01;36:*.ogg=01;36:*.ra=01;36:*.wav=01;36:*.axa=01;36:*.oga=01;36:*.spx=01;36:*.xspf=01;36:
		PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
		PWD=/home/lab5/work
		HOME=/root
		SHLVL=2
		LESSOPEN=||/usr/bin/lesspipe.sh %s
		container=docker
		_=bin/lab5



В результате переданные при запуске программы аргументы обнаружены и выведены на экран.
