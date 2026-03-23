# Domain & Network Lists

Репозиторий содержит списки доменов и IP-подсетей для маршрутизации трафика.

## 📁 Структура

Каждый сервис расположен в отдельной директории:

```
adobe/
  domains.lst
  subnets.lst

common/
  domains.lst
  subnets.lst

kinopub/
  domains.lst
  subnets.lst

telegram/
  domains.lst
  subnets.lst
```

* `domains.lst` — список доменов сервиса
* `subnets.lst` — список IP-подсетей (CIDR), относящихся к сервису

---

## 📄 Формат файлов

Все файлы имеют формат `.lst` — **одна запись на строку**.

### Домены (`domains.lst`)

```
example.com
google.com
domain.org
```

✔ Без `http://` или `https://`
✔ Без путей (`/path`)
✔ Только доменное имя

**Важно:** при добавлении домена автоматически покрываются **все его поддомены**
Пример:

* `example.com` → включает `www.example.com`, `api.example.com`, и т.д.

---

### Подсети (`subnets.lst`)

```
192.168.1.0/24
10.0.0.0/8
172.16.0.0/12
```

✔ Только CIDR-нотация
✔ IPv4

