# wp_taxi_server
Плагин Wordpress сервер такси на сайте wordpress .


Полная система управления такси-диспетчерской. Без ограничений на количество машин, водителей, диспетчеров и телефонных линий.

Версия 2.0.5 | Автор: Такси
🌐 REST API — базовый URL
https://gorod24.by/wp-json/taksi-server/v1

📎 Шорткоды

Шорткод	Описание	Как использовать

[taksi_order_form]	Форма заказа такси для клиентов	Добавьте на любую страницу сайта, доступную клиентам

[taksi_driver_app]	Приложение водителя (вход + заказы + статус)	Создайте страницу для водителей (можно скрыть из меню)

[taksi_driver_register]	Форма самостоятельной регистрации водителя	Добавьте на страницу «Стать водителем»

📡 API — Водитель
Токен водителя = md5(позывной + "taksi-server")

Метод	URL	Параметры
GET	/driver/orders?callsign=001&token=xxx	Получить активные заказы
POST	/driver/order/accept	callsign, token, order_id
POST	/driver/order/arrived	callsign, token, order_id
POST	/driver/order/complete	callsign, token, order_id
POST	/driver/order/cancel	callsign, token, order_id
POST	/driver/status	callsign, token, status (free/busy/offline)
POST	/driver/location	callsign, token, lat, lng
POST	/driver/register	name, callsign, phone, license, telegram_chat_id
📡 API — Клиент
Метод	URL	Параметры
POST	/client/order	phone, name, address_from, address_to, waypoints[], notes, tg_id
GET	/client/order/{id}?phone=xxx	Статус заказа
📍 Telegram — геопозиция водителей (webhook)
Когда водитель отправляет геопозицию боту (вручную или Live Location), координаты автоматически обновляются на карте диспетчера.

Webhook URL	
https://gorod24.by/wp-json/taksi-server/v1/telegram/location
Скопировать
Активировать webhook	⚠️ Сначала укажите токен бота водителей в Настройках.
Инструкция для водителя	
Открыть чат с ботом водителей в Telegram
Нажать скрепку (📎) → Геопозиция
Выбрать Транслировать геопозицию для Live Location (обновляется автоматически)
или Отправить текущую геопозицию разово
🖥 TCP-сервер для таксофонов (Такси Мастер)
Порт: 4000

Для запуска TCP-сервера (совместимость с таксофонами):

php /hosting1/soligorskgor/public_html/wp-content/plugins/taksi-server/taxophone-server.php
Автозапуск через crontab:

@reboot php /hosting1/soligorskgor/public_html/wp-content/plugins/taksi-server/taxophone-server.php >> /tmp/ts-tcp.log 2>&1 &
Спасибо вам за творчество с WordPress.Версия 7.0
