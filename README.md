Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose»
Задание 1
https://hub.docker.com/r/krvfilimonova/custom-nginx/tags

Задание 2
<img width="1539" height="718" alt="image" src="https://github.com/user-attachments/assets/e8325754-aad0-45f8-8d71-93dc89803d31" />

Задание 3
<img width="1426" height="554" alt="image" src="https://github.com/user-attachments/assets/d81bdf96-7492-4eac-8c05-0d360904b72a" />
Контейнер остановился, потому что docker attach подключился к главному процессу контейнера (nginx, PID 1). Когда я нажала Ctrl-C, в терминал был отправлен сигнал SIGINT, который получил основной процесс. Nginx завершил работу, а поскольку в контейнере не осталось работающих процессов, Docker автоматически остановил контейнер.

<img width="1285" height="802" alt="image" src="https://github.com/user-attachments/assets/fa91b833-0dac-4bf5-93fe-f2006f8fb9dc" />
<img width="1003" height="177" alt="image" src="https://github.com/user-attachments/assets/41ba6fe3-0e44-4a41-be4e-20f9ccb7d827" />
<img width="888" height="282" alt="image" src="https://github.com/user-attachments/assets/fb29f407-e5f3-40a2-a5c2-f3eabbe92bd6" />
<img width="669" height="181" alt="image" src="https://github.com/user-attachments/assets/af2c5b7b-7d11-41e8-8fc5-0a423c16f131" />

Я изменила конфигурацию nginx внутри контейнера, чтобы он слушал порт 81 вместо 80. Однако проброс портов Docker остался неизменным: хост-порт 8080 по-прежнему перенаправляет трафик на порт 80 внутри контейнера. Поскольку nginx больше не слушает порт 80, запросы от curl http://127.0.0.1:8080 не обрабатываются и соединение отклоняется.  
<img width="763" height="89" alt="image" src="https://github.com/user-attachments/assets/da3e7906-f3cd-4244-a6d5-66a4df35b692" />

Задание 4
<img width="1344" height="793" alt="image" src="https://github.com/user-attachments/assets/f918a7e8-a20b-467f-887e-cd19b9396c42" />
<img width="789" height="310" alt="image" src="https://github.com/user-attachments/assets/6a8db832-c122-4aff-bb73-dd052230230c" />


Задание 5

<img width="889" height="798" alt="image" src="https://github.com/user-attachments/assets/63310ef3-53cf-469a-9b8d-ebe279297da5" />
<img width="1532" height="155" alt="image" src="https://github.com/user-attachments/assets/a6c6d9d1-2d12-46fe-a03e-5299c4226d5d" />
<img width="1232" height="73" alt="image" src="https://github.com/user-attachments/assets/050977f3-5ada-47c3-9bf8-ea5ea9e62e09" />
При наличии обоих файлов в одной директории, Docker Compose использует compose.yaml (наивысший приоритет).

Редактируем файл compose.yaml

<img width="511" height="247" alt="image" src="https://github.com/user-attachments/assets/ee7ec1a8-817b-448c-81e6-04a6d04bfe8c" />
<img width="1521" height="549" alt="image" src="https://github.com/user-attachments/assets/b0526f12-d1fa-45c1-9ae9-fc5ca8cb7861" />
<img width="1542" height="710" alt="image" src="https://github.com/user-attachments/assets/ffc56b54-7177-4324-99bb-b53f66fc85aa" />
<img width="606" height="819" alt="image" src="https://github.com/user-attachments/assets/24d53bf1-4543-489f-8e9d-06ff860f668c" />
<img width="944" height="615" alt="image" src="https://github.com/user-attachments/assets/8103b460-ac73-47d0-a893-e37154294856" />
<img width="1533" height="301" alt="image" src="https://github.com/user-attachments/assets/1f92f489-3c04-44d4-b2a1-e76f4ade7dd9" />
Docker Compose обнаружил несколько файлов с поддерживаемыми именами в директории. Т. к. compose.yaml был удалён, теперь используется docker-compose.yaml (следующий по приоритету).  

ИСПРАВЛЕНИЯ:
Предупреждение об orphan-контейнере появляется, когда в проекте остаётся запущенный контейнер, который больше не описан в файлах docker-compose.yaml или compose.yaml. В моём случае: после удаления compose.yaml, контейнер portainer остался работать, но исчез из конфигурации проекта. Docker Compose обнаружил этот "осиротевший" контейнер и предложил использовать флаг --remove-orphans для его удаления.


