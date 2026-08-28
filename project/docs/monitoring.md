# Мониторинг и управление

## SNMPv3

| Параметр | Значение |
|----------|----------|
| Версия | v3 |
| Аутентификация | SHA |
| Шифрование | AES-128 |
| View | NMS (все OID) |

---

### Пример настройки SNMPv3

```cisco
snmp-server view NMS iso included
snmp-server group NMS v3 priv read NMS
snmp-server user nms NMS v3 auth sha AUTH_PASSWORD priv aes 128 PRIV_PASSWORD
snmp-server host 10.250.0.10 version 3 priv nms
```

---

## Syslog

| Параметр | Значение |
|----------|----------|
| Уровень | warnings |
| Источник | Loopback0 |
| Сервер | 10.250.0.11 |

---

### Пример настройки Syslog

```cisco
logging source-interface Loopback0
logging host 10.250.0.11
logging trap warnings
```

---

## NetFlow

| Параметр | Значение |
|----------|----------|
| Версия | 9 |
| Экспорт | UDP 2055 |
| Сервер | 10.250.0.12 |

---

### Пример настройки NetFlow

```cisco
flow record NETFLOW-RECORD
 match ipv4 source address
 match ipv4 destination address
 collect counter bytes long
!
flow exporter NETFLOW-EXPORTER
 destination 10.250.0.12
 transport udp 2055
 source Loopback0
!
flow monitor NETFLOW-MONITOR
 record NETFLOW-RECORD
 exporter NETFLOW-EXPORTER
```

---

### Преимущества NetFlow

- Полная видимость трафика.
- Анализ аномалий.
- Помощь в поиске неисправностей.
- База для ёмкостного планирования.
