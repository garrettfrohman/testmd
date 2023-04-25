---
id: "payretailers"
title: "PayRetailers"
hide_title: "true"
---

![](/img/providers/logos/payretailers.png)

# PayRetailers

## About
PayRetailers is a payment provider offering bank deposit and withdrawal operations (in local currency). PIX Withdrawal in Brazil is also supported.

| Provider Name                | PayRetailers                                                                                                     |
|------------------------------|------------------------------------------------------------------------------------------------------------------|
| Link                         | [https://payretailers.com/en/](https://payretailers.com/en/)                                                     |
| Classification               | Credit Cards and Online/Cash Bank payments                                                                       |
| API                          | Please contact our technicals support team for information.                                                      |
| Regions                      | Argentina, Brazil, Columbia, Costa Rica, Chile, Ecuador, El Salvador, Guatemala, Mexico, Nicaragua, Panama, Peru |
| Currencies                   | `USD`, `BRL`, `CLP`, `MXN`, `COP`, `CRC`, `GTQ` ,`PEN`, `ARS`                                                    |
| Methods/PaymentTxTypes       | `WebRedirectDeposit`, `PayRetailersWithdrawal`, `PixWithdrawal`, `Reversal`                                      |
| PaymentIQ Configuration File | `PayRetailersConfig`                                                                                             |

## Configuration Information

<details>
<summary>Click to view example configuration</summary>
<br/>

```xml
<com.devcode.paymentiq.integration.payretailers.PayRetailersConfig>
  <enabled>true</enabled>
  <useViqProxy>false</useViqProxy>
  <accounts>
    <entry>
      <string>DEFAULT</string>
      <account>
        <accountID>??</accountID>
        <secretKey>??</secretKey>
        <beneficiaryAccountType>person</beneficiaryAccountType><!-- person|company (for Chile only) -->
        <transactionChannel>ONLINE</transactionChannel><!--ONLINE|CASH-->
        <supportedCurrencies>USD|BRL|CLP|MXN|COP</supportedCurrencies>
        <language>en</language>
      </account>
    </entry>
  </accounts>
  <testMode>false</testMode>
  <container>window</container>
  <defaultDescriptor>Test payment ${ptx.txRefId}</defaultDescriptor>
</com.devcode.paymentiq.integration.payretailers.PayRetailersConfig>

```
</details>

### Attributes

| Attribute              | Description                                                                                                                                        |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| accountID              | Corresponds to 'shop-id' from PayRetailers. One of the parameters used in the process of authentication                                            |
| secretKey              | Corresponds to 'shop-key' from PayRetailers. One of the parameters used in the process of authentication                                           |
| beneficiaryAccountType | Beneficiary account type that is required for Chile only. Possible values are: person, company                                                     |
| transactionChannel     | Payout channel that is required for Ecuador and Peru only. Possible values are `ONLINE` or `CASH`. `ONLINE` is used by default if none is defined. |
| defaultDescriptor      | Optional parameter that is used to define a payment reason                                                                                         |


### Note

Currently CLP currency is not supported. USD must be used instead.

## Example Routing Rules
![](/img/providers/routing/payretailers.png)

## Transaction flow

The integration supports two different flows, "Paywall" and direct transactions.

### Paywall

If you as a merchant want only one option in the cashier (called "PayRetailers" for example), you only need to add the WEBREDIRECT as a payment method and send blank (null or "") or PAYWALL service in the request. When a deposit is initiated this way, the end-user will be redirected to PayRetailers page where they will identify the customer's country or IP and will display the available payment methods according with the selected country.

The mandatory fields will vary from one country to another, but the paywall is also designed so in case there is any missing parameters it will be requested before moving on to send the request to the APM, so for example, for Brazil if you send the request without PersonalID (National CPF) the paywall will show a form asking for this missing parameter.

### Direct transaction

As opposed to the paywall flow, if you instead want to display the different APMs directly in the PaymentIQ cashier (or your own), you can solve this by separating each APM as its own "service" with the WEBREDIRECT payment method. A guide on how to do this can be found [here](/docs/configuration_and_administration/system_configuration/servicemapping).

When the transaction is initiated with the specific service like this, the end-user will end up directly on the selected payment method page, instead of landing on PayRetailers page first.

This is an example of how the cashier could look for a Brazilian user.

![](/img/providers/payretailers_cashier.png)

Much like the paywall solution, PayRetailers will request the end-user if there are any missing parameters. However, to better streamline the payment flow it's recommended to make sure to provide all of the needed data from the beginning. The most important being the PersonalID (CPF/RUT). To make sure that PIQ can send this value directly to PayRetailers, you as a merchant has to make sure to provide this value as an `attribute` in the verifyuser response of the Integration API.

The attribute value needs to be sent with the parameter `nationalIdentificationNumber` as in the example below (shortened to save space).

```json
{
  "success": true,
  "userId": "user_123",
  "firstName": "John",
  "lastName": "Doe",
  ...
  "attributes": {
    "nationalIdentificationNumber": "86758181650"
  },
  ...
}
```

#### Service values

Here is a list of the supported service values to send per country and bank when using direct transactions.

| Bank name                      | Service value          | Country |
|--------------------------------|------------------------|---------|
| Boleto                         | BOLETO                 | BRA     |
| Boleto Flash                   | BOLETO_FLASH           | BRA     |
| Boleto PIX                     | BOLETO_PIX             | BRA     |
| Transferencia Bancaria         | TRANSFERENCIA_BANCARIA | BRA     |
| Banco Itaú                     | ITAU                   | BRA     |
| Santander Brasil               | SANTANDER_BR           | BRA     |
| Banco do Brasil                | BANCODOBRASIL          | BRA     |
| Banrisul                       | BANRISUL               | BRA     |
| Bradesco (cash)                | BRADESCO_CASH          | BRA     |
| Bradesco (online)              | BRADESCO_ONLINE        | BRA     |
| OXXO                           | OXXO                   | MEX     |
| SPEI                           | SPEI                   | MEX     |
| Banco Azteca                   | AZTECA                 | MEX     |
| Banorte                        | BANORTE                | MEX     |
| OpenPay                        | OPENPAY                | MEX     |
| BBVA Bancomer (cash)           | BBVA_CASH              | MEX     |
| BBVA Bancomer (online)         | BBVA_ONLINE            | MEX     |
| Scotiabank (cash)              | SCOTIABANK_CASH        | MEX     |
| Scotiabank (online)            | SCOTIABANK_ONLINE      | MEX     |
| HSBC (cash)                    | HSBC_CASH              | MEX     |
| HSBC (online)                  | HSBC_ONLINE            | MEX     |
| Santander Mexico (cash)        | SANTANDER_MX_CASH      | MEX     |
| Santander Mexico (online)      | SANTANDER_MX_ONLINE    | MEX     |
| Banco TBanc                    | TBANC                  | CHL     |
| Banco BCI                      | BCI                    | CHL     |
| Banco Walmart - aCuenta        | WALMART_ACUENTA        | CHL     |
| Banco Walmart - Lider          | WALMART_LIDER          | CHL     |
| Express Lider                  | EXPRESS_LIDER          | CHL     |
| Santander Chile                | SANTANDER_CL           | CHL     |
| WebPay                         | WEBPAY                 | CHL     |
| Servipag                       | SERVIPAG               | CHL     |
| Multicaja                      | MULTICAJA              | CHL     |
| Mach                           | MACH                   | CHL     |
| Khipu                          | KHIPU                  | CHL     |
| Tambo                          | TAMBO                  | PER     |
| BCP, Banco de Crédito (cash)   | BCP_CASH               | PER     |
| BCP, Banco de Crédito (online) | BCP_ONLINE             | PER     |
| BBVA Continental (cash)        | BBVA_PE_CASH           | PER     |
| BBVA Continental (online)      | BBVA_PE_ONLINE         | PER     |
| Caja Arequipa (cash)           | CAJA_AREQUIPA_CASH     | PER     |
| Caja Arequipa (online)         | CAJA_AREQUIPA_ONLINE   | PER     |
| Caja Huancayo (cash)           | CAJA_HUANCAYO_CASH     | PER     |
| Caja Huancayo (online)         | CAJA_HUANCAYO_ONLINE   | PER     |
| Caja Tacna (cash)              | CAJA_TACNA_CASH        | PER     |
| Caja Tacna (online)            | CAJA_TACNA_ONLINE      | PER     |
| Caja Trujillo (cash)           | CAJA_TRUJILLO_CASH     | PER     |
| Caja Trujillo (online)         | CAJA_TRUJILLO_ONLINE   | PER     |
| Interbank (cash)               | INTERBANK_CASH         | PER     |
| Interbank (online)             | INTERBANK_ONLINE       | PER     |
| Banco Ripley                   | BANCO_RIPLEY           | PER     |
| Scotiabank (cash)              | SCOTIABANK_PE_CASH     | PER     |
| Scotiabank (online)            | SCOTIABANK_PE_ONLINE   | PER     |
| Pago Efectivo (cash)           | PAGO_EFECTIVO_CASH     | PER     |

## Data

### Brazil (BR)

#### Document Type

| Value | Description |
|-------|-------------|
| 1     | CPF         |

#### Account Type

| Value | Description    |
|-------|----------------|
| 0001  | Poupança       |
| 0002  | Conta Corrente |

#### Bank Name

| Value | Description                                        |
|-------|----------------------------------------------------|
| 001   | Banco do Brasil S.A.                               |
| 341   | Banco Itaú S.A.                                    |
| 033   | Banco Santander (Brasil) S.A.                      |
| 237   | Banco Bradesco S.A.                                |
| 237   | Next Tecnologia e Serviços Digitais                |
| 104   | Caixa Econômica Federal                            |
| 422   | Banco Safra S.A.                                   |
| 748   | Banco Cooperativo Sicredi S.A.                     |
| 041   | Banco do Estado do Rio Grande do Sul S.A. BANRISUL |
| 208   | BANCO BTG PACTUAL S.A.                             |
| 655   | Neon Pagamentos                                    |
| 077   | Banco Inter S.A.                                   |
| 121   | Banco Agibank S.A.                                 |
| 212   | Banco Original S.A.                                |
| 260   | Nubank                                             |
| 336   | Banco C6 S.A.                                      |

### Chile (CL)

#### Document Type

| Value  | Description |
|--------|-------------|
| cl_rut | RUT         |

#### Account Type

| Value | Description                    | Bank         |
|-------|--------------------------------|--------------|
| 0001  | Cuenta Corriente / Cueta Vista | All banks    |
| 0003  | Chequera electrónica           | Banco Estado |
| 0004  | Cuenta RUT                     | Banco Estado |

#### Beneficiary Type
`person`, `company`

#### Bank Name

| Value | Description                                               |
|-------|-----------------------------------------------------------|
| 012   | Banco Del Estado De Chile                                 |
| 504   | Banco Bbva (Bilbao Vizcaya Argentaria Chile) / Banco Bhif |
| 028   | Banco Bice                                                |
| 055   | Banco Consorcio                                           |
| 027   | Banco Corpbanca                                           |
| 001   | Banco De Chile / Banco A. Edwards / Credichile / Citybank |
| 016   | Banco De Crédito E Inversiones (BCI) / Tbanc              |
| 507   | Banco Del Desarrollo                                      |
| 051   | Banco Falabella                                           |
| 009   | Banco Internacional                                       |
| 039   | Banco Itau Chile / Bank Boston                            |
| 053   | Banco Ripley                                              |
| 057   | Banco París                                               |
| 037   | Banco Santander – Santiago / Banco Santander / Banefe     |
| 049   | Banco Security                                            |
| 672   | Coopeuch                                                  |
| 031   | Hsbc Bank (Chile)                                         |
| 014   | Scotiabank / Sud – Americano                              |

### Mexico (MX)

#### Document Type

| Value | Description |
|-------|-------------|
| 40    | General     |

#### Account Type

| Value | Description |
|-------|-------------|
| 0001  | General     |

#### Bank Name

| Value | Description      |
|-------|------------------|
| 37006 | BANCOMEXT        |
| 37009 | BANOBRAS         |
| 37019 | BANJERCITO       |
| 37135 | NAFIN            |
| 37166 | BANSEFI          |
| 37168 | HIPOTECARIA FED  |
| 40002 | BANAMEX          |
| 40012 | BBVA BANCOMER    |
| 40014 | SANTANDER        |
| 40021 | HSBC             |
| 40030 | BAJIO            |
| 40036 | INBURSA          |
| 40042 | MIFEL            |
| 40044 | SCOTIABANK       |
| 40058 | BANREGIO         |
| 40059 | INVEX            |
| 40060 | BANSI            |
| 40062 | AFIRME           |
| 40072 | BANORTE          |
| 40102 | ACCENDO BANCO    |
| 40103 | AMERICAN EXPRESS |
| 40106 | BANK OF AMERICA  |
| 40108 | MUFG             |
| 40110 | JP MORGAN        |
| 40112 | BMONEX           |
| 40113 | VE POR MAS       |
| 40124 | DEUSTCHE         |
| 40126 | CREDIT SUISSE    |
| 40127 | AZTECA           |
| 40128 | AUTOFIN          |
| 40129 | BARCLAYS         |
| 40130 | COMPARTAMOS      |
| 40131 | BANCO FAMSA      |
| 40132 | MULTIVA BANCO    |
| 40133 | ACTINVER         |
| 40136 | INTERCAM BANCO   |
| 40137 | BANCOPPEL        |
| 40138 | ABC CAPITAL      |
| 40140 | CONSUBANCO       |
| 40141 | VOLKSWAGEN       |
| 40143 | CIBANCO          |
| 40145 | BBASE            |
| 40147 | BANKAOOL         |
| 40148 | PAGATODO         |
| 40150 | INMOBILIARIO     |
| 40151 | DONDE            |
| 40152 | BANCREA          |
| 40154 | BANCO FINTERRA   |
| 40155 | ICBC             |
| 40156 | SABADELL         |
| 40157 | SHINHAN          |
| 40158 | MIZUHO BANK      |
| 40160 | BANCO S3         |
| 90600 | MONEXCB          |
| 90601 | GBM              |
| 90602 | MASARI           |
| 90605 | VALUE            |
| 90606 | ESTRUCTURADORES  |
| 90608 | VECTOR           |
| 90613 | CBOLSA           |
| 90616 | FINAMEX          |
| 90617 | VALMEX           |
| 90620 | PROFUTURO        |
| 90630 | CB INTERCAM      |
| 90631 | CI BOLSA         |
| 90634 | FINCOMUN         |
| 90636 | HDI SEGUROS      |
| 90638 | AKALA            |
| 90642 | REFORMA          |
| 90646 | STP              |
| 90648 | EVERCORE         |
| 90652 | CREDICAPITAL     |
| 90653 | KUSPIT           |
| 90656 | UNAGRA           |
| 90659 | ASP INTEGRA OPC  |
| 90670 | CB LIBERTAD      |
| 90677 | CAJA POP MEXICA  |
| 90680 | CRISTOBAL COLON  |
| 90683 | CAJA TELEFONIST  |
| 90684 | TRANSFER         |
| 90685 | FONDO (FIRA)     |
| 90686 | INVERCAP         |
| 90689 | FOMPED           |
| 90902 | INDEVAL          |
| 90903 | CoDi Valida      |

### Colombia (CO)

#### Document Type

| Value | Description                  |
|-------|------------------------------|
| 01    | Cedula Ciudadanía (CC)       |
| 02    | Cedular de Extranjería (CE)  |
| 03    | NIT (NT)                     |
| 04    | Tarjeta de Identidad (TI)    |
| 06    | NII de Establecimientos (NE) |

#### Account Type

| Value | Description |
|-------|-------------|
| 0001  | Ahorros     |
| 0002  | Corriente   |

#### Bank Name

| Value | Description                                         |
|-------|-----------------------------------------------------|
| 0001  | BANCO DE BOGOTA                                     |
| 0002  | BANCO POPULAR                                       |
| 0006  | BANCO CORPBANCA COLOMBIA SA.                        |
| 0007  | BANCOLOMBIA                                         |
| 0009  | CITIBANK                                            |
| 0012  | BANCO GNB SUDAMERIS                                 |
| 0013  | BBVA COLOMBIA                                       |
| 0019  | BANCO COLPATRIA                                     |
| 0023  | BANCO DE OCCIDENTE                                  |
| 0031  | BANCOLDEX                                           |
| 0032  | BANCO BCSC SA (Banco Caja Social)                   |
| 0040  | BANCO AGRARIO                                       |
| 0041  | JPMORGAN CORPORACION FINANCIERA                     |
| 0042  | BNP PARIBAS                                         |
| 0051  | BANCO DAVIVIENDA S.A.                               |
| 0052  | BANCO AV VILLAS                                     |
| 0058  | BANCO PROCREDIT                                     |
| 0060  | BANCO PICHINCHA                                     |
| 0061  | BANCOOMEVA                                          |
| 0063  | BANCO FINANDINA                                     |
| 0065  | BANCO SANTANDER DE NEGOCIOS COLOMBIA SA             |
| 0066  | BANCO COOPERATIVO COOPCENTRAL                       |
| 0083  | COMPENSAR                                           |
| 0084  | GESTION CONTACTO                                    |
| 0086  | ASOPAGOS                                            |
| 0087  | FEDECAJAS                                           |
| 0088  | SIMPLE S.A                                          |
| 0089  | ENLACE OPERATIVO                                    |
| 0283  | COOPERTIVA FINANCIERA ANTIOQUIA                     |
| 0289  | COTRAFA COOPERATIVA FINANCIERA                      |
| 0292  | CONFIAR                                             |
| 0370  | COLTEFINANCIERA S.A                                 |
| 0550  | DECEVAL                                             |
| 0683  | DGCPTN                                              |
| 0685  | DGCPTN * Sistema General de Regalias                |
| 0121  | FINANCIERA JURISCOP S.A. Compañía de Financiamiento |
| 0064  | BANCO MULTIBANK S.A.                                |
| 0067  | BANCO COMPARTIR S.A.                                |
| 0062  | BANCO FALABELLA S.A.                                |
| 0342  | SERFINANSA S.A.                                     |

### Ecuador (EC)

#### Document Type

| Value | Description             |
|-------|-------------------------|
| 04    | DNI/Identification Card |

#### Account Type

| Value | Description      |
|-------|------------------|
| 0001  | Savings Bank     |
| 0002  | Checking Account |

#### Bank Name

| Value | Description                                        |
|-------|----------------------------------------------------|
| 0001  | BANCO AMAZONAS                                     |
| 0002  | BANCO BOLIVARIANO                                  |
| 0003  | BANCO CAPITAL                                      |
| 0004  | BANCO CENTRAL DEL ECUADOR                          |
| 0005  | BANCO CITY BANK                                    |
| 0006  | BANCO COFIEC                                       |
| 0007  | BANCO COOPNACIONAL SA                              |
| 0008  | BANCO D MIRO SA                                    |
| 0009  | BANCO DE FOMENTO                                   |
| 0010  | BANCO DE GUAYAQUIL S.A                             |
| 0011  | BANCO DE LA PRODUCCION                             |
| 0012  | BANCO DE LOJA                                      |
| 0013  | BANCO DEL AUSTRO                                   |
| 0014  | BANCO DEL INSTITU ECUATORIANO DE SEGURIDAD SOCIAL  |
| 0015  | BANCO DEL LITORAL S.A.                             |
| 0016  | BANCO DEL PACIFICO                                 |
| 0017  | BANCO DELBANK S.A.                                 |
| 0018  | BANCO ECUATORIANO DE LA VIVIENDA                   |
| 0019  | BANCO GENERAL RUMINAHUI S.A.                       |
| 0020  | BANCO INTERNACIONAL                                |
| 0021  | BANCO MACHALA                                      |
| 0022  | BANCO PARA LA ASISTENCIA COMUNITARIA FINCA S.A.    |
| 0023  | BANCO PICHINCHA C.A.                               |
| 0024  | BANCO PROCREDIT S.A.                               |
| 0025  | BANCO PROMERICA S.A.                               |
| 0026  | BANCO SOLIDARIO                                    |
| 0027  | BANCO SUDAMERICANO                                 |
| 0028  | C DE A Y C EMPLEAD BANCAR DEL ORO LTDA             |
| 0029  | C. A. Y C. INTERCULT. TARPUK RUNA LTDA.            |
| 0030  | C. DE A Y C 26 DE SEPTBRE LAZARO CONDO             |
| 0031  | C. DE A Y C 4 DE OCT. SAN FCO. DE CHAMBO           |
| 0032  | C. DE A Y C EDUCAD. DE ZAMORA CHINCHIPE            |
| 0033  | C. DE A Y C. EDUCADORES DE EL ORO LTD              |
| 0034  | C. DE A Y C. SAN MIGUEL DE PALLATANGA              |
| 0035  | C. DE A. Y C COOPAC AUSTRO LTDA (MIESS)            |
| 0036  | C. DE A. Y C. SAN MARTIN DE TISALEO LTDA.          |
| 0037  | C. DE AH. Y CREDITO LAS LAGUNAS (MIESS)            |
| 0038  | C.PEQ.EMPRESA DE PASTAZA                           |
| 0039  | CACPECO LTDA                                       |
| 0040  | CAJA DE A Y C JUVENTUD Y DESARROLLO                |
| 0041  | CAJA DE A Y C NUESTRA SENORA DE LA MERCED          |
| 0042  | CAJA DE AHORRO Y CREDITO EL INGENIO                |
| 0043  | CAJA DE AHORRO Y CREDITO EL MANIZAL                |
| 0044  | CAJA DE AHORRO Y CREDITO FRANCISCA CHIGUA          |
| 0045  | CAJA DE AHORRO Y CREDITO FRONTERA SUR              |
| 0046  | CAJA DE AHORRO Y CREDITO HORIZONTE FAMILIAR        |
| 0047  | CAJA DE AHORRO Y CREDITO MANU                      |
| 0048  | CAJA DE AHORRO Y CREDITO SAN FRANCISCO             |
| 0049  | CAJA DE AHORRO Y CREDITO ZHONDELEG                 |
| 0050  | CAJA SOLIDARIA DE A Y C CORDTUCH                   |
| 0051  | CAJA SOLIDARIA ESTRELLA DEL MUNDO                  |
| 0052  | CAMARA DE COMERCIO JOYA DE LOS SACHAS              |
| 0053  | COMERCIAL DE MANABI                                |
| 0054  | COOP A Y C 20 FEBRERO LTDA                         |
| 0055  | COOP A Y C CARROCEROS DE TUNGURAHUA                |
| 0056  | COOP A Y C ECUAFUTURO LTDA                         |
| 0057  | COOP A Y C ESC SUP POLITEC AGROP DE MANABI MANUEL  |
| 0058  | COOP A Y C FOCLA                                   |
| 0059  | COOP A Y C HUINARA LTDA                            |
| 0060  | COOP A Y C NUEVOS HORIZONTES EL ORO LTDA           |
| 0061  | COOP A Y C PROFESIONALES DEL VOLANTE UNION LTDA    |
| 0062  | COOP AHORRO Y CREDITO CAMARA COMERCIO DE AMBATO    |
| 0063  | COOP AHORRO Y CREDITO CARIAMANGA LTDA              |
| 0064  | COOP AHORRO Y CREDITO CONSTRC COMERCIO Y PRODUC    |
| 0065  | COOP AHORRO Y CREDITO DE LA PEQ EMP CACPE YANZATZA |
| 0066  | COOP AHORRO Y CREDITO FUNDESARROLLO                |
| 0067  | COOP AHORRO Y CREDITO MI TIERRA                    |
| 0068  | COOP AHORRO Y CREDITO MUSHUC RUNA LTDA             |
| 0069  | COOP AHORRO Y CREDITO PADRE JULIAN LORENTE LTDA    |
| 0070  | COOP AHORRO Y CREDITO PEQ EMPRESA GUALAQUIZA       |
| 0071  | COOP CACIQUE GURITAVE                              |
| 0072  | COOP CREDIUNION                                    |
| 0073  | COOP DE A Y C 16 DE JUNIO                          |
| 0074  | COOP DE A Y C 23 DE MAYO LTDA                      |
| 0075  | COOP DE A Y C ACCION TUNGURAHUA LTDA               |
| 0076  | COOP DE A Y C BANOS LTDA                           |
| 0077  | COOP DE A Y C CAMARA DE COMERICO GONZANAMA         |
| 0078  | COOP DE A Y C CASAG LTDA                           |
| 0079  | COOP DE A Y C CATAMAYO LTDA                        |
| 0080  | COOP DE A Y C COCA LTDA                            |
| 0081  | COOP DE A Y C CREDIAMIGO LTDA LOJA MIES            |
| 0082  | COOP DE A Y C CREDISUR LTDA                        |
| 0083  | COOP DE A Y C DE LA PEQ EMPRESA CACPE MACARA       |
| 0084  | COOP DE A Y C DE SERV PUBL DEL MIN EDUCACION Y CUL |
| 0085  | COOP DE A Y C DEL COL. FISC. VICENTE ROCAFUERTE    |
| 0086  | COOP DE A Y C DESARROLLO POPULAR                   |
| 0087  | COOP DE A Y C EDUCACIONES TULCAN LTDA              |
| 0088  | COOP DE A Y C EDUCADORES DE PASTAZA LTDA           |
| 0089  | COOP DE A Y C EDUCADORES TULCAN LTDA               |
| 0090  | COOP DE A Y C ESCENCIA INDIGENA LTDA               |
| 0091  | COOP DE A Y C FENIX                                |
| 0092  | COOP DE A Y C FINANCIERA INDIGENA LTDA             |
| 0093  | COOP DE A Y C FUTURO Y PROGRESO DE GALAPAGOS LTDA  |
| 0094  | COOP DE A Y C GENERAL RUMINAHUI                    |
| 0095  | COOP DE A Y C GONZANAMA MIES                       |
| 0096  | COOP DE A Y C INKA KIPU LTDA                       |
| 0097  | COOP DE A Y C JADAN LTDA (MIES)                    |
| 0098  | COOP DE A Y C LUCHA CAMPESINA LTDA                 |
| 0099  | COOP DE A Y C MAQUITA CUSHUN LTDA                  |
| 0100  | COOP DE A Y C MAQUITA CUSHUNCHIC LTDA              |
| 0101  | COOP DE A Y C MUSHUK YUYAY                         |
| 0102  | COOP DE A Y C PIJAL                                |
| 0103  | COOP DE A Y C SAN SANTIAGO DE MOLLETURO LTDA       |
| 0104  | COOP DE A Y C SANTA ROSA DE PAUTAN LTDA            |
| 0105  | COOP DE A Y C SIERRA CENTRO LTDA                   |
| 0106  | COOP DE A Y C SINCHI RUNA LTDA                     |
| 0107  | COOP DE A Y C SUMAC LLACTA LTDA                    |
| 0108  | COOP DE A Y C UNION MERCEDARIA LTDA                |
| 0109  | COOP DE A Y C VALLES DEL LIRIO                     |
| 0110  | COOP DE A Y C VENCEDORES DE TUNGURAHUA             |
| 0111  | COOP DE A Y C WUAMANLOMA                           |
| 0112  | COOP DE AHORRO Y CREDITO 22 DE JUNIO               |
| 0113  | COOP DE AHORRO Y CREDITO 23 DE ENERO               |
| 0114  | COOP DE AHORRO Y CREDITO 27 DE ABRIL LOJA          |
| 0115  | COOP DE AHORRO Y CREDITO 29 DE ENERO               |
| 0116  | COOP DE AHORRO Y CREDITO AGRICOLA JUNIN LTDA       |
| 0117  | COOP DE AHORRO Y CREDITO AMBATO LTDA               |
| 0118  | COOP DE AHORRO Y CREDITO ARTESANOS LTDA            |
| 0119  | COOP DE AHORRO Y CREDITO CAC-CICA MIES             |
| 0120  | COOP DE AHORRO Y CREDITO CACPE CELICA              |
| 0121  | COOP DE AHORRO Y CREDITO CUMBENITA LTDA            |
| 0122  | COOP DE AHORRO Y CREDITO DORADO LTDA               |
| 0123  | COOP DE AHORRO Y CREDITO ERCO LTDA                 |
| 0124  | COOP DE AHORRO Y CREDITO FASAYNAN LTDA             |
| 0125  | COOP DE AHORRO Y CREDITO FERNANDO DAQUILEMA        |
| 0126  | COOP DE AHORRO Y CREDITO FORTUNA MIES              |
| 0127  | COOP DE AHORRO Y CREDITO GUACHAPALA LTDA           |
| 0128  | COOP DE AHORRO Y CREDITO GUEL LTDA                 |
| 0129  | COOP DE AHORRO Y CREDITO HUAICANA LTDA             |
| 0130  | COOP DE AHORRO Y CREDITO HUAQUILLAS LTDA           |
| 0131  | COOP DE AHORRO Y CREDITO HUAYCO PUNGO LTDA         |
| 0132  | COOP DE AHORRO Y CREDITO INTEGRAL                  |
| 0133  | COOP DE AHORRO Y CREDITO LA FLORIDA                |
| 0134  | COOP DE AHORRO Y CREDITO LA MERCED                 |
| 0135  | COOP DE AHORRO Y CREDITO MARCABELI LTDA            |
| 0136  | COOP DE AHORRO Y CREDITO MIGRANTE SOLIDARIO        |
| 0137  | COOP DE AHORRO Y CREDITO NUESTROS ABUELOS LTDA     |
| 0138  | COOP DE AHORRO Y CREDITO NUEVA ESPERANZA           |
| 0139  | COOP DE AHORRO Y CREDITO NUEVA HUANCAVILCA         |
| 0140  | COOP DE AHORRO Y CREDITO PILAHUIN TIO LTDA         |
| 0141  | COOP DE AHORRO Y CREDITO POPULAR Y SOLIDARIA       |
| 0142  | COOP DE AHORRO Y CREDITO PUERTO LOPEZ LTDA         |
| 0143  | COOP DE AHORRO Y CREDITO QUILANGA LTDA             |
| 0144  | COOP DE AHORRO Y CREDITO SAN JORGE LTDA            |
| 0145  | COOP DE AHORRO Y CREDITO SAN JOSE EL AIRO          |
| 0146  | COOP DE AHORRO Y CREDITO SAN MIGUEL DE SIGCHOS     |
| 0147  | COOP DE AHORRO Y CREDITO SAN PEDRO DE TABOADA      |
| 0148  | COOP DE AHORRO Y CREDITO SANTA ANITA LTDA          |
| 0149  | COOP DE AHORRO Y CREDITO SIMIATUG LTDA             |
| 0150  | COOP DE LA PEQ Y MEDIANA EMPR CIUDADANA DE MACARA  |
| 0151  | COOP DE SERV MULTIPLES AGRO VIDA                   |
| 0152  | COOP ESFUERZO UNIDO PARA EL DESARR DEL CHILCO      |
| 0153  | COOP MANUEL ESTEBAN GODOY ORTEGA LTDA COOPMEGO     |
| 0154  | COOP OLMEDO                                        |
| 0155  | COOP SOLIDARIA DE GUALAQUIZA                       |
| 0156  | COOP SOLIDARIDAD Y PROGRESO ORIENTAL               |
| 0157  | COOP. 15 DE DICIEMBRE                              |
| 0158  | COOP. A. Y C. CAMARA DE COMERCIO DE PINDAL CADECOP |
| 0159  | COOP. A. Y C. DE LA PEQ. EMP. CACPE ZAMORA LTDA    |
| 0160  | COOP. AGUILAS DE CRISTO                            |
| 0161  | COOP. AHORRO Y CREDITO 15 DE ABRIL LTDA            |
| 0162  | COOP. AHORRO Y CREDITO 23 DE JULIO                 |
| 0163  | COOP. AHORRO Y CREDITO 29 DE OCTUBRE               |
| 0164  | COOP. AHORRO Y CREDITO 9 DE OCTUBRE LTDA           |
| 0165  | COOP. AHORRO Y CREDITO ACCION RURAL                |
| 0166  | COOP. AHORRO Y CREDITO ALIANZA MINAS LTDA.         |
| 0167  | COOP. AHORRO Y CREDITO AMAZONAS LTDA.              |
| 0168  | COOP. AHORRO Y CREDITO ANDALUCIA                   |
| 0169  | COOP. AHORRO Y CREDITO COTOCOLLAO                  |
| 0170  | COOP. AHORRO Y CREDITO D LA PEQ EMPR CACPE BIBLIAN |
| 0171  | COOP. AHORRO Y CREDITO DE LA PEQUENA EMPRESA GUALA |
| 0172  | COOP. AHORRO Y CREDITO DESARROLLO PUEBLOS          |
| 0173  | COOP. AHORRO Y CREDITO EL SAGRARIO                 |
| 0174  | COOP. AHORRO Y CREDITO FAMILIA AUSTRAL             |
| 0175  | COOP. AHORRO Y CREDITO GUARANDA LTDA               |
| 0176  | COOP. AHORRO Y CREDITO JUAN DE SALINAS LTDA.       |
| 0177  | COOP. AHORRO Y CREDITO JUVENTUD                    |
| 0178  | COOP. AHORRO Y CREDITO LOS RIOS                    |
| 0179  | COOP. AHORRO Y CREDITO MALCHINGUI LTDA.            |
| 0180  | COOP. AHORRO Y CREDITO MANANTIAL DE ORO LTDA.      |
| 0181  | COOP. AHORRO Y CREDITO MANUEL                      |
| 0182  | COOP. AHORRO Y CREDITO NUEVA JERUSALEN             |
| 0183  | COOP. AHORRO Y CREDITO OSCUS                       |
| 0184  | COOP. AHORRO Y CREDITO PABLO MUNOZ VEGA            |
| 0185  | COOP. AHORRO Y CREDITO PROGRESO                    |
| 0186  | COOP. AHORRO Y CREDITO PUELLARO LTDA               |
| 0187  | COOP. AHORRO Y CREDITO RIOBAMBA                    |
| 0188  | COOP. AHORRO Y CREDITO SAN FRANCISCO               |
| 0189  | COOP. AHORRO Y CREDITO SAN GABRIEL LTDA.           |
| 0190  | COOP. AHORRO Y CREDITO SAN JOSE LTDA               |
| 0191  | COOP. AHORRO Y CREDITO SAN MIGUEL DE LOS BANCOS    |
| 0192  | COOP. AHORRO Y CREDITO SEMILLA DEL PROGRESO LTDA   |
| 0193  | COOP. AHORRO Y CREDITO SENOR DE GIRON              |
| 0194  | COOP. AHORRO Y CREDITO TENA LTDA.                  |
| 0195  | COOP. AHORRO Y CREDITO TULCAN                      |
| 0196  | COOP. AHORRO. Y CREDI. MUJERES UNIDAS TANTANAKUSHK |
| 0197  | COOP. CALCETA LTDA                                 |
| 0198  | COOP. CREDITO Y AHORRO SAN FRANCISCO DE ASIS       |
| 0199  | COOP. DE A Y C. SERVIDORES MUNICIPALES DE CUENCA   |
| 0200  | COOP. DE A. Y C. 13 DE ABRIL LTDA                  |
| 0201  | COOP. DE A. Y C. ALLI TARPUC LTDA.                 |
| 0202  | COOP. DE A. Y C. CHIBULEO LTDA.                    |
| 0203  | COOP. DE A. Y C. COOPINDIGENA LTDA.                |
| 0204  | COOP. DE A. Y C. DESARROLLO INTEGRAL LTDA          |
| 0205  | COOP. DE A. Y C. EL TESORO PILLARENO               |
| 0206  | COOP. DE A. Y C. EL TRANSPORTISTA CACET            |
| 0207  | COOP. DE A. Y C. GRAMEEN AMAZONAS                  |
| 0208  | COOP. DE A. Y C. ILINIZA LTDA.                     |
| 0209  | COOP. DE A. Y C. INDIGENA ALFA Y OMEGA LTDA        |
| 0210  | COOP. DE A. Y C. JUAN PIO DE MORA LTDA             |
| 0211  | COOP. DE A. Y C. JUVENTUD UNIDA LTDA.              |
| 0212  | COOP. DE A. Y C. KISAPINCHA LTDA.                  |
| 0213  | COOP. DE A. Y C. LA UNION LTDA.                    |
| 0214  | COOP. DE A. Y C. LOS CHASQUIS PASTOCALLE LTDA.     |
| 0215  | COOP. DE A. Y C. MUSHUG CAUSAY LTDA.               |
| 0216  | COOP. DE A. Y C. PADRE VICENTE PONCE RUBIO         |
| 0217  | COOP. DE A. Y C. SALASACA                          |
| 0218  | COOP. DE A. Y C. SALINAS LTDA.                     |
| 0219  | COOP. DE A. Y C. SAN PEDRO LTDA.                   |
| 0220  | COOP. DE A. Y C. SUMAK SAMY LTDA.                  |
| 0221  | COOP. DE A. Y C. UNION QUISAPINCHA LTDA.           |
| 0222  | COOP. DE A. Y C. VIRGEN DEL CISNE                  |
| 0223  | COOP. DE AHO Y CRED LOS ANDES LATINOS LTDA.        |
| 0224  | COOP. DE AHORRO Y CRED. SANTA ROSA LTDA            |
| 0225  | COOP. DE AHORRO Y CREDITO 4 DE OCTUBRE LTDA.       |
| 0226  | COOP. DE AHORRO Y CREDITO ACCION Y DESARROLLO LTDA |
| 0227  | COOP. DE AHORRO Y CREDITO ANDINA LTDA.             |
| 0228  | COOP. DE AHORRO Y CREDITO ATUNTAQUI LTDA.          |
| 0229  | COOP. DE AHORRO Y CREDITO COMERCIO LTDA PORTOVIEJO |
| 0230  | COOP. DE AHORRO Y CREDITO COOPERA LTDA.            |
| 0231  | COOP. DE AHORRO Y CREDITO CRISTO REY               |
| 0232  | COOP. DE AHORRO Y CREDITO EDUCADORES DE CHIMBORAZO |
| 0233  | COOP. DE AHORRO Y CREDITO EL CALVARIO LTDA         |
| 0234  | COOP. DE AHORRO Y CREDITO GUARUMAL DEL CENTRO LTDA |
| 0235  | COOP. DE AHORRO Y CREDITO LA DOLOROSA LTDA         |
| 0236  | COOP. DE AHORRO Y CREDITO ONCE DE JUNIO            |
| 0237  | COOP. DE AHORRO Y CREDITO PEDRO MONCAYO LTDA.      |
| 0238  | COOP. DE AHORRO Y CREDITO PILAHUIN                 |
| 0239  | COOP. DE AHORRO Y CREDITO PROFUTURO LTDA.          |
| 0240  | COOP. DE AHORRO Y CREDITO PUCARA LTDA              |
| 0241  | COOP. DE AHORRO Y CREDITO SARAGUROS                |
| 0242  | COOP. DE LA MICROEMP. DE CHIMBORAZO                |
| 0243  | COOP. JARDIN AZUAYO                                |
| 0244  | COOP. PREVISION AHORRO Y DESARROLLO                |
| 0245  | COOP. PROD. Y DES. AGR. COOPRODESA LTDA            |
| 0246  | COOP. SAN PABLO                                    |
| 0247  | COOP.AHO Y CREDITO DE LA PEQ. EMP. DE LOJA CACPE   |
| 0248  | COOP.AHORRO Y CREDITO ALIANZA DEL VALLE LTDA       |
| 0249  | COOP.AHORRO Y CREDITO CHONE LTDA                   |
| 0250  | COOP.AHORRO Y CREDITO PRIMERO DE ENERO DEL AUSTRO  |
| 0251  | COOP.DE AHORRO Y CREDITO POLICIA NACIONAL          |
| 0252  | COOPERATIVA 15 DE AGOSTO PILACOTO                  |
| 0253  | COOPERATIVA DE AH. Y CREDITO RIOCHICO              |
| 0254  | COOPERATIVA DE AHORRO Y CREDITO ALFONSO JARAMILLO  |
| 0255  | COOPERATIVA DE AHORRO Y CREDITO CASA FACIL LTDA.   |
| 0256  | COOPERATIVA DE AHORRO Y CREDITO CREA LTDA ( MIES)  |
| 0257  | COOPERATIVA DE AHORRO Y CREDITO INTI WASI LTDA.    |
| 0258  | COOPERATIVA DE AHORRO Y CREDITO LLANGANATES        |
| 0259  | COOPERATIVA DE AHORRO Y CREDITO MINGA LTDA.        |
| 0260  | COOPERATIVA DE AHORRO Y CREDITO PROVIDA            |
| 0261  | COOPERATIVA DE AHORRO Y CREDITO SAN ISIDRO LTDA.   |
| 0262  | COOPERATIVA DE AHORRO Y CREDITO SAN JOSE S.J.      |
| 0263  | COOPERATIVA DE AHORRO Y CREDITO SANTA ANA LTDA     |
| 0264  | CORP. DE DES. SOCIAL Y FINANC ISLAS ENCANTADAS     |
| 0265  | CORPORACION DE DESARROLLO FINANCIERA RHUMY WARA    |
| 0266  | CORPORACION EN LAS HUELLAS DEL BCO GRAMEEN         |
| 0267  | CORPORACION VIENTOS SOLIDARIOS                     |
| 0268  | DE AHORRO Y CREDITO CRECIENDO JUNTOS               |
| 0269  | DE AHORRO Y CREDITO FCO. DE ORELLANA               |
| 0270  | FINANCIERA - DINERS CLUB DEL ECUADOR               |
| 0271  | FINANCIERA CONSULCREDITOS SA                       |
| 0272  | FINANCOOP                                          |
| 0273  | FONDO DE CESANTIA DEL MAGISTERIO ECUAT FCME-FCPC   |
| 0274  | INTERDIN S.A.                                      |
| 0275  | MUTUALISTA AMBATO                                  |
| 0276  | MUTUALISTA AZUAY                                   |
| 0277  | MUTUALISTA IMBABURA                                |
| 0278  | MUTUALISTA PICHINCHA                               |
| 0279  | VAZCORP SOCIEDAD FINANCIERA S.A.                   |

### Peru (PE)

#### Document Type

| Value | Description             |
|-------|-------------------------|
| 04    | DNI/Identification Card |

#### Account Type

| Value | Description      |
|-------|------------------|
| 0001  | Savings Bank     |
| 0002  | Checking Account |

#### Bank Name

| Value | Description                              |
|-------|------------------------------------------|
| 0001  | BANCO INTERNACIONAL DEL PERU (INTERBANK) |
| 0002  | BANCO BBVA PERU                          |
| 0003  | BANCO BCP PERU                           |
| 0004  | BANCO SCOTIABANK PERU                    |
| 0005  | BANCO INTERAMERICANO DE FINANZAS         |

## Test Information

It is not possible to test the whole payment flow in the test environment since the payment is not processed automatically by the provider and will remain in PENDING state. The provider can simulate an APPROVED callback notification but it will not complete the payment since PaymentIQ will call the status check API which will still return the PENDING state, thus keeping it in the PIQ state WAITING_INPUT.

This means that the whole payment flow can only be tested in the production environment.

### Deposit

**Note**: Certain countries require a NationalID, also known as CPF or RUT. If testing in "mock mode" in PIQ, the test user should have "nationalIdentificationNumber" as an attribute configured with the CPF/RUT value. If you as a merchant is testing with "integration mode", i.e real API calls to your own server, then your user has to have the "nationalIdentificationNumber" attribute in the verifyuser response to PIQ. If this is not provided you will be prompted to add this on PayRetailer's end.

Available NationalId values
- CPF: 86758181650
- RUT: 184466848

Mock User example (only for the experienced PaymentIQ user)

```xml
<com.devcode.paymentiq.integration.merchant.mock.MockUser>
  <userId>PR_CLP</userId>
  . . .
  <country>CHILE</country>
  <locale>en_US</locale>
  <balance>9986909.20 USD</balance>
  <attributes>
    <entry>
      <string>nationalIdentificationNumber</string>
      <string>184466848</string>
    </entry>
  </attributes>
  <notFound>false</notFound>
</com.devcode.paymentiq.integration.merchant.mock.MockUser>  
```

#### Using Paywall

After the deposit process is initiated the end-user will be redirected to PayRetailer's page displaying the available payment options.

![](/img/providers/payretailers_deposit_01.png)

Select the payment option you want to test and follow the instructions in the window to complete the payment. Once the payment is ACCEPTED you will be redirected to checkout page.

![](/img/providers/payretailers_deposit_02.png)

**Note: For some banks the user will have to close the checkout page manually since PayRetailers don't send a real "redirect" notification after the payment reached its final state of APPROVED, EXPIRED, or ERROR.**

It will take some time to process the payment (depending on the selected payment option) and after it's done, PayRetailers will send a final notification with final payment status.

#### Using direct transaction

The flow is identical to the paywall flow, except that the end-user will not be able to select the payment method on PayRetailers' page, and instead will be redirected to the selected payment method directly.

### Withdrawal

#### Parameters Format

**Brazil**<br/>

| Parameter             | Format     | Length |
|-----------------------|------------|--------|
| Document Number       | [A-Z][0-9] | 11     |
| Account Agency Number | [A-Z][0-9] | 6*     |
| Account Number        | [A-Z][0-9] | 13     |

**Chile**<br/>

| Parameter       | Format     | Length |
|-----------------|------------|--------|
| Document Number | [A-Z][0-9] | 9      |
| Account Number  | [A-Z][0-9] | 16     |

**Mexico**<br/>

| Parameter       | Format                                                          | Length |
|-----------------|-----------------------------------------------------------------|--------|
| Document Number | [A-Z][0-9]                                                      | 18     |
| Account Number  | [0-9]In this field you should provide the "CLABE Interbancaria" | 18     |

**Colombia**<br/>

| Parameter       | Format | Length |
|-----------------|--------|--------|
| Document Number | [0-9]  | 6-10   |
| Account Number  | [0-9]  | 16*    |

**Ecuador**<br/>

| Parameter       | Format | Length |
|-----------------|--------|--------|
| Document Number | [0-9]  | 10     |
| Account Number  | [0-9]  | 12     |

**Peru**<br/>

| Parameter       | Format | Length                                                                                                                                                                                                                  |
|-----------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Document Number | [0-9]  | 8                                                                                                                                                                                                                       |
| Account Number  | [0-9]  | Bank Account Number types will vary by bank between Cuenta Corriente Interbancaria (CCI - 20 digits) and Cuenta Bancaria (CB, normal bank account number, which varies length based on bank). See API doc for more info |

**Note**<br/>
- "Account Agency Number" is a required parameter for Brazil only (for other countries it can be left blank).<br/>This parameter is deprecated now for  `PayRetailersWithdrawal` tx type, and will be removed in the future. Due to this, it is recommended to use `PixWithdrawal` for PIX payout in Brazil and `PayRetailersWithdrawal` - for all other payout options.
- (*) Maybe less numbers depends on bank

To initiate a withdrawal the end-user should specify all the required parameters (e.g. see this BRL example from our cashier)

![](/img/providers/payretailers_withdrawal_01.png)

### PIX Withdrawal (Brazil)

You can use either `PayRetailersWithdrawal` tx type with `service=PIX` or `PixWithdrawal` (recommended) tx type to initiate a PIX withdrawal (see `PixWithdrawal` usage below).

![](/img/providers/payretailers_withrawal_pix.png)

To initiate a PIX withdrawal in Brazil the end-user should also specify Recipient Pix Key. This parameter will vary in value depending on the customer's PIX key, which can be one of the following:<br/>

- Phone Number
- E-mail
- Random Key
- CPF
