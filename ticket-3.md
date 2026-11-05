# Тикет 3: Ошибка прав доступа (403 Forbidden)

**Жалоба клиента:**
При открытии файла `test.html` выдается ошибка 403 Forbidden. Главная страница по IP открывается нормально, Nginx работает.

**Диагностика:**
1. Фиксация ошибки: в браузере подтвержден статус `403 Forbidden`.
2. Анализ логов: 
   - `access.log`: подтвержден код ответа 403.
   - `error.log`: найдена запись `Permission denied` с указанием пути к файлу.
3. Проверка прав файла: команда `ls -l` показала права `-rw-------` (600), что означает отсутствие прав на чтение для пользователя `www-data` (от которого работает Nginx).
4. Проверка всего пути: команда `namei -l` подтвердила, что у всех директорий есть права на проход (`x`), проблема локализована именно в самом файле.

**Решение:**
Выданы права на чтение для всех пользователей: `sudo chmod 644 /var/www/html/test.html`. Файл стал доступен для чтения веб-сервером.

**Доказательства:**
1. Ошибка 403 Forbidden в браузере
<img width="981" height="513" alt="3" src="https://github.com/user-attachments/assets/e7ac65b6-e2a4-46f3-a379-2051852622b0" />

2. Лог Nginx (Permission denied)
<img width="979" height="506" alt="2" src="https://github.com/user-attachments/assets/0c099cf9-7366-4f0e-bfae-6588185aeb7c" />

3. Права на файл и весь путь (namei -l)
<img width="1218" height="408" alt="1" src="https://github.com/user-attachments/assets/a96f0e79-da90-4c02-9f37-43ce010b4ea1" />

4. Успешное открытие файла ("Hello")
<img width="1222" height="372" alt="4" src="https://github.com/user-attachments/assets/ebe30a56-5e5b-41f2-98f1-097bb96ff75b" />
