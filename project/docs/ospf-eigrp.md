# OSPF / EIGRP — внутренняя маршрутизация

## Используется EIGRP

| Параметр | Значение |
|----------|----------|
| AS | 100 |
| BFD | включён |
| Пассивные интерфейсы | все, кроме P2P-линков |

---

### Особенности EIGRP

- **EIGRP** выбран вместо OSPF для упрощения настройки и быстрой сходимости.
- **BFD** обеспечивает обнаружение отказа каналов за < 50 мс.
- **Суммаризация маршрутов** не используется — все маршруты анонсируются точечно.
- **Passive-interface default** отключает отправку hello-пакетов на всех интерфейсах, кроме явно разрешённых.

---

### Пример настройки EIGRP (DC1-R1)

```cisco
router eigrp EIGRP-CORE
 address-family ipv4 autonomous-system 100
  network 10.254.0.0 0.0.255.255
  network 10.255.1.1 0.0.0.0
  passive-interface default
  no passive-interface TenGigabitEthernet1/0/1
  no passive-interface TenGigabitEthernet1/0/2
  bfd all-interfaces
 exit-address-family
```

---

## Почему EIGRP, а не OSPF?

- Проще настройка и меньше команд.
- Меньше служебного трафика (overhead).
- Быстрая сходимость.
- Поддержка BFD из коробки.
- Хорошо работает в частных сетях без сложной иерархии.

---

## Альтернатива — OSPF (если бы использовался)

- **Area 0** — все Core-роутеры.
- **Network type point-to-point** — на всех P2P-линках.
- **BFD** — аналогично.
