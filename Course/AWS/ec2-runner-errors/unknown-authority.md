### Got error while using command "docker login":

`$ docker login` - "x509: certificate signed by unknown authority"

### info:

После запроса списка сертификатов, у меня появляется ошибка:

`openssl s_client -showcerts -connect sregistry.mts.ru:443` - verify error:num=19:self signed certificate in certificate chain (в цепочке сертификатов есть самоподписанный сертификат, который не может быть проверен, так как он не имеет связи с доверенными корневыми сертификатами)

Из-за этого у меня выдаёт ошибку при `docker login` / `docker pull` и тд - "x509: certificate signed by unknown authority"



### Пробовал:

1. Обновить пакеты OpenSSL на сервере:

`sudo apt update`\
`sudo apt upgrade openssl`

2. Установить пакет ca-certificates, который содержит список доверенных сертификатов:

`sudo apt install ca-certificates`

3. Обновить список доверенных сертификатов:

`sudo update-ca-certificates`

4. Снова пробовал авторизоваться:

`docker login sregistry.mts.ru`

Делал рестарт для обновления конфигурации сертификатов:

`sudo systemctl restart docker`

5. Пробовал создать собственный серт:
   /etc/docker/certs.d/sregistry.mts.ru/sregistry.mts.ru.crt
   с value из перменной GitLab - DOCKER_AUTH_CONFIG