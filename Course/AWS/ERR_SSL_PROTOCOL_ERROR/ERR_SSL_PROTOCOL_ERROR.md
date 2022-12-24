### ERROR when open https://ec2-174-129-174-241.compute-1.amazonaws.com:3000/
* Этот сайт не может обеспечить безопасное соединение
* Сайт ec2-174-129-174-241.compute-1.amazonaws.com отправил недействительный ответ.
* `ERR_SSL_PROTOCOL_ERROR`

### Solution:
* `http://ec2-174-129-174-241.compute-1.amazonaws.com:3000/` - **change PROTOCOL**
  * https -> http