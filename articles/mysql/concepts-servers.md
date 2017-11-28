---
title: "MySQL에 대 한 Azure 데이터베이스에 대 한 aaaServer 개념 | Microsoft Docs"
description: "이 항목에서는 MySQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a><span data-ttu-id="d3699-103">MySQL용 Azure 데이터베이스의 서버 개념</span><span class="sxs-lookup"><span data-stu-id="d3699-103">Server concepts in Azure Database for MySQL</span></span>
<span data-ttu-id="d3699-104">이 항목에서는 MySQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-104">This topic provides considerations and guidelines for working with Azure Database for MySQL servers.</span></span>

## <a name="what-is-an-azure-database-for-mysql-server"></a><span data-ttu-id="d3699-105">MySQL용 Azure 데이터베이스 서버란?</span><span class="sxs-lookup"><span data-stu-id="d3699-105">What is an Azure Database for MySQL server?</span></span>

<span data-ttu-id="d3699-106">MySQL용 Azure 데이터베이스 서버는 여러 데이터베이스에 대한 중앙 관리 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-106">An Azure Database for MySQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="d3699-107">되기 hello 동일한 MySQL 서버 구문 hello 온-프레미스 환경에서에 대해 잘 알고 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-107">It is hello same MySQL server construct that you may be familiar with in hello on-premises world.</span></span> <span data-ttu-id="d3699-108">특히, MySQL 서비스에 대 한 hello Azure 데이터베이스 관리 되는 성능을 보장, 액세스 및 서버 수준에서 기능을 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-108">Specifically, hello Azure Database for MySQL service is managed, provides performance guarantees, exposes access and features at server-level.</span></span>

<span data-ttu-id="d3699-109">MySQL용 Azure 데이터베이스 서버:</span><span class="sxs-lookup"><span data-stu-id="d3699-109">An Azure Database for MySQL server:</span></span>

- <span data-ttu-id="d3699-110">Azure 구독 내에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="d3699-111">데이터베이스에 대 한 hello 부모 리소스가입니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-111">Is hello parent resource for databases.</span></span>
- <span data-ttu-id="d3699-112">데이터베이스에 대한 네임스페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="d3699-113">컨테이너 강력한 수명 의미 체계가-있는 서버를 삭제 하 고 hello 포함 된 데이터베이스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-113">Is a container with strong lifetime semantics - delete a server and it deletes hello contained databases.</span></span>
- <span data-ttu-id="d3699-114">하위 지역에 리소스를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="d3699-115">서버 및 데이터베이스 액세스에 대한 연결 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-115">Provides a connection endpoint for server and database access.</span></span>
- <span data-ttu-id="d3699-116">Tooits 데이터베이스 적용 되는 관리 정책에 대 한 hello 범위를 제공 합니다: 로그인, 방화벽, 사용자, 역할, 구성, 등입니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-116">Provides hello scope for management policies that apply tooits databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="d3699-117">여러 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-117">Is available in multiple versions.</span></span> <span data-ttu-id="d3699-118">자세한 내용은 [지원되는 MySQL용 Azure 데이터베이스 버전](./concepts-supported-versions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3699-118">For more information, see [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md).</span></span>

<span data-ttu-id="d3699-119">Azure Database for MySQL 서버 내에서 하나 이상의 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-119">Within an Azure Database for MySQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="d3699-120">모든 hello 리소스 toocreate 서버 tooutilize 당 단일 데이터베이스를 선택 하거나 여러 데이터베이스 tooshare hello 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-120">You can opt toocreate a single database per server tooutilize all hello resources, or create multiple databases tooshare hello resources.</span></span> <span data-ttu-id="d3699-121">구조적된 서버 hello 가격 책정은, 가격 책정 계층의 hello 구성에 따라, 단위, 저장소 (GB)를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-121">hello pricing is structured per-server, based on hello configuration of pricing tier, compute units, storage (GB).</span></span> <span data-ttu-id="d3699-122">자세한 내용은 [가격 책정 계층](./concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3699-122">For more information, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a><span data-ttu-id="d3699-123">어떻게 연결 하 고 MySQL server에 대 한 Azure 데이터베이스 tooan 인증?</span><span class="sxs-lookup"><span data-stu-id="d3699-123">How do I connect and authenticate tooan Azure Database for MySQL server?</span></span>

<span data-ttu-id="d3699-124">hello 다음과 같은 요소가 보장할 안전 하 게 액세스할 tooyour 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="d3699-124">hello following elements help ensure safe access tooyour database.</span></span>

|||
| :-- | :-- |
| <span data-ttu-id="d3699-125">**인증 및 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="d3699-125">**Authentication and authorization**</span></span> | <span data-ttu-id="d3699-126">MySQL용 Azure 데이터베이스 서버는 네이티브 MySQL 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-126">Azure Database for MySQL server supports native MySQL authentication.</span></span> <span data-ttu-id="d3699-127">연결 하 고 hello 서버의 관리자 로그인과 tooserver 인증 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-127">You can connect and authenticate tooserver with hello server's admin login.</span></span> |
| <span data-ttu-id="d3699-128">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="d3699-128">**Protocol**</span></span> | <span data-ttu-id="d3699-129">hello 서비스는 MySQL에서 사용 되는 메시지 기반 프로토콜을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-129">hello service supports a message-based protocol used by MySQL.</span></span> |
| <span data-ttu-id="d3699-130">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="d3699-130">**TCP/IP**</span></span> | <span data-ttu-id="d3699-131">hello 프로토콜 over TCP/IP 사용 및 Unix 도메인 소켓을 통해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-131">hello protocol is supported over TCP/IP, and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="d3699-132">**방화벽**</span><span class="sxs-lookup"><span data-stu-id="d3699-132">**Firewall**</span></span> | <span data-ttu-id="d3699-133">toohelp 데이터를 보호, 방화벽 규칙 방지 모든 액세스 tooyour 데이터베이스 서버 또는 컴퓨터를 지정할 때까지 tooits 데이터베이스 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-133">toohelp protect your data, a firewall rule prevents all access tooyour database server, or tooits databases, until you specify which computers have permission.</span></span> <span data-ttu-id="d3699-134">[MySQL용 Azure 데이터베이스 서버 방화벽 규칙](./concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3699-134">See [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span></span> |
| <span data-ttu-id="d3699-135">**SSL**</span><span class="sxs-lookup"><span data-stu-id="d3699-135">**SSL**</span></span> | <span data-ttu-id="d3699-136">hello 서비스 지원 응용 프로그램와 데이터베이스 서버 간에 SSL 연결을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-136">hello service supports enforcing SSL connections between your applications and your database server.</span></span>  <span data-ttu-id="d3699-137">참조 [응용 프로그램 toosecurely에서 SSL 구성 연결 MySQL 용 tooAzure 데이터베이스 연결](./howto-configure-ssl.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-137">See [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span> |
|||

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="d3699-138">서버는 어떻게 관리해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="d3699-138">How do I manage a server?</span></span>
<span data-ttu-id="d3699-139">Azure CLI hello 또는 hello Azure 포털을 사용 하 여 MySQL server에 대 한 Azure 데이터베이스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-139">You can manage Azure Database for MySQL servers by using hello Azure portal or hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d3699-140">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d3699-140">Next steps</span></span>
- <span data-ttu-id="d3699-141">Hello 서비스의 개요를 참조 하십시오. [Azure 데이터베이스에 대 한 MySQL 개요](./overview.md)</span><span class="sxs-lookup"><span data-stu-id="d3699-141">For an overview of hello service, see [Azure Database for MySQL Overview](./overview.md)</span></span>
- <span data-ttu-id="d3699-142">**서비스 계층**에 따른 특정 리소스 할당량 및 제한 사항에 대한 자세한 내용은 [서비스 계층](./concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d3699-142">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-service-tiers.md)</span></span>
- <span data-ttu-id="d3699-143">연결 toohello 서비스에 대 한 정보를 참조 하십시오. [MySQL에 대 한 Azure 데이터베이스에 대 한 연결 라이브러리](./concepts-connection-libraries.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d3699-143">For information about connecting toohello service, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md).</span></span>
