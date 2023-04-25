---
id: "ccresponsecodes"
---

# General scheme response codes
Here’s a list of general response codes you might see from different schemes and acquires. Please note that this is not a complete list nor will it be definitive as it's up to the issuing bank and acquirers to classify and interpolate. We've tried to add explanations and descriptions to guide to understand when you might see the different responses.


|	Response Code	|	Scheme	|	Description	|	Explanation	|
|	--------	|	--------	|	--------	|	--------	|
|	00	|	Mastercard	|	Approved or completed	|		|
|	00	|	Unionpay	|	Approved or completed	|		|
|	00	|	Visa	|	Approved or completed	|		|
|	01	|	Mastercard	|	Refer to card issuer Call Issuer	|		|
|	01	|	Unionpay	|	Refer to card issuer Call Issuer	|		|
|	01	|	Visa	|	Refer to card issuer Call Issuer (not valid for an issuer to use anymore)	|		|
|	02	|	Visa	|	Refer to card issuer Call Issuer (not valid for an issuer to use anymore)	|		|
|	03	|	Mastercard	|	Invalid merchant	|		|
|	03	|	Unionpay	|	Invalid merchant 	|		|
|	03	|	Visa	|	Invalid merchant	|		|
|	04	|	Mastercard	|	Capture card	|	Fraud	|
|	04	|	Unionpay	|	Capture card 	|	Fraud	|
|	04	|	Visa	|	Capture card	|	Fraud	|
|	05	|	Mastercard	|	Do not honor	|		|
|	05	|	Unionpay	|	ID certificationfails	|		|
|	05	|	Visa	|	Do not honor	|		|
|	06	|	Visa	|	Error	|		|
|	07	|	Visa	|	Capture Card	|	Fraud	|
|	08	|	Mastercard	|	Honor with ID	|		|
|	10	|	Mastercard	|	Partial Approval	|		|
|	10	|	Unionpay	|	Partial Approval 	|		|
|	10	|	Visa	|	Partial Approval	|		|
|	11	|	Unionpay	|	VIP (Approved)	|		|
|	11	|	Visa	|	Veas approval	|		|
|	12	|	Mastercard	|	Invalid transaction	|	Card doesnt support recurring payments. (pre-paid cards)	|
|	12	|	Unionpay	|	Invalid related transaction	|	Card doesnt support recurring payments. (pre-paid cards)	|
|	12	|	Visa	|	Invalid transaction	|	Card doesnt support recurring payments. (pre-paid cards)	|
|	13	|	Mastercard	|	Invalid amount	|		|
|	13	|	Unionpay	|	Invalid amount	|		|
|	13	|	Visa	|	Invalid amount	|		|
|	14	|	Mastercard	|	Invalid card number	|	User typed wrong number / No such card	|
|	14	|	Unionpay	|	Invalid cardnumber	|	User typed wrong number / No such card	|
|	14	|	Visa	|	Invalid account number	|	User typed wrong number / No such card	|
|	15	|	Mastercard	|	Invalid issuer	|	Scheme not supported / wrong cardnumber & Test Cards in used in wrong environment	|
|	15	|	Unionpay	|	No such Issuers	|	Scheme not supported / wrong cardnumber & Test Cards in used in wrong environment	|
|	15	|	Visa	|	No such issuer	|		|
|	16	|	Unionpay	|	Approved to update track3 (approved)	|		|
|	19	|	Visa	|	Re-enter transaction	|		|
|	21	|	Unionpay	|	Card not initialized	|		|
|	21	|	Visa	|	No action taken, unable to back out prior transaction	|		|
|	22	|	Unionpay	|	Suspected malfunction; related transaction error	|	System error / Provider error	|
|	25	|	Unionpay	|	Unable to locate original transaction	|	System error / Provider error	|
|	25	|	Visa	|	Unable to locate record in file, or Account number missing from inquiry	|	System error / Provider error	|
|	25	|	Mastercard	|	Unable to locate record in file, or Account number missing from inquiry	|		|
|	28	|	Visa	|	File is temporarily unavailable 	|		|
|	30	|	Mastercard	|	Format error	|		|
|	30	|	Unionpay	|	Format Error	|		|
|	34	|	Unionpay	|	Fraud	|	Fraud	|
|	38	|	Unionpay	|	PIN try limit exceeded	|		|
|	39	|	Visa	|	No credit account	|		|
|	40	|	Unionpay	|	Function requested not supported	|	Account Verification not supported by Unionpay	|
|	41	|	Mastercard	|	Lost card	|	Fraud	|
|	41	|	Unionpay	|	Lost Card	|	Fraud	|
|	41	|	Visa	|	Pick-up card, lost card	|	Fraud	|
|	43	|	Mastercard	|	Stolen card	|	Fraud	|
|	43	|	Unionpay	|	Stolen Card	|	Fraud	|
|	43	|	Visa	|	Pick-up card, stolen card	|	Fraud	|
|	45	|	Unionpay	|	Fallback transaction is not allowed	|		|
|	51	|	Mastercard	|	Insufficient funds/over credit limit	|	No Funds	|
|	51	|	Unionpay	|	Insufficientbalance	|	No Funds	|
|	51	|	Visa	|	Insufficient funds	|	No Funds	|
|	52	|	Visa	|	No current account	|		|
|	53	|	Visa	|	No savings account	|		|
|	54	|	Mastercard	|	Expired card	|		|
|	54	|	Unionpay	|	Expired Card	|		|
|	54	|	Visa	|	Expired card	|		|
|	55	|	Mastercard	|	Invalid PIN	|		|
|	55	|	Unionpay	|	Incorrect personal identification number	|		|
|	55	|	Visa	|	Incorrect PIN 	|		|
|	57	|	Mastercard	|	Transaction not permitted to issuer/cardholder	|	Card restrictions	|
|	57	|	Unionpay	|	Transaction not allowed to be processed by cardholder 	|	Card restrictions	|
|	57	|	Visa	|	Transaction not permitted to Cardholder 	|	Card restrictions	|
|	58	|	Mastercard	|	Transaction not permitted to acquirer/terminal	|		|
|	58	|	Unionpay	|	Transaction not allowed to be processed by terminal	|		|
|	58	|	Visa	|	Transaction not allowed at terminal 	|		|
|	59	|	Unionpay	|	Suspected fraud	|	Fraud	|
|	59	|	Visa	|	Suspected fraud	|	Fraud	|
|	61	|	Mastercard	|	Exceeds withdrawal amount limit	|	No Funds	|
|	61	|	Unionpay	|	Transaction amount limit exceeded	|	No Funds	|
|	61	|	Visa	|	Activity amount limit exceeded 	|	No Funds	|
|	62	|	Mastercard	|	Restricted card	|	Card restrictions	|
|	62	|	Unionpay	|	Restricted card	|	Card restrictions	|
|	62	|	Visa	|	Restricted card, for example, listed in Country Exclusion table	|	Card restrictions	|
|	63	|	Mastercard	|	Security violation	|		|
|	63	|	Visa	|	Security violation 	|		|
|	64	|	Unionpay	|	Original transaction amount error	|		|
|	64	|	Visa	|	Transaction does not fulfil AML requirement 	|		|
|	65	|	Mastercard	|	Exceeds withdrawal count limit	|		|
|	65	|	Unionpay	|	Exceeds withdrawal velocity limit	|		|
|	65	|	Visa	|	Activity count limit exceeded 	|		|
|	68	|	Unionpay	|	Issuer response Timeout	|		|
|	70	|	Mastercard	|	Contact Card Issuer	|		|
|	71	|	Mastercard	|	PIN Not Changed	|		|
|	75	|	Mastercard	|	Allowable number of PIN tries exceeded	|		|
|	75	|	Unionpay	|	Allowablen umber of PIN tries exceeded	|		|
|	75	|	Visa	|	Allowable number of PIN entry tries exceeded	|		|
|	76	|	Mastercard	|	Invalid/nonexistent “To Account” specified	|		|
|	76	|	Visa	|	Unable to locate previous message, no match on Retrieval Reference number 	|		|
|	77	|	Mastercard	|	Invalid/nonexistent “From Account” specified	|		|
|	77	|	Visa	|	Previous message located for a repeat or reversal, but repeat or reversal data is inconsistent with	|		|
|	78	|	Mastercard	|	Invalid/nonexistent account specified (general)	|		|
|	78	|	Visa	|	‘Blocked, first used’, the transaction is from a new Cardholder, and the card has not been properly	|		|
|	79	|	Visa	|	Transaction already reversed 	|		|
|	80	|	Visa	|	Visa transaction, credit Issuer unavailable, or Private label transaction, invalid date 	|		|
|	81	|	Mastercard	|	Domestic Debit Transaction Not Allowed (Regional use only)	|		|
|	81	|	Mastercard	|	Domestic Debit Transaction Not Allowed (Regional use only)	|		|
|	81	|	Visa	|	PIN cryptographic error found, error found by VIC security module during PIN decryption 	|		|
|	82	|	Visa	|	Negative online CAM, dCVV, iCVV, or CVV results, or Offline PIN authentication was interrupted 	|		|
|	84	|	Mastercard	|	Invalid Authorization Life Cycle	|		|
|	85	|	Mastercard	|	Not declined (Valid for all zero amount transactions)	|	Successful transaction if Account Verification. Used for Zero Amount transactions	|
|	85	|	Visa	|	No reason to decline	|	Successful transaction if Account Verification. Used for Zero Amount transactions	|
|	86	|	Mastercard	|	PIN Validation not possible Decline	|		|
|	86	|	Visa	|	Cannot verify PIN	|		|
|	87	|	Mastercard	|	Purchase Amount Only, No Cash Back Allowed	|		|
|	88	|	Mastercard	|	Cryptographic failure	|		|
|	89	|	Mastercard	|	Unacceptable PIN - Transaction Declined	|		|
|	90	|	Unionpay	|	Cut-off in progress	|		|
|	91	|	Mastercard	|	Authorization System or issuer system inoperative	|		|
|	91	|	Unionpay	|	Issuer not capable to process	|	Provider Error	|
|	91	|	Visa	|	Issuer unavailable	|	Provider Error	|
|	92	|	Mastercard	|	Unable to route transaction	|	Provider Error	|
|	92	|	Unionpay	|	Financial institution or intermediate network facility cannot be found for routing	|		|
|	92	|	Visa	|	Routing not found	|		|
|	93	|	Visa	|	Transaction cannot be completed, violation of law.	|		|
|	94	|	Mastercard	|	Duplicate transmission detected	|		|
|	94	|	Unionpay	|	Duplicated transaction	|		|
|	94	|	Visa	|	Duplicate transaction 	|		|
|	96	|	Mastercard	|	System error Decline	|	System error / Provider error	|
|	96	|	Unionpay	|	Switch system malfunction	|	System error / Provider error	|
|	96	|	Visa	|	System malfunction	|	System error / Provider error	|
|	97	|	Unionpay	|	ATM/POS terminal number cannot be located	|		|
|	98	|	Unionpay	|	Issuer response not received by CUPS	|		|
|	99	|	Unionpay	|	PIN Block Error	|		|
|	A0	|	Unionpay	|	MAC failed	|		|
|	A2	|	Unionpay	|	Successful transaction with fault (Approved)	|		|
|	A3	|	Unionpay	|	Account not found in Transfer-inside	|		|
|	A4	|	Unionpay	|	Successful transaction with fault (Approved)	|		|
|	A5	|	Unionpay	|	Successful transaction with fault (Approved)	|		|
|	A6	|	Unionpay	|	Successful transaction with fault (Approved)	|		|
|	A7	|	Unionpay	|	Security processing failure	|		|
|	B1	|	Unionpay	|	No arrears (transaction receipt not printed)	|		|
|	B1	|	Visa	|	Surcharge amount not permitted on Visa cards US Acquirers only 	|		|
|	C1	|	Unionpay	|	Illegal Status of Acquirer	|		|
|	D1	|	Unionpay	|	Incorrect IIN	|		|
|	D2	|	Unionpay	|	Date Error	|		|
|	D3	|	Unionpay	|	Invalid file type	|		|
|	D4	|	Unionpay	|	File processed	|		|
|	D5	|	Unionpay	|	No such file	|		|
|	D6	|	Unionpay	|	Not supported by Receiver	|		|
|	D7	|	Unionpay	|	File locked	|		|
|	D8	|	Unionpay	|	Unsuccessful	|		|
|	D9	|	Unionpay	|	Incorrect file length	|		|
|	DA	|	Unionpay	|	File decompression error	|		|
|	DB	|	Unionpay	|	Filename error	|		|
|	DC	|	Unionpay	|	File cannot be received	|		|
|	F1	|	Unionpay	|	File record format error	|		|
|	F2	|	Unionpay	|	File record repeated	|		|
|	F3	|	Unionpay	|	File record not existing	|		|
|	F4	|	Unionpay	|	File record error	|		|
|	N0	|	Visa	|	Force STIP	|		|
|	N1	|	Unionpay	|	Items not on Bankbook beyond limit, declined	|		|
|	N3	|	Visa	|	Cash service not available	|		|
|	N4	|	Visa	|	Cash back request exceeds Issuer limit	|		|
|	N7	|	Visa	|	Decline for CVV2 failure	|		|
|	N8	|	Visa	|	Transaction amount exceeds preauthorized approval amount 	|		|
|	P2	|	Visa	|	Invalid biller information	|		|
|	P5	|	Visa	|	PIN change/unblock request declined	|		|
|	P6	|	Visa	|	Unsafe PIN	|		|
|	Q1	|	Visa	|	Card authentication failed, or Offline PIN authentication interrupted 	|		|
|	R0	|	Visa	|	Stop payment order	|		|
|	R1	|	Visa	|	Revocation of authorization order. Issuers receive an advice each time a transaction is stopped in VE	|		|
|	R3	|	Visa	|	Revocation of all authorizations order. Issuers receive an advice each time a transaction is stopped 	|		|
|	Y1	|	Unionpay	|	The offline transaction is successful (only used for IC cards based on UICS debit/credit standard. 	|		|
|	Y3	|	Unionpay	|	It is unable to be online. The offline transaction is successful (only used for IC cards based on U	|		|
|	Z1	|	Unionpay	|	The offline transaction fails (only used for IC cards based on UICS debit/credit standard. 	|		|
|	Z3	|	Unionpay	|	It is unable to be online. The offline transaction fails (only used for IC cards based on UICS debit	|		|
