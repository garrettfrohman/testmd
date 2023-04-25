---
id: "cardmigration"
---


# Card migration & card import

When you (referred as merchant from now on) migrating from another platform or PSP to PaymentIQ it's sometimes to keep 
existing agreements and records to keep payment experience and to be able to
keep subscriptions and COF transactions without the need for customers to re-enter
credentials. 

### Migration and import process
In order to do this securely a few things need to be exported from the existing provider. 
1. PCI provider needs to send their public key to the project manager or account manager|
2. PIQ will return a username to be used when accessing the server (using public key from step 1)
3. PCI provider makes a test file. The file should be a comma separated CSV file.
    Export file needs to consist of, but is not limited to, the following data:
    
      |Data parameter | Description|
      |----------|------|
      |merchant-user-id | Some identifier that the merchant recognizes as an identifier of the end customer. |
      |token | If the same merchant user ID has multiple stored credentials, this identifier can be used in conjunction to merchant user id|
      |merchant-id | PaymentIQ MID that the import should be done to|
      |PAN | Card number|
      |expiry date | Expiry date for the PAN|
      |cardholder name | Name of the card holder|
   
4. PCI provider makes an export file and uploads it to our SFTP server:
http://export.paymentiq.io/
The migrating data needs to be done in two copies encrypted using the following ASC-files. 

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
RrrG0K++IJsech93C37s
=RA5N
-----END PGP PUBLIC KEY BLOCK----- 
```

and

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

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
=7Thv
-----END PGP PUBLIC KEY BLOCK-----
```

5. PaymentIQ team will return with a response file including the export file parameters and your new payment UUIDs (payment tokens)
6. If all is OK. A Full export can be done.
