<img width="1219" height="821" alt="1" src="https://github.com/user-attachments/assets/08e93e64-2efb-4bce-9f6c-bc792b55335e" />
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
*(Сюда мы сейчас вставим картинки)*
<img width="1219" height="821" alt="1" src="https://github.com/user-attachments/assets/d94c94a1-c310-414a-95e6-a2284a591c7c" />
<img width="982" height="508" alt="2" src="https://github.com/user-attachments/assets/31280e2a-dae5-44f2-8e31-3b2e0195dccd" />
<img width="982" height="508" alt="3" src="https://github.com/user-attachments/assets/7127319f-7a99-4699-9bd6-673c704ea7df" />
<img width="982" height="511" alt="4" src="https://github.com/user-attachments/assets/cf86e385-1cdf-432b-9ded-4f70af9a57dc" />


