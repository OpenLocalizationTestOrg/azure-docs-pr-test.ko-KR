---
title: "PostgreSQL용 Azure Database에서 서버를 백업 및 복원하는 방법 | Microsoft Docs"
description: "Azure CLI를 사용하여 PostgreSQL용 Azure Database에서 서버를 백업 및 복원하는 방법을 알아봅니다."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 871887e67d686a965a0648d2c6f0c72b3008db05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-back-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-the-azure-cli"></a><span data-ttu-id="83dbe-103">Azure CLI를 사용하여 PostgreSQL용 Azure Database에서 서버를 백업 및 복원하는 방법</span><span class="sxs-lookup"><span data-stu-id="83dbe-103">How to back up and restore a server in Azure Database for PostgreSQL by using the Azure CLI</span></span>

<span data-ttu-id="83dbe-104">PostgreSQL용 Azure Database를 사용하여 7~35일 이전 날짜로 서버 데이터베이스를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-104">Use Azure Database for PostgreSQL to restore a server database to an earlier date that spans from 7 to 35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83dbe-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="83dbe-105">Prerequisites</span></span>
<span data-ttu-id="83dbe-106">이 방법 가이드를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-106">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="83dbe-107">[PostgreSQL용 Azure Database 서버 및 데이터베이스](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="83dbe-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="83dbe-108">Azure CLI를 로컬로 설치하여 사용하는 경우 이 방법 가이드를 사용하려면 Azure CLI 버전 2.0 이상을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-108">If you install and use the Azure CLI locally, this how-to guide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="83dbe-109">버전을 확인하려면 Azure CLI 명령 프롬프트에서 `az --version`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-109">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="83dbe-110">설치하거나 업그레이드하려면 [Azure CLI 2.0 설치]( /cli/azure/install-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83dbe-110">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="83dbe-111">자동으로 수행되는 백업</span><span class="sxs-lookup"><span data-stu-id="83dbe-111">Back up happens automatically</span></span>
<span data-ttu-id="83dbe-112">PostgreSQL용 Azure Database를 사용하는 경우 데이터베이스 서비스에서 자동으로 5분마다 서비스 백업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-112">When you use Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="83dbe-113">기본 계층의 경우 백업은 7일간 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-113">For Basic Tier, the backups are available for 7 days.</span></span> <span data-ttu-id="83dbe-114">표준 계층의 경우 백업은 35일간 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-114">For Standard Tier, the backups are available for 35 days.</span></span> <span data-ttu-id="83dbe-115">자세한 내용은 [PostgreSQL용 Azure Database 가격 책정 계층](concepts-service-tiers.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="83dbe-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="83dbe-116">이 자동 백업 기능을 사용하여 서버 및 해당 데이터베이스를 이전 날짜 또는 특정 시점으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-116">With this automatic backup feature, you can restore the server and its databases to an earlier date, or point in time.</span></span>

## <a name="restore-a-database-to-a-previous-point-in-time-by-using-the-azure-cli"></a><span data-ttu-id="83dbe-117">Azure CLI를 사용하여 이전 특정 시점으로 데이터베이스 복원</span><span class="sxs-lookup"><span data-stu-id="83dbe-117">Restore a database to a previous point in time by using the Azure CLI</span></span>
<span data-ttu-id="83dbe-118">PostgreSQL용 Azure Database를 사용하여 서버를 이전 특정 시점으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-118">Use Azure Database for PostgreSQL to restore the server to a previous point in time.</span></span> <span data-ttu-id="83dbe-119">복원된 데이터는 새 서버에 복사되고 기존 서버는 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-119">The restored data is copied to a new server, and the existing server is left as is.</span></span> <span data-ttu-id="83dbe-120">예를 들어 테이블이 오늘 정오에 실수로 삭제된 경우 정오 바로 전 시간으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-120">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span></span> <span data-ttu-id="83dbe-121">그런 다음 서버의 복원된 복사본에서 누락된 테이블 및 데이터를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-121">Then, you can retrieve the missing table and data from the restored copy of the server.</span></span> 

<span data-ttu-id="83dbe-122">서버를 복원하려면 Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-122">To restore the server, use the Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-the-restore-command"></a><span data-ttu-id="83dbe-123">복원 명령 실행</span><span class="sxs-lookup"><span data-stu-id="83dbe-123">Run the restore command</span></span>

<span data-ttu-id="83dbe-124">서버를 복원하려면 Azure CLI 명령 프롬프트에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-124">To restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="83dbe-125">`az postgres server restore` 명령에는 다음과 같은 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-125">The `az postgres server restore` command requires the following parameters:</span></span>
| <span data-ttu-id="83dbe-126">설정</span><span class="sxs-lookup"><span data-stu-id="83dbe-126">Setting</span></span> | <span data-ttu-id="83dbe-127">제안 값</span><span class="sxs-lookup"><span data-stu-id="83dbe-127">Suggested value</span></span> | <span data-ttu-id="83dbe-128">설명</span><span class="sxs-lookup"><span data-stu-id="83dbe-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="83dbe-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="83dbe-129">resource-group</span></span> |  <span data-ttu-id="83dbe-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="83dbe-130">myResourceGroup</span></span> |  <span data-ttu-id="83dbe-131">원본 서버가 있는 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-131">The resource group where the source server exists.</span></span>  |
| <span data-ttu-id="83dbe-132">name</span><span class="sxs-lookup"><span data-stu-id="83dbe-132">name</span></span> | <span data-ttu-id="83dbe-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="83dbe-133">mypgserver-restored</span></span> | <span data-ttu-id="83dbe-134">복원 명령에 의해 만들어진 새 서버의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-134">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="83dbe-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="83dbe-135">restore-point-in-time</span></span> | <span data-ttu-id="83dbe-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="83dbe-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="83dbe-137">복원할 특정 시점을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-137">Select a point in time to restore to.</span></span> <span data-ttu-id="83dbe-138">이 날짜 및 시간은 원본 서버의 백업 보존 기간 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-138">This date and time must be within the source server's back up retention period.</span></span> <span data-ttu-id="83dbe-139">ISO8601 날자 및 시간 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-139">Use the ISO8601 date and time format.</span></span> <span data-ttu-id="83dbe-140">예를 들어 `2017-04-13T05:59:00-08:00`과 같이 현지 표준 시간대를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="83dbe-141">UTC Zulu 형식을 사용할 수도 있습니다(예: `2017-04-13T13:59:00Z`).</span><span class="sxs-lookup"><span data-stu-id="83dbe-141">You can also use the UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="83dbe-142">source-server</span><span class="sxs-lookup"><span data-stu-id="83dbe-142">source-server</span></span> | <span data-ttu-id="83dbe-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="83dbe-143">mypgserver-20170401</span></span> | <span data-ttu-id="83dbe-144">복원을 수행하려는 원본 서버의 이름 또는 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-144">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="83dbe-145">서버를 이전 특정 시점으로 복원하는 경우 새 서버가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-145">When you restore a server to an earlier point in time, a new server is created.</span></span> <span data-ttu-id="83dbe-146">지정된 특정 시점의 원본 서버 및 해당 데이터베이스가 새 서버에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-146">The original server and its databases from the specified point in time are copied to the new server.</span></span>

<span data-ttu-id="83dbe-147">복원된 서버에 대한 위치 및 가격 책정 계층 값은 원본 서버와 같게 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-147">The location and pricing tier values for the restored server remain the same as the original server.</span></span> 

<span data-ttu-id="83dbe-148">`az postgres server restore` 명령은 동기식입니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-148">The `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="83dbe-149">서버가 복원된 후 다른 특정 시점에 대해 이 프로세스를 반복하기 위해 이 서버를 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-149">After the server is restored, you can use it again to repeat the process for a different point in time.</span></span> 

<span data-ttu-id="83dbe-150">복원 프로세스가 완료된 후 새 서버를 찾아 데이터가 예상대로 복원되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="83dbe-150">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83dbe-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="83dbe-151">Next steps</span></span>
[<span data-ttu-id="83dbe-152">PostgreSQL용 Azure Database에 대한 연결 라이브러리</span><span class="sxs-lookup"><span data-stu-id="83dbe-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
