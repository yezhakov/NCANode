
![NCANode](NCANode.png)


⭐ Приложение-сервер для работы с Электронно Цифровой Подписью (ЭЦП) РК

---

![License:MIT](https://img.shields.io/badge/license-MIT-green.svg)
![Downloads](https://img.shields.io/github/downloads/malikzh/NCANode/total.svg)
![Docker Pulls](https://img.shields.io/docker/pulls/malikzh/ncanode)
[![Build CI and Test](https://github.com/malikzh/NCANode/actions/workflows/build-ci.yml/badge.svg)](https://github.com/malikzh/NCANode/actions/workflows/build-ci.yml)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/malikzh/NCANode)
[![codecov](https://codecov.io/gh/malikzh/NCANode/branch/master/graph/badge.svg?token=yk6ln3mlTB)](https://codecov.io/gh/malikzh/NCANode)

---

## Возможности

- Кроссплатформенный сервер (Windows, Mac OS, Linux)
- Работа с API посредством JSON
- Подпись XML данных с помощью xmldsig
- Подпись Wsse для [SmartBridge](https://sb.egov.kz/)
- Поддержка OCSP и CRL
- Проверка валидности сертификатов (включая цепочку доверия)
- Поддержка работы с CMS ( [Cryptographic Message Syntax](https://en.wikipedia.org/wiki/Cryptographic_Message_Syntax) )
- Поддержка TSP-меток в CMS
- Поддержка множественных подписей для xmldsig и CMS
- Возможность добавления подписей уже в существующие файлы CMS и XML
- Поддержка новых ЭЦП (ГОСТ 2015) и новых CRL
- Добавлены тесты на весь функционал
- Docker

## Кому надо?

Если Вам необходимо реализовать подпись данных будь формата XML или любом другом произвольном формате, при этом на стороне сервера,
Вы можете запустить NCANode на сервере и обращаться к нему посредством API (Http/RabbitMQ).

## Кто использует?

Исходя из полученных писем от программистов, NCANode используется как в стартапах, так и в крупных страховых компаниях

## СМИ об NCANode

https://profit.kz/news/56732/Otkritij-kod-Beeline-Hacktoberfest-v-Kazahstane/

## Пример

Пример запроса (запрос информации о ключе):

```json
{
  "xml": "<?xml version=\"1.0\" encoding=\"utf-8\"?><a><b>test</b></a>",
  "signers": [
    {
      "key": "MIIHTwIBAzCCBwkGCSqGS...",
      "password": "qwerty12"
    }
  ]
}
```

Пример ответа:

```json
{
  "status": 200,
  "message": "OK",
  "xml": "<?xml version=\"1.0\" encoding=\"utf-8\" standalone=\"no\"?><a><b>test</b><ds:Signature x..."
}
```

## Документация

Документацию можно найти на http://ncanode.kz

## Contributors

<a href="https://github.com/malikzh/NCANode/graphs/contributors">
  <img src="https://contributors-img.web.app/image?repo=malikzh/NCANode" />
</a>

## Лицензия

Проект лицензирован под лицензией [MIT](LICENSE)

## Важно!!!

По требованию  АО «НИТ» | НУЦ РК. Библиотеки `kalkancrypt-0.6.jar` и `kalkancrypt_xmldsig-0.3.jar`
Были удалены из репозитория, поэтому для компиляции Вам необходимо подставить библиотеки
из комплекта разработчика (SDK) в директорию `/lib`.

### Сборка проекта

Для сборки проекта необходимо:

1. Подставить бибилиотеки kalkancrypt (Их можно запросить [тут](https://pki.gov.kz/developers/))
2. `./gradlew bootJar` (для jar файла) или `./gradlew bootWar` (для jar файла)


Собранный проект будет лежать: `build/libs/NCANode.jar` или `build/libs/NCANode.war`

### Запуск в Docker

```bash
docker volume create ncanode_cache
docker run -p 14579:14579 -v ncanode_cache:/app/cache -d malikzh/ncanode
```

### Запуск проекта без сборки

Проект запустить можно командой:

```bash
$ ./gradlew bootRun
```

### После запуска

Проверить можно, перейдя на страницу: http://localhost:14579/actuator/health

Сделано с ❤️
