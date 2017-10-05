---
title: "MySQL용 Azure 데이터베이스에 대한 SSL 연결 | Microsoft Docs"
description: "SSL 연결을 올바르게 사용하도록 MySQL용 Azure 데이터베이스 및 연결된 응용 프로그램을 구성하는 방법에 대한 정보"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="f8ac4-103">MySQL용 Azure 데이터베이스의 SSL 연결</span><span class="sxs-lookup"><span data-stu-id="f8ac4-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="f8ac4-104">MySQL용 Azure 데이터베이스는 SSL(Secure Sockets Layer)을 사용하여 데이터베이스 서버를 클라이언트 응용 프로그램에 연결하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="f8ac4-105">데이터베이스 서버와 클라이언트 응용 프로그램 간 SSL 연결을 적용하면 서버와 응용 프로그램 간 데이터 스트림을 암호화함으로써 “메시지 가로채기(man in the middle)” 공격으로부터 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="f8ac4-106">기본 설정</span><span class="sxs-lookup"><span data-stu-id="f8ac4-106">Default settings</span></span>
<span data-ttu-id="f8ac4-107">기본적으로 데이터베이스 서비스는 MySQL에 연결할 때 SSL 연결이 필요하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="f8ac4-108">가능하면 SSL 옵션을 해제하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="f8ac4-109">Azure Portal 및 CLI를 통해 새로운 MySQL용 Azure 데이터베이스 서버를 프로비전할 때 SSL 연결 적용이 기본적으로 활성화됩니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="f8ac4-110">마찬가지로, Azure Portal의 해당 서버에 있는 “연결 문자열” 설정에서 미리 정의된 연결 문자열에는 SSL을 사용하여 데이터베이스 서버에 연결하기 위한 일반적인 언어에 대한 필수 매개 변수가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="f8ac4-111">SSL 매개 변수는 커넥터에 따라 달라집니다. 예를 들어 "ssl = true", "sslmode=require" 또는 "sslmode=required"이거나 다른 변형이 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="f8ac4-112">응용 프로그램을 개발할 때 SSL 연결을 사용하거나 사용하지 않도록 설정하는 방법을 알아보려면 [SSL 구성 방법](howto-configure-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8ac4-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8ac4-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f8ac4-113">Next steps</span></span>
[<span data-ttu-id="f8ac4-114">MySQL용 Azure 데이터베이스에 대한 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f8ac4-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
