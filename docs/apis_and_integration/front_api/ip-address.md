---
id: "ip-address"
---

# End user IP address

For better traceability and for security reasons the end user's IP address can be sent to PaymentIQ, in order for it to be logged for each transaction. This is also the IP that will be sent to the PSP when doing a payment. The IP address can be sent in one of following HTTP headers:

1. PIQ-Client-IP
2. X-Forwarded-For
3. Z-Forwarded-For
4. Proxy-Client-IP
5. WL-Proxy-Client-IP
6. HTTP_CLIENT_IP
7. HTTP_X_FORWARDED_FOR

The headers will be checked from the top to bottom. If none of the headers exist, PIQ will take the IP address of the HTTP request.

**Note: Some PSPs do not support IPv6**
