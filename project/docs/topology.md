# 📊 Топология сети

## Устройства и роли

| Устройство | Роль | Описание |
|------------|------|----------|
| DC1-R1, DC1-R2 | Core (ЦОД-1) | Ядро ЦОД-1, CE для MPLS |
| DC2-R1, DC2-R2 | Core (ЦОД-2) | Ядро ЦОД-2, CE для MPLS |
| MSK-R1, MSK-R2 | Core (МСК) | Ядро филиала МСК |
| SPB-R1, SPB-R2 | Core (СПБ) | Ядро филиала СПБ |
| DC1-ACC | Access (ЦОД-1) | Доступ серверов ЦОД-1 |
| DC2-ACC | Access (ЦОД-2) | Доступ серверов ЦОД-2 |
| MSK-ACC1, MSK-ACC2 | Access (МСК) | Доступ пользователей МСК |
| SPB-ACC1, SPB-ACC2 | Access (СПБ) | Доступ пользователей СПБ |

---

## Связи внутри ЦОД-1

| Откуда | Куда | Интерфейсы | Подсеть | Назначение |
|--------|------|------------|---------|------------|
| DC1-R1 | DC1-R2 | 10Gig1/0/1 ↔ 10Gig1/0/1 | 10.254.1.0/31 | Core ↔ Core |
| DC1-R1 | DC1-ACC | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |
| DC1-R2 | DC1-ACC | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |

---

## Связи внутри ЦОД-2

| Откуда | Куда | Интерфейсы | Подсеть | Назначение |
|--------|------|------------|---------|------------|
| DC2-R1 | DC2-R2 | 10Gig1/0/1 ↔ 10Gig1/0/1 | 10.254.2.0/31 | Core ↔ Core |
| DC2-R1 | DC2-ACC | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |
| DC2-R2 | DC2-ACC | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |

---

## Связи между ЦОД (тёмная оптика)

| Откуда | Куда | Интерфейсы | Подсеть | Назначение |
|--------|------|------------|---------|------------|
| DC1-R1 | DC2-R1 | 10Gig1/0/2 ↔ 10Gig1/0/2 | 10.254.100.0/31 | Тёмная оптика |
| DC1-R2 | DC2-R2 | 10Gig1/0/2 ↔ 10Gig1/0/2 | 10.254.100.2/31 | Тёмная оптика |

---

## Связи MPLS L3VPN (CE → PE)

| Откуда | Куда | Подсеть | Назначение |
|--------|------|---------|------------|
| MSK-R1 | PE1 | 172.31.10.0/31 | MPLS WAN |
| MSK-R1 | PE2 | 172.31.10.2/31 | MPLS WAN |
| MSK-R2 | PE1 | 172.31.10.4/31 | MPLS WAN |
| MSK-R2 | PE2 | 172.31.10.6/31 | MPLS WAN |
| SPB-R1 | PE1 | 172.31.20.0/31 | MPLS WAN |
| SPB-R1 | PE2 | 172.31.20.2/31 | MPLS WAN |
| SPB-R2 | PE1 | 172.31.20.4/31 | MPLS WAN |
| SPB-R2 | PE2 | 172.31.20.6/31 | MPLS WAN |

---

## Связи внутри МСК

| Откуда | Куда | Интерфейсы | Подсеть | Назначение |
|--------|------|------------|---------|------------|
| MSK-R1 | MSK-R2 | Port-channel10 ↔ Port-channel10 | Trunk | Core ↔ Core |
| MSK-R1 | MSK-ACC1 | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |
| MSK-R2 | MSK-ACC2 | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |

---

## Связи внутри СПБ

| Откуда | Куда | Интерфейсы | Подсеть | Назначение |
|--------|------|------------|---------|------------|
| SPB-R1 | SPB-R2 | Port-channel10 ↔ Port-channel10 | Trunk | Core ↔ Core |
| SPB-R1 | SPB-ACC1 | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |
| SPB-R2 | SPB-ACC2 | Port-channel10 ↔ Port-channel1 | Trunk | Core → Access |

---

## Схема (текстовое описание)
[ MPLS L3VPN (AS 64500) ]
/
/
[ PE1 ] [ PE2 ]
/ | \ / |
/ | \ / |
[MSK-R1] [SPB-R1] [MSK-R2] [SPB-R2]
| | | |
[MSK-ACC1] [SPB-ACC1] [MSK-ACC2] [SPB-ACC2]

┌───────────────────────┐
│ Тёмная оптика │
│ 10.254.100.0/31 │
│ 10.254.100.2/31 │
└──────────┬────────────┘
│
┌──────────▼────────────┐
│ ЦОД-1 / ЦОД-2 │
│ DC1-R1 ↔ DC2-R1 │
│ DC1-R2 ↔ DC2-R2 │
└────────────────────────┘

text
