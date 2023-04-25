---
id: "testcards3dsv2"
---

# 3DS2 Test Cards For Staging Environment

:::info

In order to begin testing you will need to make sure all additional required parameters are submitted properly via the APIs

:::

# Clearhaus 3DS Server

Test card for Clearhaus: `4111111111111111`. Any CVC and future expiry date can be used. Can be routed to any PSP that can handle this card in test.

| Amount          | Scenario               |
|-----------------|------------------------|
| 200.01          | Frictionless success   |
| 200.02          | Frictionless reject    |
| 200.03          | Frictionless attempt   |
| 200.04          | Auto challenge success |
| 200.05          | Auto challenge reject  |
| Everything else | Challenge              |

# Ingenico 3DS Server

| Provider        | Card                                                                                                         |
|-----------------|--------------------------------------------------------------------------------------------------------------|
| BamboraGa       | **PAN:** 5574788643393809 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Frictionless         |
| BamboraGa       | **PAN:** 5457210002001420 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Challenge            |
| BamboraGa       | **PAN:** 5200000000000106 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| BamboraGa       | **PAN:** 4186455175836497 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| BamboraGa       | **PAN:** 4874970686672022 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| Credorax        | **PAN:** 5223450000000007 <br/>**CVC:** 090 <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| Credorax        | **PAN:** 5223450000000015 <br/>**CVC:** 090 <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| WorldPay        | **PAN:** 5555555555554444 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| WorldPay        | **PAN:** 4444333322221111 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| Payvision       | **PAN:** 4000000000000002 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| Payvision       | **PAN:** 5200000000000106 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| Ogone           | **PAN:** 4186455175836497 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| Ogone           | **PAN:** 4874970686672022 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| Realex          | **PAN:** 4263970000005262 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| Realex          | **PAN:** 4012001038488884 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| SafeCharge      | **PAN:** 4000023104662535 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| SafeCharge      | **PAN:** 4000027891380961 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| WirecardElastic | **PAN:** 5413330300201184 <br/>**CVC:** 184 <br/> **Exp date:** 01/2023 <br/> **Type:** Frictionless         |
| WirecardElastic | **PAN:** 5413330300201002 <br/>**CVC:** 002 <br/> **Exp date:** 01/2023 <br/> **Type:** Challenge            |
| PowerPay21      | **PAN:** 5574788643393809 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Frictionless         |
| PowerPay21      | **PAN:** 5457210002001420 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Challenge            |
| PowerPay21      | **PAN:** 5200000000000106 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| PowerPay21      | **PAN:** 4186455175836497 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| PowerPay21      | **PAN:** 4874970686672022 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| ECommPay        | **PAN:** 5574788643393809 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Frictionless         |
| ECommPay        | **PAN:** 5457210002001420 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Challenge            |
| ECommPay        | **PAN:** 5200000000000106 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| ECommPay        | **PAN:** 4186455175836497 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| ECommPay        | **PAN:** 4874970686672022 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| SecureTrading   | **PAN:** 5574788643393809 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Frictionless         |
| SecureTrading   | **PAN:** 5457210002001420 <br/>**CVC:** Any <br/> **Exp date:** 12/2025 <br/> **Type:** Challenge            |
| SecureTrading   | **PAN:** 5200000000000106 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |
| SecureTrading   | **PAN:** 4186455175836497 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless |
| SecureTrading   | **PAN:** 4874970686672022 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge    |

# Credorax 3DS Server

| Provider | Card                                                                                                                   |
|----------|------------------------------------------------------------------------------------------------------------------------|
| Credorax | **PAN:** 5185520050000010 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Frictionless           |
| Credorax | **PAN:** 5299910010000015 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge (Y) OTP=4445 |
| Credorax | **PAN:** 5455330200000016 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge (R) OTP=9999 |
| Credorax | **PAN:** 5455330200000099 <br/>**CVC:** Any <br/> **Exp date:** Any future date <br/> **Type:** Challenge (A) OTP=4444 |

Check [this link](https://docs.google.com/document/d/1LTlAbR6ERsM-Y1DqO_HkaOod8D4ieBrvmHNUpnSF99M/edit) for an updated list of all Credorax test cards.


# Safecharge 3DS Server

| Card             | Card name  | Amount | Scenario     |
|------------------|------------|--------|--------------|
| 4000020951595032 | FL-BRW1    | 150    | Frictionless |
| 2221008123677736 | CL-BRW2    | 151    | Challenge    |
| 4407106439671112 | John Smith | 152    | Fallback     |
| 4000027891380961 | John Smith | 10     | non-3D       |