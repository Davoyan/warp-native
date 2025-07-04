![screenshot](screenshot.png)

Этот скрипт устанавливает Cloudflare WARP в "нативном" режиме через `WireGuard`, без использования `warp-cli`.

Он автоматизирует:
- Установку необходимых пакетов
- Скачивание и настройку `wgcf`
- Проверку наличия ipv6 в системе
- Генерацию и модификацию WireGuard-конфигурации
- Подключение и проверку статуса
- Включение автозапуска интерфейса `warp`

---

## Установка (производится на каждую нужную ноду):

```bash
curl -sL https://raw.githubusercontent.com/distillium/warp-native/main/install.sh | bash
```

## Шаблоны для конфигурации Xray
<details>
  <summary>📝 Показать пример outbound</summary>

```json
{
  "tag": "warp-out",
  "protocol": "freedom",
  "settings": {},
  "streamSettings": {
    "sockopt": {
      "interface": "warp"
    }
  }
}
```
</details>

<details>
  <summary>📝 Показать пример routing rule</summary>

```json
{
  "type": "field",
  "domain": [
    "netflix.com",
    "youtube.com",
    "twitter.com"
  ],
  "inboundTag": [
    "Node-1",
    "Node-2"
  ],
  "outboundTag": "warp-out"
}

```
</details>

## Доступные команды после установки:

| Операция                    | Команда                           |
| --------------------------- | --------------------------------- |
| Проверить статус интерфейса | `wg show warp`                    |
| Отключить интерфейс         | `wg-quick down warp`              |
| Включить интерфейс          | `wg-quick up warp`                |
| Перезапустить интерфейс     | `systemctl restart wg-quick@warp` |
| Отключить автозапуск        | `systemctl disable wg-quick@warp` |
| Включить автозапуск         | `systemctl enable wg-quick@warp`  |

## Удаление:
```bash
curl -sL https://raw.githubusercontent.com/distillium/warp-native/main/uninstall.sh | bash
```
