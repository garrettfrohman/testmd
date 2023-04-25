---
id: "backoffice-users"
---

# Backoffice Users

This​ ​is​ ​the​ ​area​ ​where​ ​merchant​ ​administrators​ ​can​ ​create,​ ​enable​ ​and​ ​disable,​ ​and adjust​ ​permissions​ ​granted​ ​to​ ​the​ ​merchant​ ​users​ ​of​ ​PaymentIQ.

## Creating a new User

Users​ ​with​ ​administrative​ ​privileges​ ​can​ ​create​ ​additional​ ​users​ ​and​ ​assign​ ​roles​ ​to​ ​that user.

1. Click​ ​on​ ​the​ ​“Admin”​ ​tab

2. Click​ ​on​ ​“Back​ ​office​ ​Users”

3. Click​ ​on​ ​“New?”​ ​and​ ​the​ ​new​ ​user​ ​form​ ​will​ ​be​ ​displayed​ ​where​ ​you​ ​may​ ​create​ ​a new​ ​user.​ ​Once​ ​a​ ​user​ ​is​ ​created,​ ​access​ ​to​ ​certain​ ​roles​ ​in​ ​order​ ​to​ ​perform certain​ ​tasks,​ ​and​ ​viewing​ ​capabilities​ ​within​ ​the​ ​back​ ​office,​ ​can​ ​be​ ​given​ ​by simply​ adding them in the multiple select input 'Roles'.​ ​These​ ​user​ ​characteristics​ ​can​ ​be​ ​edited​ ​at​ ​any time.

4. Click​ ​on​ ​“Save”​ ​and​ a welcome email will be sent to the newly created user with a link to choose password and finalize the creation.​

Example​ ​setup​ ​for​ ​a​ ​Payments​ ​Agent​ ​with​ ​transaction​ ​search​ ​and​ ​approval​ ​permissions.

![](/img/settingsandadmin/AdminBackofficeUsers/1.png)

Once created and added to the list of back office users, two new options become available to reset the user's password and also a checkbox for forcing the user to change the password on next login. From here it is also possible  to either disable/enable the user or deleting the user entirely.

![](/img/settingsandadmin/AdminBackofficeUsers/2.png)

## Managing User Accounts

In the test/staging environment our Technical Support and Onboarding teams are available to help out with password resets, role changes and other backoffice user tasks on the request of merchants.

But for the live/production environment it is very important that merchant's are ready to manage this on their own. You as a merchant is strogly recommended to have staff available to help colleagues out with password resets, role management and to unlock accounts when that happens. Our Technical Support team are not allowed to change these user settings in the live environment unless contacted by a verified contact, and this should be seen as a absolute last resort to resolve account issues.


## PaymentIQ User Role definitions

| Role                           | Description                                                                                                                                                                                                                                                                  |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ROLE_MERCHANT_SUPPORT          | Full access to “Transactions” section, full search and download permissions. View access to “Approve” section, full search and download permissions. No approve permissions.                                                                                                 |
| ROLE_MERCHANT_ADMIN            | Allows complete access to all functionalities. Note: This role should only be set for admin users.                                                                                                                                                                           |
| ROLE_INVESTIGATOR              | Limited access to “Transactions” full access to “Investigate” for forcing inconsistent transactions ONLY to become successful or failed.                                                                                                                                     |
| ROLE_INVESTIGATOR_ADMIN        | Limited access to “Transactions” full access to “Investigate” for forcing ANY transactions to become successful or failed. Warning: Internal fraudster might misuse this role to top up user accounts with fake money.                                                       |
| ROLE_USER_PSP_ACCOUNT          | Limited access to “Transactions”, full access to “User accounts” for status changes (e.g.activating, inactivating, blocking, or deleting).                                                                                                                                   |
| ROLE_USER_EDIT_PSP_ACCOUNT     | Deprecated,​​ do​​ not ​​use                                                                                                                                                                                                                                                       |
| ROLE_USER_PSP_ACCOUNT_ADMIN    | Limited access to “Transactions”, full access to “User accounts” for status changes plus access to edit users’ PSP account details.Warning: Internal fraudster might misuse this role to change account details, such as bank account numbers.                               |
| ROLE_STORE                     | Deprecated,​​ do​​ not ​​use                                                                                                                                                                                                                                                       |
| ROLE_STORE_ADMIN               | Deprecated,​​ do​​ not ​​use                                                                                                                                                                                                                                                       |
| ROLE_AGENT                     | Limited access to “Transactions” section, with limited search. Typical as a CS agent role.                                                                                                                                                                                   |
| ROLE_KYC                       | Limited access to the “KYC” section for searching KYC transactions                                                                                                                                                                                                           |
| ROLE_KYC_ADMIN                 | Full access to the “KYC” section including editing age status and id status.                                                                                                                                                                                                 |
| ROLE_IIN                       | Limited access to view and edit info about IIN numbers, also known as BIN numbers.                                                                                                                                                                                           |
| ROLE_IIN_ADMIN                 | Full access to view and edit info about IIN numbers, and delete entries.                                                                                                                                                                                                     |
| ROLE_MAINTENANCE_SUPPORT       | Role​ ​for​ ​viewing​ ​maintenance​ ​info                                                                                                                                                                                                                                            |
| ROLE_MAINTENANCE_ADMIN         | Full​ ​access​ ​to​ ​view,​ ​edit​ ​and​ ​delete maintenance​ ​info.                                                                                                                                                                                                                       |
| ROLE_RULES                     | Limited view only access to "Rules" section.                                                                                                                                                                                                                                 |
| ROLE_RULES_ADMIN               | Full view and edit access to "Rules" section.                                                                                                                                                                                                                                |
| ROLE_TRANSACTION_VIEWER        | Limited access to "Transactions" section without export functionality.                                                                                                                                                                                                       |
| ROLE_TRANSACTION_DETAIL_VIEWER | Full access to view transaction history details.                                                                                                                                                                                                                             |
| ROLE_DATA_VIEWER               | Full access to view masked data in transactions/approve/investigate/kyc/analytics view.                                                                                                                                                                                      |
| ROLE_FIRST_APPROVER            | Can approve single approval withdrawals and can act as first approver of a TWO_LEVEL_APPROVAL withdrawal. Please note that a user with both ROLE_FIRST_APPROVER and ROLE_SECOND_APPROVER roles can act as both first and second approver on the same transaction.            |
| ROLE_SECOND_APPROVER           | Can not approve single approval withdrawals but can act only as second approver of a TWO_LEVEL_APPROVAL withdrawal. Please note that a user with both ROLE_FIRST_APPROVER and ROLE_SECOND_APPROVER roles can act as both first and second approver on the same transaction.  |
| ROLE_ADMIN_APPROVER            | Can approve single approval withdrawals and can act as second approver. Can also act as both first and second approver on the same transaction.                                                                                                                              |
| ROLE_CONFIG_ADMIN              | Role for edit / add / view configuration                                                                                                                                                                                                                                     |
| ROLE_ANALYTICS                 | Real Time Analytics functionality/tab / Kibana based transaction overview, statistics and monitoring system                                                                                                                                                                                                                            |
| ROLE_ANALYTICS_ADMIN           | Role for edit / add / view and change widgets and dashboards in Real Time Analytics / Analytics tab                                                                                                                                                                                                                                     |


# Two Factor Authentication

PaymentIQ enforces the use of Two Factor Authentication (2FA) for backoffice users. 2FA adds an extra security layer by requiring the user to provide two different authentication factors to verify their identity. This means that in addition to providing the password the user will be required to identify themselves via for example an authentication app on a mobile phone, or an SMS code, which makes the system more secure.

## Which users can manage 2FA

2FA is enforced on all users, but it can be managed by a user that has role `ROLE_MERCHANT_ADMIN`, for example if you have to force a user to redo the authentication setup.

## Activating 2FA on a new user

When a backoffice user admin with role `ROLE_MERCHANT_ADMIN` creates a new user, there are two fields that control 2FA which have to be selected.

![](/img/settingsandadmin/AdminBackofficeUsers/2FA1.png)

### 2-Factor

There is one main option which a merchant admin will be able to choose:
- **2-Factor Authentication Required:** Specifies that the user is required to log in with 2FA.

### User Actions

Gives two options to set the 2FA method:
- **Set up Authenticator Application:** The user must give a One Time Password via a mobile app. The App is chosen by the user on the first login after this is set.
- **Set up Security Key:** The user must have a Security Key on for example a USB or YubiKey connected to the computer to log in. The key is configured on the first login after this is set. This 2FA method is commonly known as [WebAuthn](https://webauthn.io/).

Please note that you can also set both at the same time to give the user the option themselves regarding which method to identify with.

After you have specified the requirement and user action press **Save** for the new requirement to be implemented.

## Activating 2FA via Presets in MerchantConfig

This method enables a dropdown menu in the backoffice user creation page with previously specified 2FA option sets. This could be useful for larger organizations with many users where you want to have better oversight.

### Enabling backoffice user presets

As an example, by adding the following in the MerchantConfig in the backofficeConfig section on the MID you wish to have the preset options:

```xml
<backofficeConfig>
    <userPresetsConfig>
      <entry>
        <string>preset1</string>
        <userPresets>
          <twoFactorCondition>required</twoFactorCondition>
          <requiredActions>CONFIGURE_TOTP,webauthn-register</requiredActions>
        </userPresets>
      </entry>
      <entry>
        <string>preset2</string>
        <userPresets>
          <twoFactorCondition>required</twoFactorCondition>
          <requiredActions>CONFIGURE_TOTP</requiredActions>
        </userPresets>
      </entry>
    </userPresetsConfig>
</backofficeConfig>
```

This enables the dropdown when you create new users:

![](/img/settingsandadmin/AdminBackofficeUsers/2FA2.png)

In this case, if you chose preset1 2FA is required for the user and both identity methods are enabled as an option. If you chose preset1 only the authenticator app option will be enabled .

## Activating 2FA via My Account

As a backoffice user you can activate 2FA on your own account by clicking the top right button with your account name on it and selecting **Your Account** in the dropdown.

You are then presented with a **Welcome to Account Management** section where you chose **Signing In** under **Account Security**

![](/img/settingsandadmin/AdminBackofficeUsers/2FA3.png)

On the following page under **Two-Factor Authentication** you have the two options for 2FA method

- Authenticator Application
- Security Key

![](/img/settingsandadmin/AdminBackofficeUsers/2FA4.png)

You can see the status of your current settings, but also chose to set up either by clicking **Set Up Authenticator Application** / **Set Up Security Key**. The link will prompt you to log in again and then you will be taken to the 2FA methods configuration page. Please see the **Logging in with 2FA** section for more details.

## Logging in with 2FA

### Using Authenticator Application

On the first login you will be presented with an instruction to install one of the two supported authentication apps and set up the account. Please follow the instructions.

![](/img/settingsandadmin/AdminBackofficeUsers/2FA5.png)

After you have configured the app you will be prompted on each login to enter a One Time Password generated in the application, proving that you have access not only to the backoffice password but also the mobile device for 2FA.

### Using Security Key

On the first login you will be presented with a button to **register** the USB security key.

![](/img/settingsandadmin/AdminBackofficeUsers/2FA6.png)

By clicking the button a popup appears prompting to insert the key to enable it. PaymentIQ supports the following types of Security Keys:
- USB-Dongle Authentication. For example [YubiKey](https://www.yubico.com/authentication-standards/webauthn/)
- [Apple TouchId](https://support.apple.com/en-gb/HT207054)
- [Microsoft Windows Hello](https://support.microsoft.com/en-us/help/4028017/windows-learn-about-windows-hello-and-set-it-up)

![](/img/settingsandadmin/AdminBackofficeUsers/2FA7.png)

After you have configured the device you will be required to have it connected on every login, proving that you have access not only to the backoffice password but also the USB security key for 2FA.
