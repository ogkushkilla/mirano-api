# Документация серверного API

## Конечные точки (Endpoints)

### Получение товаров определённого типа

- **Метод**: GET
- **URL**: `/api/products?type=***`
- **Описание**: Запросы возвращают список товаров конкретного типа. Можно использовать фильтры по категории, цене и названию или получить товары по списку идентификаторов.
- **Параметр type**:
  - тип продукта, который может быть `bouquets`, `toys` или `postcards`.
- **Параметры запроса**:
  - `category`: строка (необязательный) - фильтр товаров по категории.
  - `minPrice`: число (необязательный) - фильтр товаров по минимальной цене.
  - `maxPrice`: число (необязательный) - фильтр товаров по максимальной цене.
    специфичных товаров.
- **Пример запроса**:
  - `/api/products?type=bouquets`
  - `/api/products?type=toys`
  - `/api/products?type=postcards`
  - Фильтрация: `/api/products?category=toys&minPrice=500`
  - Список ID: `/api/products?list=1,2,3`

### Получение всех продуктов

- **Метод**: GET
- **URL**: `/api/products`
- **Описание**: Запрос возвращает список всех продуктов. Можно получить товары по списку идентификаторов или названию (часть названия).
- **Параметры запроса**:
  - `name`: строка (необязательный) - поиск товаров, содержащих указанные символы в названии.
  - `list`: строка (необязательный) - список ID товаров, разделённых запятыми, для получения специфичных товаров.
- **Пример запроса**:
  - Все товары: `/api/products`
  - Список ID: `/api/products?list=1,2,3`
  - Список по совпадению названия: `/api/products?name=розы`

### Оформление заказа

- **Метод**: POST
- **URL**: `/api/orders`
- **Описание**: Запрос создаёт новый заказ с данными, предоставленными в теле запроса.
- **Тело запроса**:
  ```json
  {
    "buyer": {
      "name": "Иван Иванов",
      "phone": "1234567890"
    },
    "recipient": {
      "name": "Мария Петрова",
      "phone": "0987654321"
    },
    "address": "ул. Советская, дом 10, кв 15",
    "paymentOnline": true,
    "deliveryDate": "2023-10-05",
    "deliveryTime": "с 9:00 до 12:00",
    "products": [
      {
        "id": 1,
        "quantity": 2
      },
      {
        "id": 2,
        "quantity": 3
      }
    ]
  }
  ```

## Пример запроса с использованием cURL:

```bash
curl -X POST http://localhost:3000/api/orders -H 'Content-Type: application/json' -d '{
  "buyer": {"name": "Иван Иванов", "phone": "1234567890"},
  "recipient": {"name": "Мария Петрова", "phone": "0987654321"},
  "address": "ул. Советская, дом 10, г. Москва, Россия",
  "paymentOnline": true,
  "deliveryDate": "2023-10-05",
  "deliveryTime": "с 9:00 до 12:00",
  "products": [{"id": 1, "quantity": 2}, {"id": 2, "quantity": 3}],
  "total":
```

## Примечания

- Параметры, помеченные как "необязательный", могут быть опущены в запросе.
- Все данные, включая номера телефонов и адреса, должны быть предоставлены в соответствии с требованиями формата данных.
