# People are always asking me if I know Tyler Nginx
## Что нужно сделать в этом задании: 
* ~~Зайти в коворкинг и затеять драку с незнакомым программистом, да так, чтобы вас в ней одолели~~
## Настроить nginx по заданному тз. Нужно чтобы:
* Подключение осуществлялось через протокол https с сертификатом;
* Было настроено принудительное перенаправление HTTP-запросов (порт 80) на HTTPS (порт 443) для обеспечения безопасного соединения;
* Использовался alias для создания псевдонимов путей к файлам или каталогам на сервере;
* Имелись настроенные виртуальные хосты для обслуживания нескольких доменных имен на одном сервере.
# Подготовка
## Сдуваем пыль с виртуальной коробки, на которой стоит Ubuntu, вспоминаем пароль
![image](https://github.com/user-attachments/assets/b2f05e3f-0f9a-42dd-9978-9b8921b610b1)
## Устанавливаем nginx
## Сначала он упирался из-за ведомых только ему unattended processes, ~~ну и чем линукс тогда отличается от винды~~
![image](https://github.com/user-attachments/assets/812c77bc-e9d9-47c8-a2b8-195048ebcd0b)
## готово
![image](https://github.com/user-attachments/assets/a69cd163-4b57-41b5-a941-d7594907192b)
## Оно живое и откликается на localhost
![image](https://github.com/user-attachments/assets/7805a982-a92f-4e7c-afeb-4303336b554b)
# Готовим проекты ~~"Разгром"~~
## Создаем директории proj1 и proj2 в /var/www/
![image](https://github.com/user-attachments/assets/7eb26c16-da9e-4275-903f-573e9211dfe9)
## Не для того ИИ придумывали, чтобы я руками html теги писал
![image](https://github.com/user-attachments/assets/e908ac63-bde9-4916-80fe-2d5e8d9073f9)
## Добавляем index.html файлы в директории
![image](https://github.com/user-attachments/assets/b373ef62-7a63-451e-b6b2-ff325227e96b)
![image](https://github.com/user-attachments/assets/4eb05f03-ca4c-4382-ac69-0065f665040c)
## Далее заходим в /etc/hosts и присваиваем доменам IP-адрес локального хоста, чтобы мы могли затестить
![image](https://github.com/user-attachments/assets/782f8611-c7ba-41d2-8052-964cb5997e6d)
![image](https://github.com/user-attachments/assets/a89ada90-cb92-44f9-8545-fd3b374cbdf5)
# SSL
Чтобы мы могли использовать HTTPS, нам нужны сертификаты SSL. Мы сделаем самоподписанные сертификаты сроком на 365 дней c помощью OpenSSL
## Устанавливаем OpenSSL
![image](https://github.com/user-attachments/assets/5ad84238-0b84-43e0-bda5-9829d0fa2303)
## Вводим команды для создания сертификата  
```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/proj2.key \
  -out /etc/ssl/certs/proj2.crt
```
### Параметры у команды означают: самоподписанный сертификат, нешифрованный ключ, срок действия, создание RSA-ключа длиной 2048 бит и куда сертификат, и куда ключ
И аналогичную команду для второго проекта
![image](https://github.com/user-attachments/assets/7bbc6f95-15e3-4d5b-8c4a-612ef9ecbad5)
## Спрашивал меня мои данные, но я не до конца сознался
![image](https://github.com/user-attachments/assets/8bba8b13-b7f5-4fce-8f26-f4e973f1f92d)
# Конфигурационные файлы
## Создаем их в директории /etc/nginx/sites-available
![image](https://github.com/user-attachments/assets/4c78f74e-747c-430c-9532-6ee69c0bf1fb)
### В файликах я сначала потерял точку с запятой, потом закрывающую скобку, потом забыл, потом что надо перезагрузить, потом что нужно return 301 прописать и думал почему же не перекидывает на https, еще перепутал, где находятся сертификат и ключ и думал, почему не работает. Вот скриншотики моих ошибочек
![image](https://github.com/user-attachments/assets/f5cb49ee-609b-440e-8193-a36f8c540d36)
![image](https://github.com/user-attachments/assets/3d6f426e-b178-4b50-be7d-f87f3204282e)
![image](https://github.com/user-attachments/assets/53dd5c36-b39e-4ba8-82b3-e93e81311d54)
![image](https://github.com/user-attachments/assets/ae91216c-203a-4f9a-b397-5a3c0b068604)

## Нужно было еще добавить ссылки на файлы конфигурации в sites-enabled, что сделано сверху. Работоспособность проверял с помощью nginx -t. 
## По итогу довел до рабочего состояния файлики:
![image](https://github.com/user-attachments/assets/a9bba1c2-4180-42d8-90c0-9771971e88f3)
### Аналогично выглядит второй.
## Когда пишем http, перекидывает на https. Условие выполнено. Но пишет об опасности сайта, так как сертификат самоподписанный
![image](https://github.com/user-attachments/assets/51e09e4c-ed73-4143-a12f-d36f279daf23)
![image](https://github.com/user-attachments/assets/3500aec6-71fa-464e-bcfb-fb3edb2488a4)
## И второй
![image](https://github.com/user-attachments/assets/9bfe9ba2-6a27-4709-8411-ec70fdbca664)
# Настроим alias
Alias нужен для создания пседовнимов для глубоко лежащих файликов в иерархии папок. Поэтому создадим пару папок first_rule, second_rule и туда уже закинем туда html файлик, зададим ему псевдоним rule
![image](https://github.com/user-attachments/assets/0aa9d670-485d-4d4e-99bd-bcf0b203ab61)
## Теперь можно ввести /rule вместо first_rule/second_rule
![image](https://github.com/user-attachments/assets/4b63a142-eb68-4e83-98c0-7cd98db603e5)
# Итого поставленные задачи были выполнены. Писать отчет is a quite an exhausting activity
![image](https://github.com/user-attachments/assets/46956245-b8fd-487a-86ed-66fcf738aa7e)




