# Тикет 1: Сайт недоступен 

**Жалоба клиента:**
Браузер выдает ERR_CONNECTION_REFUSED при заходе на IP сервера. Вчера всё работало.

**Диагностика:**
1. Так как SSH-доступ работает, проблема локальная (сервер жив).
2. Проверил файрвол: `sudo ufw status` (статус: `inactive`).
3. Проверил логи веб-сервера: `sudo journalctl -u nginx --no-pager | tail -n 10`. В логах обнаружена запись `Stopped A high performance web server...`.
4. Проверил статус: `systemctl status nginx` (статус: `inactive (dead)`).

**Решение:**
Запуск службы командой `sudo systemctl start nginx`. Сайт восстановил работоспособность.

**Доказательства:**
1. Ошибка в браузере (сайт недоступен)
<img width="1219" height="821" alt="1" src="https://github.com/user-attachments/assets/d94c94a1-c310-414a-95e6-a2284a591c7c" />

2. Логи Nginx: служба остановлена
<img width="982" height="508" alt="2" src="https://github.com/user-attachments/assets/31280e2a-dae5-44f2-8e31-3b2e0195dccd" />

3. Статус Nginx до починки (inactive/dead)
<img width="982" height="508" alt="3" src="https://github.com/user-attachments/assets/7127319f-7a99-4699-9bd6-673c704ea7df" />

4. Статус Nginx после починки (active/running)
<img width="982" height="511" alt="4" src="https://github.com/user-attachments/assets/cf86e385-1cdf-432b-9ded-4f70af9a57dc" />


