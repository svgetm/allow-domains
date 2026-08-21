# 🌐 Allow Domains

Пользовательские списки доменов и IP-подсетей для [Podkop](https://github.com/itdoginfo/podkop) и [Forkop](https://github.com/ushan0v/forkop).

В репозитории подготовлены два представления одних и тех же категорий, поскольку Podkop и Forkop по-разному принимают текстовые списки.

## 📁 Структура

```text
allow-domains/
├── podkop/
│   ├── common/
│   │   ├── domains.lst
│   │   ├── secondary.lst
│   │   └── subnets.lst
│   └── <category>/
│       ├── domains.lst
│       └── subnets.lst
└── forkop/
    ├── main.lst
    ├── secondary.lst
    └── <category>.lst
```

- В `podkop/` домены и подсети разделены по разным файлам.
- В `forkop/` домены и подсети объединены в один файл категории.

## 🧩 Podkop

Podkop обрабатывает домены и подсети как разные типы источников. Поэтому для каждой категории используются отдельные файлы:

```text
podkop/<category>/
  domains.lst
  subnets.lst
```

- `domains.lst` подключается в поле **Remote Domains Lists** / **Внешние списки доменов**.
- `subnets.lst` подключается в поле **Remote Subnets Lists** / **Внешние списки подсетей**.

Оба URL добавляются в одну секцию Podkop, если категории нужны и доменные, и сетевые правила. Пустой `subnets.lst` означает, что категория содержит только домены.

Пример URL:

```text
https://raw.githubusercontent.com/svgetm/allow-domains/refs/heads/master/podkop/<category>/domains.lst
https://raw.githubusercontent.com/svgetm/allow-domains/refs/heads/master/podkop/<category>/subnets.lst
```

Подробнее о внешних списках — в [документации Podkop](https://podkop.net/docs/sections/#vneshnie-spiski-domenov-remote-domains-lists).

## 🔀 Forkop

Forkop принимает домены и подсети совместно через поле **Domain and IP lists** / **Списки доменов и IP**. Поэтому каждая категория представлена одним файлом:

```text
forkop/<category>.lst
```

В таком файле могут находиться и домены, и IP-подсети. Forkop распознаёт тип каждой записи при обработке списка.

Пример URL:

```text
https://raw.githubusercontent.com/svgetm/allow-domains/refs/heads/master/forkop/<category>.lst
```

## 📄 Формат записей

Одна запись размещается на одной строке.

Домен указывается без протокола, порта и URL-пути:

```text
example.com
api.example.org
```

IP-подсеть указывается в CIDR-нотации:

```text
192.0.2.0/24
198.51.100.10/32
```

В объединённых списках Forkop домены и подсети для удобства могут быть разделены пустой строкой.

## ✏️ Внесение изменений

При добавлении или удалении записей необходимо обновлять оба представления категории:

1. Разнести домены и подсети по соответствующим файлам в `podkop/<category>/`.
2. Добавить все записи категории в общий файл `forkop/<category>.lst`.
3. Не добавлять протоколы, URL-пути и дубликаты.

Названия категорий, включая `common`, `main` и `secondary`, относятся только к организации списков в этом репозитории и не задают режим обработки в Podkop или Forkop.
