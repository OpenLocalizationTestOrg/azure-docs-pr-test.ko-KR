---
title: "MySQL에 대 한 데이터베이스 aaaConnect 응용 프로그램 tooAzure | Microsoft Docs"
description: "이 문서는 ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python 및 Ruby를 비롯 한 MySQL에 대 한 Azure 데이터베이스 tooconnect 응용 프로그램에 대 한 현재 지원 되는 hello 연결 문자열을 나열 합니다."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>MySQL에 대 한 응용 프로그램 tooAzure tooconnect 데이터베이스 하는 방법
이 문서에 지원 되는 Azure 데이터베이스에서 MySQL에 대 한 서식 파일 및 예제와 함께 hello 연결 문자열 형식을 보여 줍니다. 연결 문자열에 다른 매개 변수 및 다른 설정을 할 수도 있습니다.

- tooobtain hello 인증서 참조 [어떻게 tooconfigure SSL](./howto-configure-ssl.md)합니다.
- {your_host} = <servername>.mysql.database.azure.com
- {your_user}@{servername} = 올바른 인증을 위한 사용자 ID 형식입니다.  방금 hello userID를 사용 하 여 hello 인증 toofail을 발생 합니다.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

이 예제에서는 hello 서버 이름은 `myserver4demo`, 데이터베이스 이름은 `wpdb`, 사용자 이름은 `WPAdmin`, 암호도 `mypassword!2`합니다. 그런 다음 연결 문자열 hello 여야 합니다.

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>루비
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Hello Azure 포털에서에서 hello 연결 문자열 정보 가져오기
Hello에 [Azure 포털](https://portal.azure.com)MySQL server에 대 한 Azure 데이터베이스 tooyour 이동한 다음 클릭 **연결 문자열** 인스턴스에 대 한 문자열 목록 tooget: ![hello에 hello 연결 문자열 창 Azure 포털](./media/howto-connection-strings/connection-strings-on-portal.png)

hello 문자열 hello 드라이버, 서버 및 다른 데이터베이스 연결 매개 변수 등의 세부 정보를 제공합니다. 데이터베이스 이름, 암호 등과 같은 고유한 매개 변수를 사용하여 이러한 예제를 수정합니다. 다음 코드와 응용 프로그램에서이 문자열 tooconnect toohello 서버를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
- 연결 라이브러리에 대한 자세한 내용은 [개념 - 연결 라이브러리](./concepts-connection-libraries.md)를 참조하세요.
