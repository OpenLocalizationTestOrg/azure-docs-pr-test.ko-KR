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
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a><span data-ttu-id="1c7cf-103">MySQL에 대 한 응용 프로그램 tooAzure tooconnect 데이터베이스 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1c7cf-103">How tooconnect applications tooAzure Database for MySQL</span></span>
<span data-ttu-id="1c7cf-104">이 문서에 지원 되는 Azure 데이터베이스에서 MySQL에 대 한 서식 파일 및 예제와 함께 hello 연결 문자열 형식을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-104">This document lists hello connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="1c7cf-105">연결 문자열에 다른 매개 변수 및 다른 설정을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="1c7cf-106">tooobtain hello 인증서 참조 [어떻게 tooconfigure SSL](./howto-configure-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-106">tooobtain hello certificate, see [How tooconfigure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="1c7cf-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="1c7cf-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="1c7cf-108">{your_user}@{servername} = 올바른 인증을 위한 사용자 ID 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="1c7cf-109">방금 hello userID를 사용 하 여 hello 인증 toofail을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-109">Using just hello userID will cause hello authentication toofail.</span></span>

## <a name="adonet"></a><span data-ttu-id="1c7cf-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="1c7cf-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="1c7cf-111">이 예제에서는 hello 서버 이름은 `myserver4demo`, 데이터베이스 이름은 `wpdb`, 사용자 이름은 `WPAdmin`, 암호도 `mypassword!2`합니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-111">In this example, hello server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="1c7cf-112">그런 다음 연결 문자열 hello 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-112">Then, hello connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="1c7cf-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="1c7cf-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="1c7cf-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="1c7cf-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="1c7cf-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="1c7cf-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="1c7cf-116">PHP</span><span class="sxs-lookup"><span data-stu-id="1c7cf-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="1c7cf-117">Python</span><span class="sxs-lookup"><span data-stu-id="1c7cf-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="1c7cf-118">루비</span><span class="sxs-lookup"><span data-stu-id="1c7cf-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a><span data-ttu-id="1c7cf-119">Hello Azure 포털에서에서 hello 연결 문자열 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="1c7cf-119">Get hello connection string details from hello Azure portal</span></span>
<span data-ttu-id="1c7cf-120">Hello에 [Azure 포털](https://portal.azure.com)MySQL server에 대 한 Azure 데이터베이스 tooyour 이동한 다음 클릭 **연결 문자열** 인스턴스에 대 한 문자열 목록 tooget: ![hello에 hello 연결 문자열 창 Azure 포털](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="1c7cf-120">In hello [Azure portal](https://portal.azure.com), go tooyour Azure Database for MySQL server, and then click **Connection strings** tooget your string list for your instance: ![hello Connection strings pane in hello Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="1c7cf-121">hello 문자열 hello 드라이버, 서버 및 다른 데이터베이스 연결 매개 변수 등의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-121">hello string provides details such as hello driver, server, and other database connection parameters.</span></span> <span data-ttu-id="1c7cf-122">데이터베이스 이름, 암호 등과 같은 고유한 매개 변수를 사용하여 이러한 예제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="1c7cf-123">다음 코드와 응용 프로그램에서이 문자열 tooconnect toohello 서버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-123">You can then use this string tooconnect toohello server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c7cf-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1c7cf-124">Next steps</span></span>
- <span data-ttu-id="1c7cf-125">연결 라이브러리에 대한 자세한 내용은 [개념 - 연결 라이브러리](./concepts-connection-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1c7cf-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
