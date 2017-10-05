---
title: "MySQL용 Azure Database에 응용 프로그램 연결 | Microsoft Docs"
description: "이 문서에는 MySQL용 Azure Database와 연결하는 응용 프로그램에 대한 현재 지원되는 연결 문자열이 나열되어 있습니다(ADO.NET (C#), JDBC, Node.js, ODBC, PHP, Python 및 Ruby)."
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: 2f40da41bcfda7e35f6fc63ead5d055246ab390c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-applications-to-azure-database-for-mysql"></a><span data-ttu-id="9b6f5-103">MySQL용 Azure Database에 응용 프로그램을 연결하는 방법</span><span class="sxs-lookup"><span data-stu-id="9b6f5-103">How to connect applications to Azure Database for MySQL</span></span>
<span data-ttu-id="9b6f5-104">이 문서에는 템플릿 및 예제와 함께 MySQL용 Azure Database에서 지원되는 연결 문자열 형식이 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-104">This document lists the connection string types that are supported by Azure Database for MySQL, together with templates and examples.</span></span> <span data-ttu-id="9b6f5-105">연결 문자열에 다른 매개 변수 및 다른 설정을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-105">You might have different parameters and different settings in your connection string.</span></span>

- <span data-ttu-id="9b6f5-106">인증서를 가져오려면 [SSL 구성 방법](./howto-configure-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-106">To obtain the certificate, see [How to configure SSL](./howto-configure-ssl.md).</span></span>
- <span data-ttu-id="9b6f5-107">{your_host} = <servername>.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="9b6f5-107">{your_host} = <servername>.mysql.database.azure.com</span></span>
- <span data-ttu-id="9b6f5-108">{your_user}@{servername} = 올바른 인증을 위한 사용자 ID 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-108">{your_user}@{servername} = userID format for authentication correctly.</span></span>  <span data-ttu-id="9b6f5-109">사용자 ID를 사용하면 인증에 실패하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-109">Using just the userID will cause the authentication to fail.</span></span>

## <a name="adonet"></a><span data-ttu-id="9b6f5-110">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="9b6f5-110">ADO.NET</span></span>
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

<span data-ttu-id="9b6f5-111">이 예제에서 서버 이름은 `myserver4demo`, 데이터베이스 이름은 `wpdb`, 사용자 이름은 `WPAdmin`, 암호는 `mypassword!2`입니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-111">In this example, the server name is `myserver4demo`, database name is `wpdb`, user name is `WPAdmin`, and password is `mypassword!2`.</span></span> <span data-ttu-id="9b6f5-112">그러면 연결 문자열은 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-112">Then, the connection string should be:</span></span>

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a><span data-ttu-id="9b6f5-113">JDBC</span><span class="sxs-lookup"><span data-stu-id="9b6f5-113">JDBC</span></span>
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a><span data-ttu-id="9b6f5-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="9b6f5-114">Node.js</span></span>
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a><span data-ttu-id="9b6f5-115">ODBC</span><span class="sxs-lookup"><span data-stu-id="9b6f5-115">ODBC</span></span>
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a><span data-ttu-id="9b6f5-116">PHP</span><span class="sxs-lookup"><span data-stu-id="9b6f5-116">PHP</span></span>
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a><span data-ttu-id="9b6f5-117">Python</span><span class="sxs-lookup"><span data-stu-id="9b6f5-117">Python</span></span>
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a><span data-ttu-id="9b6f5-118">Ruby</span><span class="sxs-lookup"><span data-stu-id="9b6f5-118">Ruby</span></span>
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-the-connection-string-details-from-the-azure-portal"></a><span data-ttu-id="9b6f5-119">Azure Portal에서 연결 문자열 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="9b6f5-119">Get the connection string details from the Azure portal</span></span>
<span data-ttu-id="9b6f5-120">[Azure Portal](https://portal.azure.com)에서 MySQL용 Azure Database 서버로 이동하고 **연결 문자열**을 클릭하여 사용자 인스턴스에 대한 문자열 목록을 가져옵니다. ![Azure Portal의 연결 문자열 창](./media/howto-connection-strings/connection-strings-on-portal.png)</span><span class="sxs-lookup"><span data-stu-id="9b6f5-120">In the [Azure portal](https://portal.azure.com), go to your Azure Database for MySQL server, and then click **Connection strings** to get your string list for your instance: ![The Connection strings pane in the Azure portal](./media/howto-connection-strings/connection-strings-on-portal.png)</span></span>

<span data-ttu-id="9b6f5-121">문자열은 드라이버, 서버 및 다른 데이터베이스 연결 매개 변수와 같은 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-121">The string provides details such as the driver, server, and other database connection parameters.</span></span> <span data-ttu-id="9b6f5-122">데이터베이스 이름, 암호 등과 같은 고유한 매개 변수를 사용하여 이러한 예제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-122">Modify these examples by using your own parameters, such as database name, password, and so on.</span></span> <span data-ttu-id="9b6f5-123">그런 다음, 이 문자열을 사용하여 사용자 코드와 응용 프로그램에서 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-123">You can then use this string to connect to the server from your code and applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b6f5-124">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b6f5-124">Next steps</span></span>
- <span data-ttu-id="9b6f5-125">연결 라이브러리에 대한 자세한 내용은 [개념 - 연결 라이브러리](./concepts-connection-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9b6f5-125">For more information about connection libraries, see [Concepts - Connection libraries](./concepts-connection-libraries.md).</span></span>
