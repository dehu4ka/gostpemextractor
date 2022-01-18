# Gost PEM Extractor

Основано на [Privkey2012](https://github.com/iliadmitriev/privkey2012)

## Требования для работы

При экспорте из ViPNet CSP достаточно PFX с включенным в него приватным ключом.

При экспорте из КриптоПро CSP нужен PFX (не обязательно с ключом) и ключ (хранилище).

Хранилище это директория с файлами:
```
header.key
masks.key
masks2.key
name.key
primary.key
primary2.key
```

### Для экспорта из ViPNet CSP:
1. В окне «ViPNet CSP» в разделе «Контейнеры ключей» выберите контейнер ключей, содержащий сертификат или сертификат и закрытый ключ, которые вы хотите экспортировать. Нажмите кнопку «Свойства» либо дважды щелкните нужный контейнер ключей.
2. В окне «Свойства контейнера ключей» нажмите кнопку «Открыть».
3. В окне «Сертификат» перейдите на вкладку «Состав» и нажмите кнопку «Копировать в файл».
4. На странице приветствия мастера экспорта сертификатов нажмите кнопку «Далее».
5. На странице «Экспортирование закрытого ключа» укажите, что хотите вместе с сертификатом экспортировать закрытый ключ.
6. На странице «Формат экспортируемого файла» выберите формат PKCS #12 (.PFX).
7. На странице «Пароль» задайте и подтвердите пароль доступа к экспортируемому закрытому ключу.
8. На странице «Имя файла экспорта» укажите диреткторию, в которой вы хотите создать файл с экспортируемыми ключами, и задайте имя этого файла.
9. На странице завершения работы мастера экспорта сертификатов нажмите кнопку «Готово».

### Для экспорта из КриптоПро CSP:
1. Перейти в Панель управления (ПУСК – Панель управления) найдите и запустить КриптоПро CSP.
2. На вкладке сервис выбрать «Просмотреть сертификат в контейнере».
3. Выбрать нужный контейнер и нажать «Далее». Если в контейнере присутствует сертификат, то отобразится информация о нём.
4. Нажать «Свойства». Откроется сам сертификат.
5. Перейти на вкладку «Состав». Нажать кнопку «Копировать в файл».
6. Выбрать варианты: «Нет, не экспортировать закрытый ключ» и «Файл в DER-кодировке X509» (.CER)
7. Указать путь для сохранения файла сертификата.
8. На вкладке сервис выбрать «Скопировать».
9. Выбрать нужный контейнер и нажать «Далее» и следуя мастеру, скопировать ключ на съемный носитель.

## Сборка

```
docker build -t gostpemextractor ./
```

## Запуск

Файл certificate.pfx и диреткория storage.001 находятся в текущей директории

При успехе в текущей директории создаются два файла certificate.crt.pem и certificate.key.pem
```
docker run --rm -ti -v `pwd`:/work gostpemextractor -f certificate.pfx -p password [-s storage.001]
```

