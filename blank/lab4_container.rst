.. Заменить на команду для загрузки и запуска своего контейнера

docker run --privileged -v /tmp/.X11-unix -e DISPLAY=$DISPLAY --net=host -v /home/digit/SPO/lab4:/lab4 -ti ubuntu bash
