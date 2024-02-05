# E-Wallet System


##### Dependencies:
 - golang `https://golang.org/doc/install`
 - dep `https://github.com/golang/dep`
 
##### Build:
```
make build
```

One day, I thought of building a fintech application that facilitates non-cash transactions. As the Minimum Viable Product (MVP), this is the application to have the following features:

##Transactions:

1. Customers can register.
2. As the owner, you can register new merchants who can conduct transactions.
3. Customers can top up their balance.
4. Customers can make payments to registered merchants.

##Meet the actors:

- Customer
- Merchant
- Transaction

##Actions:

- Customer can register.
- Merchant can be registered by the owner and conduct transactions.
- Customers can top up their balance.
- Customers can make transactions with registered merchants.



Some Spec: 
```
GIVEN I am unregister person
WHEN i register as customer with (name, email, phone)
THEN E-wallet should record it as new customer and return my wallet-id

GIVEN I am owner of E-wallet
WHEN i register new merchant with (name, email)
THEN e-wallet should record it as new merchant and return merchant wallet-id

GIVEN I am customer of E-wallet
WHEN i topup some amount
THEN e-wallet my balance should increased

GIVEN I am customer of Ewallet
WHEN i pay merchant 
THEN my balance should decreased, and merchant balance should increased, and i get transactionsID
```

```
(entity) user_accounts
 - user_id
 - name
 - email
 - phonenumber
 - user_type (merchant | customer)

(entity) wallet
 - wallet_id
 - user_id
 - balance

(entity) transaksi
  - id
  - reference
  - date
  - description
  - type (topup | payment)
  
topup:
  - credit wallet

payment:
  - credited wallet (merchant walletid)
  - debited wallet (customer walletid)
```

```
service
  - register_customer | register_merchant =
    - add new user to user_accounts
    - add new wallet to wallet 

  - topup:
    - add new transaksi with type topup 
    - increase balance from wallet

  - payment:
    - add new transaksi with type payment 
    - decrease balance from debited wallet
    - incrase balance from credited wallet
```

```
API:
  -> :register_customer
    {
      "name": "",
      "email": "",
      "phonenumber": ""
    }
  -> :register_merchant
    {
      "name": "",
      "email": ""
    }
  -> :topup
    {
      "wallet_id": "",
      "amount": ""
    }
  -> :payment
    {
      "wallet_id": "",
      "amount": "",
      "merchant_id": ""
    }
 ```

