# это лаба 2 со звездочкой йоу
![image](https://github.com/user-attachments/assets/bb283f0a-43fc-4fef-a3fe-3f85159549d5)
## Что надо:
* Написать “плохой” Docker compose файл, в котором есть не менее трех “bad practices” по их написанию
* Написать “хороший” Docker compose файл, в котором эти плохие практики исправлены
* В Readme описать каждую из плохих практик в плохом файле, почему она плохая и как в хорошем она была исправлена, как исправление повлияло на результат
* После предыдущих пунктов в хорошем файле настроить сервисы так, чтобы контейнеры в рамках этого compose-проекта так же поднимались вместе, но не "видели" друг друга по сети. В отчете описать, как этого добились и кратко объяснить принцип такой изоляции
# Подготовка
### Была какая-то фигня с установкой docker-compose, потому что я сначала написал sudo apt-get install docker-compose и очень долго там что-то устанавливалось, пока я отошел. Потом пришел, а там все еще не установилось - писало странные вещи в консоли, не помню что, скрин не сделал.
![image](https://github.com/user-attachments/assets/8c5173cc-c6e6-4bff-abfb-8171154948e6)
### Почитал документацию, сделал только apt-get-update
### Потом ввел вот так вот, пишет же, что не может найти, но при этом docker-compose работает
![image](https://github.com/user-attachments/assets/409d8016-c613-4d96-918f-ef7edc176a3b)
### работает - не трогай
# Делаем докерфайлы
### плохой
![image](https://github.com/user-attachments/assets/02c3e461-59b8-4600-b528-53ca338c354d)
![image](https://github.com/user-attachments/assets/e14e6ac4-387d-4a1b-9d21-2de7368fafcd)
![image](https://github.com/user-attachments/assets/32632123-517c-4d47-bf83-a912b1bf3cd3)
### хороший
![image](https://github.com/user-attachments/assets/4f627e27-93f9-4eca-841a-8babfd7f89cd)
![image](https://github.com/user-attachments/assets/f0413e3b-ee9f-489c-9500-29b3ff958549)

