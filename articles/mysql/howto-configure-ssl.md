---
title: "aaaConfigure SSL 연결 toosecurely MySQL 용 tooAzure 데이터베이스 연결 | Microsoft Docs"
description: "SSL 연결을 사용 하는 tooproperly MySQL 및 toocorrectly 관련된 응용 프로그램에 대 한 Azure 데이터베이스를 구성 하는 방법에 대 한 지침"
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="8681e-103">SSL을 구성에서 응용 프로그램 toosecurely 연결 MySQL 용 tooAzure 데이터베이스 연결</span><span class="sxs-lookup"><span data-stu-id="8681e-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="8681e-104">MySQL에 대 한 azure 데이터베이스 MySQL 서버 tooclient 응용 프로그램 (SECURE Sockets Layer)을 사용 하 여 Azure 데이터베이스 연결을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="8681e-105">데이터베이스 서버와 클라이언트 응용 프로그램 간의 SSL 연결을 강제 적용 하면 공격 으로부터 보호 "man hello 중간에" hello 서버와 응용 프로그램 간의 hello 데이터 스트림을 암호화 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="8681e-106">1단계: SSL 인증서 받기</span><span class="sxs-lookup"><span data-stu-id="8681e-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="8681e-107">Azure에서 MySQL 서버에 대 한 데이터베이스와 함께 SSL을 통해 hello 필요한 인증서 toocommunicate 다운로드 [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) hello 인증서 파일 tooyour 로컬 저장 드라이브 (이 자습서와 함께 사용 c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="8681e-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="8681e-108">**Microsoft Internet Explorer 및 Microsoft Edge:** hello 다운로드 완료 되 면 hello 인증서 tooBaltimoreCyberTrustRoot.crt.pem 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="8681e-109">2단계: SSL 바인딩</span><span class="sxs-lookup"><span data-stu-id="8681e-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="8681e-110">Tooserver hello MySQL 워크 벤치를 사용 하 여 SSL을 통한 연결</span><span class="sxs-lookup"><span data-stu-id="8681e-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="8681e-111">MySQL 워크 벤치 tooconnect SSL을 통해 안전 하 게 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="8681e-112">Toohello 이동 **SSL** hello MySQL 워크 벤치 hello 새 연결 설정 대화 상자에서 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="8681e-113">Hello의 hello 파일 위치를 입력 **BaltimoreCyberTrustRoot.crt.pem** hello에 **SSL CA 파일:** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="8681e-114">![사용자 지정된 타일 저장](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="8681e-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="8681e-115">Tooserver hello MySQL CLI를 사용 하 여 SSL을 통한 연결</span><span class="sxs-lookup"><span data-stu-id="8681e-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="8681e-116">Hello MySQL 명령줄 인터페이스를 사용 하 여 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="8681e-117">3단계: Azure에 SSL 연결 적용</span><span class="sxs-lookup"><span data-stu-id="8681e-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="8681e-118">Azure Portal 사용</span><span class="sxs-lookup"><span data-stu-id="8681e-118">Using Azure portal</span></span>
<span data-ttu-id="8681e-119">MySQL 서버와 클릭에 대 한 Azure 데이터베이스 방문 hello Azure 포털을 사용 하 여 **연결 보안**합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="8681e-120">토글 단추 tooenable hello를 사용 하 여 hello를 사용 하지 않도록 설정 하거나 **적용 SSL 연결** 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="8681e-121">그런 다음 **Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-121">Then click **Save**.</span></span> <span data-ttu-id="8681e-122">Tooalways 사용 하도록 설정 하는 것이 좋습니다 **적용 SSL 연결** 강화 된 보안을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="8681e-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="8681e-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="8681e-124">Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="8681e-124">Using Azure CLI</span></span>
<span data-ttu-id="8681e-125">Hello를 사용 하지 않도록 설정 하거나 설정할 수 있습니다 **ssl 적용** Azure CLI에서 Enabled 또는 Disabled 값을 각각 사용 하는 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="8681e-126">4단계: SSL 연결 확인</span><span class="sxs-lookup"><span data-stu-id="8681e-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="8681e-127">Hello mysql 실행 **상태** 명령 tooverify SSL을 사용 하 여 tooyour MySQL 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="8681e-128">Hello 출력을 검토 하 여 hello 연결이 암호화 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="8681e-129">**SSL: Cipher in use is AES256-SHA**라고 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8681e-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="8681e-130">샘플 코드</span><span class="sxs-lookup"><span data-stu-id="8681e-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="8681e-131">PHP</span><span class="sxs-lookup"><span data-stu-id="8681e-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="8681e-132">파이썬</span><span class="sxs-lookup"><span data-stu-id="8681e-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="8681e-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8681e-133">Next steps</span></span>
<span data-ttu-id="8681e-134">[MySQL용 Azure Database에 대한 연결 라이브러리](concepts-connection-libraries.md)에 이어지는 다양한 응용 프로그램 연결 옵션 검토</span><span class="sxs-lookup"><span data-stu-id="8681e-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
