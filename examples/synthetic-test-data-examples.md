# Synthetic test data examples

## 1. Good synthetic customer dataset

```json
[
  {
    "customer_id": "cust_1001",
    "full_name": "Aleksey Morozov",
    "birth_date": "1991-07-14",
    "phone": "+7-999-000-10-01",
    "email": "aleksey.morozov@example.test",
    "segment": "mass_affluent"
  },
  {
    "customer_id": "cust_1002",
    "full_name": "Elena Petrova",
    "birth_date": "1988-03-22",
    "phone": "+7-999-000-10-02",
    "email": "elena.petrova@example.test",
    "segment": "retail"
  }
]
```

Почему это хорошо:
- данные выглядят реалистично;
- используются заведомо тестовые идентификаторы и домены;
- нет привязки к реальным клиентам.

## 2. Good synthetic transaction dataset

```json
[
  {
    "transaction_id": "txn_5001",
    "customer_id": "cust_1001",
    "amount": 12500,
    "currency": "RUB",
    "channel": "mobile_app",
    "status": "pending"
  },
  {
    "transaction_id": "txn_5002",
    "customer_id": "cust_1002",
    "amount": 98000,
    "currency": "RUB",
    "channel": "web",
    "status": "completed"
  }
]
```

## 3. Bad synthetic data example

```json
{
  "full_name": "Ivan Ivanov",
  "passport": "4510 123456",
  "card_number": "4276380012345678",
  "phone": "+7-921-123-45-67"
}
```

Почему это плохо:
- слишком похоже на реальные персональные данные;
- содержит номер карты;
- может нарушать требования по банковской тайне и защите данных.

## 4. Safe masking example

Исходно:

```text
Client Ivan Ivanov transferred 12000 RUB from account 40817810000000000001
```

Безопасно для теста:

```text
Client [CUSTOMER_001] transferred 12000 RUB from account [ACCOUNT_001]
```

## 5. Rules of thumb

- использовать `.test`, `.example`, `cust_*`, `txn_*`;
- не использовать реальные ИНН, номера карт, счетов и паспортов;
- отдельно маркировать synthetic datasets как synthetic.
