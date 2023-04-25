---
id: "kyc_features"
---
# KYC - Features

The following sections present detailed information about KYC module functionalities.

## KYC - Search

You can search KYC transactions by using either the smart search or the advanced search. By default, once you have clicked on the search tab, the latest transactions for each user are displayed. In order to view all transactions, you will need to add the filter **Show all tx** in either the smart search or the advanced one.

The smart search allows you to filter the results based on the following (merchant, user ID, date, score, email, transaction status, PEPs & sanction, provider, and/or displaying all related transactions).

![](/img/fraudrisk/kyc02.png)

Moreover, the advanced search allows you to export all the results into a spreadsheet. An example of some filters that exist at the advanced search can be seen in following screenshot.

![](/img/fraudrisk/kyc03.png)

By right clicking over any KYC transaction, you will be able to: 

- View transaction details
- View KYC response
- Export the page data

![](/img/fraudrisk/kyc04.png)

### View KYC response

By right clicking over any KYC transaction and selecting **View KYC response**, a new tab(screen) will be opened in order to view a summary of the KYC-response. This summary includes some details about: 

- The overall verification status
- Provider details
- Input details
- Age verification results
- Identity verification results  

![](/img/fraudrisk/kyc05.png)

### View transaction

By selecting **View transaction**, the payment transaction can be displayed in a new tab since each KYC transaction is connected to a payment transaction and can be accessed directly. The KycResult tag includes the results of KYC transaction.

![](/img/fraudrisk/kyc06.png)

### Export

By clicking on **Export**, the current displayed results, 100 KYC transactions, will be exported directly into a spreadsheet.

## KYC - Block

Payment transactions can be declined or accepted based on specific predefined criteria.

Conditions can be specified and accordingly actions can be taken. Besides transaction acceptance or declination, an email can be triggered according to your template details.

![](/img/fraudrisk/kyc07.png)

## KYC - Routing

You can configure a routing rule to a specific provider in order to force the system to trigger a KYC check for the payment transaction according to a predefined criteria by specifying the conditions.

The main conditions that you can use are: 

- KYC age status
- KYC ID status
- Internal KYC status

Beside these ones, there is a long list of conditions that you can utilize according to your criteria.

When it comes to the **KYC age status** as well as **KYC ID status**, you can map them according to your provider’s configured profile. This mapping can be updated accordingly at your provider config (GbgConfig and CallcreditConfig). The status in either one of them can be `ERROR`, `UNDER_AGE`, `NOT_VERIFIED` or `VERIFIED`.

In regards to the **Internal KYC status**, it is calculated based on different factors for each provider. Consequently, an internal status is specified accordingly. Following table provides further details about how the internal status is specified.

### CallCredit 

- If the user was under 18 years the internal status will be `UNDER_AGE`
- Otherwise, if the user did NOT pass the identity check, then the status will be `VERIFICATION_FAILED`
- Otherwise, if the user passed the identity check, then the status will be `VERIFIED` 
- If something is wrong with the response, the status will be `VERIFICATION_EXTERNAL_FAILURE`

### GBGroup

- If the age status was VERIFIED OR the ID status was VERIFIED, then the status will be `VERIFIED`
- Otherwise, if the age status UNDER_AGE OR id status was UNDER_AGE, then the status will be `UNDER_AGE`
- Otherwise, if the age status NOT_VERIFIED OR id status was NOT_VERIFIED, then the status will be `NOT_VERIFIED`
- If something is wrong with the response, the status will be `VERIFICATION_EXTERNAL_FAILURE`
- Otherwise, the status will be `VERIFICATION_FAILED`

The following are the current internal KYC status types:
- `VERIFIED`
- `VERIFICATION_IN_PROGRESS`
- `VERIFICATION_FAILED`
- `VERIFICATION_EXTERNAL_FAILURE`
- `VERIFICATION_FAILED_INVALID_USER_DATA`
- `NOT_VERIFIED`
- `BLOCKED`
- `UNDER_AGE`
- `UNKNOWN`
- `UNKNOWN_AGE`

![](/img/fraudrisk/kyc08.png)

## KYC - Fallback
You can configure a fallback rule based on the received response from a specific KYC provider, in case you are using more than one provider, and in order to investigate the case further. This way, you could double check the KYC status using two providers if you were not satisfied by the results or even in case of failure to check the status as a backup plan.

The following example provides a fallback rule in case that Callcredit failed to verify the ID of the client, or if an error occurred in their response.

![](/img/fraudrisk/kyc09.png)
