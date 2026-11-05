# Тикет 4: Отказ DNS

**Жалоба клиента:**
На сервере перестали открываться внешние сайты по доменным именам. При обращении к IP-адресам (например, `8.8.8.8`) подключение работает, локальные сервисы работают.

**Диагностика:**
1. Проверка локализации проблемы: `ping 8.8.8.8` работает (сеть есть), `ping google.com` выдает ошибку (сломан DNS).
2. Проверка файрвола: `sudo ufw status` -> `inactive`. Локальный фаервол не блокирует трафик.
3. Анализ конфигурации: `cat /etc/resolv.conf` показал несуществующий DNS-сервер `nameserver 192.0.2.1` (тестовый IP).
4. Проверка доступности DNS: `ping 192.0.2.1` -> нет ответа. `nslookup google.com 192.0.2.1` -> нет ответа. Подтверждено, что сервер не отвечает.

**Решение:**
Замена нерабочего DNS на публичный сервер Google через текстовый редактор nano. Команда: `sudo nano /etc/resolv.conf`.
В файл записано: `nameserver 8.8.8.8`. Проверка: `ping google.com` работает.

**Доказательства:**

1. Сеть работает по IP, но не работает по домену
<img width="964" height="500" alt="1" src="https://github.com/user-attachments/assets/116859fa-0b02-4299-8aac-2781d54c169b" />


2. Конфигурация resolv.conf (нерабочий DNS)
<img width="979" height="504" alt="2" src="https://github.com/user-attachments/assets/0b9c3bf4-1c4e-4de7-8abc-5403df2f4959" />


3. Проверка DNS-сервера (нет ответа)
<img width="979" height="509" alt="3" src="https://github.com/user-attachments/assets/8798e207-d12f-4ade-9a93-e77e41d326dd" />


4. Редактирование через nano и успешный пинг
<img width="979" height="509" alt="4" src="https://github.com/user-attachments/assets/7ed8a465-1af9-411b-b225-6d7965ec43ba" />
