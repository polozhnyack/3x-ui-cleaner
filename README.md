# 3x-ui-cleaner

**X-ui-cleaner** — сервис для очистки базы данных **3x-ui** от забаганных пользователей, возникающих при ошибках типа `record not found` и других.

## Установка

Развертывание происходит одной командой:

```bash
curl -fsSL https://raw.githubusercontent.com/polozhnyack/X-ui-cleaner/main/deploy.sh | bash
```

Сервис развертывается на **порту 8000**.

## Пример запроса

```python
import requests

resp = requests.delete(
    "http://{you_ip_server}:8000/deleteclient",
    headers={"Content-Type": "application/json", "X-API-Key": "You_WebPath"},
    json={"identifier": "user@example.com"},
    timeout=5
)
print(resp.status_code, resp.json())
```
* `identifier` — email пользователя или его UUID.
* `X-API-Key` — значение `webBasePath` самой панели.


Пример ответа

```json
{
    "status": "ok",
    "uuid": "123e4567-e89b-12d3-a456-426614174000",
    "email": "user@example.com",
    "inbounds_deleted": 2,
    "tables_deleted": ["inbounds"]
}
```

* `status` — `"ok"` если удаление прошло успешно.
* `uuid` — UUID пользователя.
* `email` — email пользователя.
* `inbounds_deleted` — количество удалённых inbound-записей.
* `tables_deleted` — список таблиц, где данные пользователя были удалены.


