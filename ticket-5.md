# Тикет 5: Переполнение диска

**Жалоба клиента:**
Ошибка `No space left on device`. Сервер работает нестабильно, не пишутся логи.

**Диагностика:**
1. Оценка состояния диска: `df -h` показал, что корневой раздел `/` заполнен на 100%.
2. Поиск виновника (по каталогам): с помощью `sudo du -xhd1 / | sort -h` выявлено, что больше всего места занимает каталог `/var`.
3. Детализация: `sudo du -xhd1 /var/log | sort -h` не показал аномально больших подкаталогов, что указывает на проблему с конкретным файлом.
4. Поиск тяжелых файлов: выполнена команда `sudo du -ah /var/log | sort -h | tail -n 20`. Обнаружен файл `big_mistake.log` размером 5 ГБ.

**Решение:**
Файл удален командой `sudo rm /var/log/big_mistake.log`. Повторная проверка `df -h` подтвердила освобождение дискового пространства.

**Доказательства:**

1. Диск заполнен на 100% (df -h)
<img width="970" height="494" alt="2" src="https://github.com/user-attachments/assets/c44cd8b9-f057-4e64-9395-ef603ccc72d6" />

<img width="1056" height="629" alt="1" src="https://github.com/user-attachments/assets/8e81fae4-7e28-4406-b93e-b2ed510a07a2" />

2. Поиск тяжелых файлов (найден big_mistake.log)
<img width="984" height="517" alt="3" src="https://github.com/user-attachments/assets/141abdb1-3943-4440-a7e3-a4ee6f06f2f0" />

3. Диск после очистки (df -h)
<img width="984" height="517" alt="4" src="https://github.com/user-attachments/assets/edf9b457-8cda-45eb-873f-d891738c7f36" />
