## Подписание через QR

# Требование к QR

Содержимое QR кода должно быть представлено ссылкой в виде `https://<url>/{id}` (пример - `https://qr.msign.biz/1234567890`). Общая длина содержимого QR не должно превышать 100 символов.

# Требование к сервису

- Получение данных по QR

Получение данных осуществляется вызовом POST запроса на ссылку, указанной в QR.

Тело POST запроса представляет из себя объект в виде:
```
{
  x509certificate: <сертификат в кодировке base64>,
  authenticationToken: <ЭЦП сформированная подписью ссылки, указанной в QR>
}
```

Ответ:
```
{
  id: <идентификатор запроса на подпись>,
  secured: <данные предоставлены в зашифрованном виде - значения true/false>,
  data: <данные для подписания в формате base64>,
  contentType: <тип данных для подписание в соответствии со стандартом MIME>,
  signatureFormat: <один из форматов CAdES-BES, CAdES-EPES, CAdES-T, CAdES-C, CAdES-X-Long, CAdES-X-Type1, CAdES-X-Type2, CAdES-X-Type12, CAdES-A, XAdES-BES, XAdES-T, XAdES-C, XAdES-X, XAdES-X-L, XAdES-A, PAdES)
}
```

- Отправка данных по QR

Отправка данных осуществляется вызовом POST запроса на ссылку, указанной в QR путем добавления `/<id>` указанного в данных на запрос.

Тело POST запроса представляет из себя объект в виде:

```
{
  id: <идентификатор>,
  signatureFormat: <один из форматов CAdES-BES, CAdES-EPES, CAdES-T, CAdES-C, CAdES-X-Long, CAdES-X-Type1, CAdES-X-Type2, CAdES-X-Type12, CAdES-A, XAdES-BES, XAdES-T, XAdES-C, XAdES-X, XAdES-X-L, XAdES-A, PAdES),
  signedData: <Подписанные данные в необходимом формате>
}
```
