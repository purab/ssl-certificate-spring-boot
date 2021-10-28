# SSL certificate integration
SSL certificate setting applied in application.properties file To generate self signed SSL certificate use following command:

```
cd src/main/resources
keytool -genkeypair -alias local_ssl -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore local-ssl.p12 -validity 365 -ext san=dns:localhost
```

Put following code into application.properties file
```
spring.application.name=ssl-certificate
server.port=8443
#server.port=8080
server.ssl.enabled: true
server.ssl.key-alias: local_ssl
server.ssl.key-store: classpath:local-ssl.p12
server.ssl.key-store-type: PKCS12
server.ssl.key-password: 12345678
server.ssl.key-store-password: 12345678
```

Open this URL:
https://localhost:8443/

For production use following command and use p12 file in application Convert .crt to .p12
```
openssl pkcs12 -export -out server.p12 -inkey server.key -in server.crt
```
Where server.key , is the server key . server.crt is cert file from CA or self sign
