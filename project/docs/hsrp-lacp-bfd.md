# HSRP, LACP и BFD — резервирование

## HSRP (Hot Standby Router Protocol)

| Параметр | Значение |
|----------|----------|
| Версия | v2 |
| VIP | .1 |
| R1 priority | 115 |
| R2 priority | 100 |
| Preempt | включён (задержка 60 сек) |

---

### Пример настройки HSRP (DC1-R1)

```cisco
interface Vlan20
 description USERS
 vrf forwarding CORP-MPLS
 ip address 10.1.20.2 255.255.254.0
 standby version 2
 standby 20 ip 10.1.20.1
 standby 20 priority 115
 standby 20 preempt delay minimum 60
```

---

## LACP (Link Aggregation Control Protocol)

| Параметр | Значение |
|----------|----------|
| Режим | active |
| Port-channel (Core) | 10 |
| Port-channel (Access) | 1 |

---

### Пример настройки LACP (Core)

```cisco
interface Port-channel10
 description DC1_CORE_MLAG
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50,60,999
 no shutdown
!
interface TenGigabitEthernet1/0/47
 channel-group 10 mode active
 no shutdown
```

---

## BFD (Bidirectional Forwarding Detection)

| Параметр | Значение |
|----------|----------|
| Интервал | 50 мс |
| Множитель | 3 |
| Обнаружение отказа | < 150 мс |

---

### Применение BFD

- EIGRP
- BGP
- Статические маршруты (при необходимости)

---

### Пример настройки BFD

```cisco
interface TenGigabitEthernet1/0/1
 bfd interval 50 min_rx 50 multiplier 3
```

---

### Преимущества BFD

- Мгновенное переключение.
- Независимость от протоколов верхнего уровня.
- Не создаёт лишней нагрузки.
