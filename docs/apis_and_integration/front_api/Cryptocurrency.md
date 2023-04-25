---
id: "Cryptocurrency"
---

# Cryptocurrency

The below listed crypto providers all have some additional parameter that needs to be included in the request for the transaction to be successful.

If the crypto provider you are adding is not listed, it means only the standard parameters are required.

## Apco

### CryptoCurrencyDeposit

`POST /api/cryptocurrency/deposit/process`

No provider specific params required - [To general request parameters](request)

### CryptoCurrencyWithdrawal

`POST /api/cryptocurrency/withdrawal/process`

| Name          | Located in   | Description                   | Data Type | Required | Example                            |
|---------------|--------------|-------------------------------|-----------|----------|------------------------------------|
| walletAddress | Request Body | Cryptocurrency wallet address | string    | false    | 3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy |

## Bitpace

### CryptoCurrencyDeposit

`POST /api/cryptocurrency/deposit/process`

No provider specific params required - [To general request parameters](request)

### CryptoCurrencyWithdrawal

`POST /api/cryptocurrency/withdrawal/process`

| Name           | Located in   | Description                    | Data Type | Required | Example                            |
|----------------|--------------|--------------------------------|-----------|----------|------------------------------------|
| walletAddress  | Request Body | Cryptocurrency wallet address  | string    | true     | 3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy |
| cryptoCurrency | Request Body | Crypto currency                | string    | true     | BTC                                |
| destinationTag | Request Body | Only required for Ripple (XRP) | string    | false    | 123456789                          |

## Bitpay

### CryptoCurrencyDeposit

`POST /api/cryptocurrency/deposit/process`

No provider specific params required - [To general request parameters](request)

## CryptoPay

### CryptoCurrencyDeposit

`POST /api/cryptocurrency/deposit/process`

| Name           | Located in   | Description     | Data Type | Required | Example |
|----------------|--------------|-----------------|-----------|----------|---------|
| cryptoCurrency | Request Body | Crypto currency | string    | true     | BTC     |

### CryptoCurrencyWithdrawal

`POST /api/cryptocurrency/withdrawal/process`

| Name           | Located in   | Description                   | Data Type | Required | Example                            |
|----------------|--------------|-------------------------------|-----------|----------|------------------------------------|
| walletAddress  | Request Body | Cryptocurrency wallet address | string    | true     | 3J98t1WpEZ73CNmQviecrnyiWrnqRhWNLy |
| cryptoCurrency | Request Body | Crypto currency               | string    | true     | BTC                                |

### CryptoPayDeposit

`POST /api/cryptopay/deposit/process`

| Name           | Located in   | Description     | Data Type | Required | Example |
|----------------|--------------|-----------------|-----------|----------|---------|
| cryptoCurrency | Request Body | Crypto currency | string    | true     | BTC     |

## CoinsPaid (Crytoprocessing.com)

### CryptoCurrencyDeposit

`POST /api/cryptocurrency/deposit/process`

| Name           | Located in   | Description     | Data Type | Required | Example |
|----------------|--------------|-----------------|-----------|----------|---------|
| cryptoCurrency | Request Body | Crypto currency | string    | true     | BTC     |

## Utorg

### CryptoCurrencyDeposit

`POST /api/cryptocurrency/deposit/process`

| Name           | Located in   | Description     | Data Type | Required | Example |
|----------------|--------------|-----------------|-----------|----------|---------|
| cryptoCurrency | Request Body | Crypto currency | string    | true     | BTC     |
