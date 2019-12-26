## curl 请求参数带变量


写的升级shell脚本，里面调用了某些restapi，需要传header或者body参数，使用shell中定义的变量($xx,  ${xx}形式)，发现不能转换，原因是在单引号里面。

https://stackoverflow.com/questions/13341955/how-to-pass-a-variable-in-a-curl-command-in-shell-scripting

结论：如果使用变量，得换成双引号，数据里面也有双引号，加转义字符即可。

最终形式如下：

curl-X POST --header'Content-Type: application/json'--header'Accept: application/json'--header'authtype: local'--header"username: $admin_user"--header"password:${admin_token}"-d"{\"email\": \"$payment_email\", \"paymentAccount\": \"$payment_account\", \"paymentServer\": \"${server_name}\", \"remarks\": \"vendor for${wx_service_name}\", \"vendor\": \"xxx\" }" "http://xxxxx.com/api/001api"-w"\nhttp_code=%{http_code}\n"-v -o${result_log} |grep'http_code=200'
