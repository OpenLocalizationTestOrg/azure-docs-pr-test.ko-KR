---
title: "PostgreSQL용 Azure 데이터베이스의 서버 개념 | Microsoft Docs"
description: "이 항목에서는 PostgreSQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: c79603a11fa23ad775783157675c07ab67102057
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-servers"></a><span data-ttu-id="4200d-103">PostgreSQL용 Azure 데이터베이스 서버</span><span class="sxs-lookup"><span data-stu-id="4200d-103">Azure Database for PostgreSQL Servers</span></span>
<span data-ttu-id="4200d-104">이 항목에서는 PostgreSQL용 Azure 데이터베이스 서버를 사용할 때의 고려 사항 및 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-104">This topic provides considerations and guidelines for working with Azure Database for PostgreSQL servers.</span></span>

## <a name="what-is-an-azure-database-for-postgresql-server"></a><span data-ttu-id="4200d-105">PostgreSQL용 Azure 데이터베이스 서버란?</span><span class="sxs-lookup"><span data-stu-id="4200d-105">What is an Azure Database for PostgreSQL server?</span></span>
<span data-ttu-id="4200d-106">PostgreSQL용 Azure 데이터베이스 서버는 여러 데이터베이스에 대한 중앙 관리 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-106">An Azure Database for PostgreSQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="4200d-107">온-프레미스 환경에서도 익숙할 수 있는 동일한 PostgreSQL 서버 구문입니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-107">It is the same PostgreSQL server construct that you may be familiar with in the on-premises world.</span></span> <span data-ttu-id="4200d-108">특히, PostgreSQL 서비스는 관리되며, 성능 보장을 제공하고, 서버 수준에서 액세스 권한 및 기능을 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-108">Specifically, the PostgreSQL service is managed, provides performance guarantees, exposes access and features at server-level.</span></span>

<span data-ttu-id="4200d-109">PostgreSQL용 Azure 데이터베이스 서버:</span><span class="sxs-lookup"><span data-stu-id="4200d-109">An Azure Database for PostgreSQL server:</span></span>

- <span data-ttu-id="4200d-110">Azure 구독 내에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="4200d-111">데이터베이스에 대한 부모 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-111">Is the parent resource for databases.</span></span>
- <span data-ttu-id="4200d-112">데이터베이스에 대한 네임스페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="4200d-113">강력한 수명 의미 체계를 가진 컨테이너로서 서버를 삭제하고 포함된 데이터베이스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-113">Is a container with strong lifetime semantics - delete a server and it deletes the contained databases.</span></span>
- <span data-ttu-id="4200d-114">하위 지역에 리소스를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="4200d-115">서버 및 데이터베이스 액세스에 대한 연결 끝점(.postgresql.database.azure.com)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-115">Provides a connection endpoint for server and database access (.postgresql.database.azure.com).</span></span>
- <span data-ttu-id="4200d-116">로그인, 방화벽, 사용자, 역할 구성 등 해당 데이터베이스에 적용되는 관리 정책에 대한 범위를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-116">Provides the scope for management policies that apply to its databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="4200d-117">여러 버전으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-117">Is available in multiple versions.</span></span> <span data-ttu-id="4200d-118">자세한 내용은 [지원되는 PostgreSQL 데이터베이스 버전](concepts-supported-versions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-118">For more information, see [Supported PostgreSQL database versions](concepts-supported-versions.md).</span></span>
- <span data-ttu-id="4200d-119">사용자가 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-119">Is extensible by users.</span></span> <span data-ttu-id="4200d-120">자세한 내용은 [PostgreSQL 확장](concepts-extensions.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-120">For more information, see [PostgreSQL extensions](concepts-extensions.md).</span></span>

<span data-ttu-id="4200d-121">PostgreSQL 서버용 Azure Database 내에서 하나 이상의 데이터베이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-121">Within an Azure Database for PostgreSQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="4200d-122">서버당 단일 데이터베이스를 만들어 모든 리소스를 활용하도록 하거나 여러 데이터베이스를 만들어 리소스를 공유하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-122">You can opt to create a single database per server to utilize all the resources, or create multiple databases to share the resources.</span></span> <span data-ttu-id="4200d-123">가격은 가격 책정 계층, 계산 단위, 저장소(GB)의 구성에 따라 서버별로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-123">The pricing is structured per-server, based on the configuration of pricing tier, compute units, storage (GB).</span></span> <span data-ttu-id="4200d-124">자세한 내용은 [가격 책정 계층](./concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-124">For more details, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-postgresql-server"></a><span data-ttu-id="4200d-125">PostgreSQL용 Azure 데이터베이스 서버에 연결하고 인증을 받으려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="4200d-125">How do I connect and authenticate to an Azure Database for PostgreSQL server?</span></span>
<span data-ttu-id="4200d-126">다음과 같은 요소가 데이터베이스에 안전하게 액세스할 수 있도록 도와줍니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-126">The following elements help ensure safe access to your database.</span></span>

|||
| :-- | :-- |
| <span data-ttu-id="4200d-127">**인증 및 권한 부여**</span><span class="sxs-lookup"><span data-stu-id="4200d-127">**Authentication and authorization**</span></span> | <span data-ttu-id="4200d-128">PostgreSQL용 Azure 데이터베이스 서버는 네이티브 PostgreSQL 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-128">Azure Database for PostgreSQL server supports native PostgreSQL authentication.</span></span> <span data-ttu-id="4200d-129">서버의 관리자 로그인을 사용하여 서버에 연결하고 인증을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-129">You can connect and authenticate to server with the server's admin login.</span></span> |
| <span data-ttu-id="4200d-130">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="4200d-130">**Protocol**</span></span> | <span data-ttu-id="4200d-131">이 서비스는 PostgreSQL에서 사용되는 메시지 기반 프로토콜을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-131">The service supports a message-based protocol used by PostgreSQL.</span></span> |
| <span data-ttu-id="4200d-132">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="4200d-132">**TCP/IP**</span></span> | <span data-ttu-id="4200d-133">이 프로토콜은 TCP/IP 및 Unix 도메인 소켓을 통해 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-133">The protocol is supported over TCP/IP, and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="4200d-134">**방화벽**</span><span class="sxs-lookup"><span data-stu-id="4200d-134">**Firewall**</span></span> | <span data-ttu-id="4200d-135">데이터를 보호하기 위해, 방화벽 규칙은 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버 또는 해당 데이터베이스에 대한 모든 액세스를 금지합니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-135">To help protect your data, a firewall rule prevents all access to your database server, or to its databases, until you specify which computers have permission.</span></span> <span data-ttu-id="4200d-136">[PostgreSQL용 Azure 데이터베이스 서버 방화벽 규칙](concepts-firewall-rules.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-136">See [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md).</span></span> |
|||

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="4200d-137">서버는 어떻게 관리해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="4200d-137">How do I manage a server?</span></span>
<span data-ttu-id="4200d-138">Azure Portal 또는 [Azure CLI](/cli/azure/postgres)를 사용하여 PostgreSQL용 Azure 데이터베이스 서버를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4200d-138">You can manage Azure Database for PostgreSQL servers by using the Azure portal or the [Azure CLI](/cli/azure/postgres).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4200d-139">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4200d-139">Next steps</span></span>
- <span data-ttu-id="4200d-140">서비스 개요를 보려면 [PostgreSQL용 Azure 데이터베이스 개요](overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-140">For an overview of the service, see [Azure Database for PostgreSQL Overview](overview.md)</span></span>
- <span data-ttu-id="4200d-141">**서비스 계층**에 따른 특정 리소스 할당량 및 제한 사항에 대한 자세한 내용은 [서비스 계층](concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-141">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="4200d-142">서비스 연결에 대한 자세한 내용은 [PostgreSQL용 Azure 데이터베이스에 대한 연결 라이브러리](concepts-connection-libraries.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4200d-142">For information on connecting to the service, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md).</span></span>
