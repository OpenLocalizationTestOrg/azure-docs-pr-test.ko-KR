---
title: "MySQL용 Azure 데이터베이스의 서버 개념 | Microsoft Docs"
description: "이 항목에서는 MySQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: a2556206ac53829fcd6ab92ffe292859349790d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a><span data-ttu-id="b52e8-103">MySQL용 Azure 데이터베이스의 서버 개념</span><span class="sxs-lookup"><span data-stu-id="b52e8-103">Server concepts in Azure Database for MySQL</span></span>
<span data-ttu-id="b52e8-104">이 항목에서는 MySQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-104">This topic provides considerations and guidelines for working with Azure Database for MySQL servers.</span></span>

## <a name="what-is-an-azure-database-for-mysql-server"></a><span data-ttu-id="b52e8-105">MySQL용 Azure 데이터베이스 서버란?</span><span class="sxs-lookup"><span data-stu-id="b52e8-105">What is an Azure Database for MySQL server?</span></span>

<span data-ttu-id="b52e8-106">MySQL용 Azure 데이터베이스 서버는 여러 데이터베이스에 대한 중앙 관리 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-106">An Azure Database for MySQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="b52e8-107">온-프레미스 환경에서도 익숙할 수 있는 동일한 MySQL 서버 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-107">It is the same MySQL server construct that you may be familiar with in the on-premises world.</span></span> <span data-ttu-id="b52e8-108">특히, MySQL용 Azure 데이터베이스 서비스는 관리되며, 성능 보장을 제공하고, 서버 수준에서 액세스 권한 및 기능을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-108">Specifically, the Azure Database for MySQL service is managed, provides performance guarantees, exposes access and features at server-level.</span></span>

<span data-ttu-id="b52e8-109">MySQL용 Azure 데이터베이스 서버:</span><span class="sxs-lookup"><span data-stu-id="b52e8-109">An Azure Database for MySQL server:</span></span>

- <span data-ttu-id="b52e8-110">Azure 구독 내에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="b52e8-111">데이터베이스에 대한 부모 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-111">Is the parent resource for databases.</span></span>
- <span data-ttu-id="b52e8-112">데이터베이스에 대한 네임스페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="b52e8-113">강력한 수명 의미 체계를 가진 컨테이너로서 서버를 삭제하고 포함된 데이터베이스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-113">Is a container with strong lifetime semantics - delete a server and it deletes the contained databases.</span></span>
- <span data-ttu-id="b52e8-114">하위 지역에 리소스를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="b52e8-115">서버 및 데이터베이스 액세스에 대한 연결 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-115">Provides a connection endpoint for server and database access.</span></span>
- <span data-ttu-id="b52e8-116">로그인, 방화벽, 사용자, 역할 구성 등 해당 데이터베이스에 적용되는 관리 정책에 대한 범위를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-116">Provides the scope for management policies that apply to its databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="b52e8-117">여러 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-117">Is available in multiple versions.</span></span> <span data-ttu-id="b52e8-118">자세한 내용은 [지원되는 MySQL용 Azure 데이터베이스 버전](./concepts-supported-versions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-118">For more information, see [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md).</span></span>

<span data-ttu-id="b52e8-119">MySQL 서버용 Azure Database 내에서 하나 이상의 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-119">Within an Azure Database for MySQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="b52e8-120">서버당 단일 데이터베이스를 만들어 모든 리소스를 활용하도록 하거나 여러 데이터베이스를 만들어 리소스를 공유하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-120">You can opt to create a single database per server to utilize all the resources, or create multiple databases to share the resources.</span></span> <span data-ttu-id="b52e8-121">가격은 가격 책정 계층, 계산 단위, 저장소(GB)의 구성에 따라 서버별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-121">The pricing is structured per-server, based on the configuration of pricing tier, compute units, storage (GB).</span></span> <span data-ttu-id="b52e8-122">자세한 내용은 [가격 책정 계층](./concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-122">For more information, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-mysql-server"></a><span data-ttu-id="b52e8-123">MySQL용 Azure 데이터베이스 서버에 연결하고 인증을 받으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b52e8-123">How do I connect and authenticate to an Azure Database for MySQL server?</span></span>

<span data-ttu-id="b52e8-124">다음과 같은 요소가 데이터베이스에 안전하게 액세스할 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-124">The following elements help ensure safe access to your database.</span></span>

|||
| :-- | :-- |
| <span data-ttu-id="b52e8-125">**인증 및 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="b52e8-125">**Authentication and authorization**</span></span> | <span data-ttu-id="b52e8-126">MySQL용 Azure 데이터베이스 서버는 네이티브 MySQL 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-126">Azure Database for MySQL server supports native MySQL authentication.</span></span> <span data-ttu-id="b52e8-127">서버의 관리자 로그인을 사용하여 서버에 연결하고 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-127">You can connect and authenticate to server with the server's admin login.</span></span> |
| <span data-ttu-id="b52e8-128">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="b52e8-128">**Protocol**</span></span> | <span data-ttu-id="b52e8-129">이 서비스는 MySQL에서 사용되는 메시지 기반 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-129">The service supports a message-based protocol used by MySQL.</span></span> |
| <span data-ttu-id="b52e8-130">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="b52e8-130">**TCP/IP**</span></span> | <span data-ttu-id="b52e8-131">이 프로토콜은 TCP/IP 및 Unix 도메인 소켓을 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-131">The protocol is supported over TCP/IP, and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="b52e8-132">**방화벽**</span><span class="sxs-lookup"><span data-stu-id="b52e8-132">**Firewall**</span></span> | <span data-ttu-id="b52e8-133">데이터를 보호하기 위해, 방화벽 규칙은 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버 또는 해당 데이터베이스에 대한 모든 액세스를 금지합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-133">To help protect your data, a firewall rule prevents all access to your database server, or to its databases, until you specify which computers have permission.</span></span> <span data-ttu-id="b52e8-134">[MySQL용 Azure 데이터베이스 서버 방화벽 규칙](./concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-134">See [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span></span> |
| <span data-ttu-id="b52e8-135">**SSL**</span><span class="sxs-lookup"><span data-stu-id="b52e8-135">**SSL**</span></span> | <span data-ttu-id="b52e8-136">이 서비스는 응용 프로그램 및 데이터베이스 서버 간의 SSL 연결 적용을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-136">The service supports enforcing SSL connections between your applications and your database server.</span></span>  <span data-ttu-id="b52e8-137">[MySQL용 Azure 데이터베이스에 안전하게 연결하기 위한 사용자 응용 프로그램의 SSL 연결 구성](./howto-configure-ssl.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-137">See [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span> |
|||

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="b52e8-138">서버는 어떻게 관리해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="b52e8-138">How do I manage a server?</span></span>
<span data-ttu-id="b52e8-139">Azure Portal 또는 Azure CLI를 사용하여 MySQL용 Azure 데이터베이스 서버를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b52e8-139">You can manage Azure Database for MySQL servers by using the Azure portal or the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b52e8-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b52e8-140">Next steps</span></span>
- <span data-ttu-id="b52e8-141">서비스 개요를 보려면 [MySQL용 Azure 데이터베이스 개요](./overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-141">For an overview of the service, see [Azure Database for MySQL Overview](./overview.md)</span></span>
- <span data-ttu-id="b52e8-142">**서비스 계층**에 따른 특정 리소스 할당량 및 제한 사항에 대한 자세한 내용은 [서비스 계층](./concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-142">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-service-tiers.md)</span></span>
- <span data-ttu-id="b52e8-143">서비스 연결에 대한 자세한 내용은 [MySQL용 Azure 데이터베이스에 대한 연결 라이브러리](./concepts-connection-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b52e8-143">For information about connecting to the service, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md).</span></span>
