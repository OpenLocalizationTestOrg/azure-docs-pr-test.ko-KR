---
title: "PostgreSQL용 Azure 데이터베이스의 제한 사항 | Microsoft Docs"
description: "PostgreSQL용 Azure 데이터베이스의 제한 사항을 설명합니다."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: 38988fc5c0dc05331ea078534cd1a05e9eca2493
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="b3cc9-103">PostgreSQL용 Azure 데이터베이스의 제한 사항</span><span class="sxs-lookup"><span data-stu-id="b3cc9-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="b3cc9-104">PostgreSQL용 Azure 데이터베이스 서비스는 공개 미리 보기 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-104">The Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="b3cc9-105">다음 섹션에서는 데이터베이스 서비스의 용량 및 기능 제한에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="b3cc9-106">서비스 계층 최대값</span><span class="sxs-lookup"><span data-stu-id="b3cc9-106">Service Tier Maximums</span></span>
<span data-ttu-id="b3cc9-107">PostgreSQL용 Azure 데이터베이스에는 서버를 만들 때 선택할 수 있는 여러 서비스 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="b3cc9-108">자세한 내용은 [각 서비스 계층에서 사용할 수 있는 기능 이해](concepts-service-tiers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="b3cc9-109">다음과 같이 서비스 미리 보기 동안 각 서비스 계층에는 연결, Compute 단위 및 저장소의 최대 수가 지정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="b3cc9-110">**최대 연결**</span><span class="sxs-lookup"><span data-stu-id="b3cc9-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="b3cc9-111">기본 50 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="b3cc9-112">50개 연결</span><span class="sxs-lookup"><span data-stu-id="b3cc9-112">50 connections</span></span>    |
| <span data-ttu-id="b3cc9-113">기본 100 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="b3cc9-114">100개 연결</span><span class="sxs-lookup"><span data-stu-id="b3cc9-114">100 connections</span></span>   |
| <span data-ttu-id="b3cc9-115">표준 100 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="b3cc9-116">200개 연결</span><span class="sxs-lookup"><span data-stu-id="b3cc9-116">200 connections</span></span>   |
| <span data-ttu-id="b3cc9-117">표준 200 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="b3cc9-118">300개 연결</span><span class="sxs-lookup"><span data-stu-id="b3cc9-118">300 connections</span></span>   |
| <span data-ttu-id="b3cc9-119">표준 400 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="b3cc9-120">400개 연결</span><span class="sxs-lookup"><span data-stu-id="b3cc9-120">400 connections</span></span>   |
| <span data-ttu-id="b3cc9-121">표준 800 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="b3cc9-122">500개 연결</span><span class="sxs-lookup"><span data-stu-id="b3cc9-122">500 connections</span></span>   |
| <span data-ttu-id="b3cc9-123">**최대 Compute 단위**</span><span class="sxs-lookup"><span data-stu-id="b3cc9-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="b3cc9-124">기본 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="b3cc9-124">Basic service tier</span></span>         | <span data-ttu-id="b3cc9-125">100 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-125">100 Compute Units</span></span> |
| <span data-ttu-id="b3cc9-126">표준 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="b3cc9-126">Standard service tier</span></span>      | <span data-ttu-id="b3cc9-127">800 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="b3cc9-127">800 Compute Units</span></span> |
| <span data-ttu-id="b3cc9-128">**최대 저장소**</span><span class="sxs-lookup"><span data-stu-id="b3cc9-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="b3cc9-129">기본 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="b3cc9-129">Basic service tier</span></span>         | <span data-ttu-id="b3cc9-130">1TB</span><span class="sxs-lookup"><span data-stu-id="b3cc9-130">1 TB</span></span>              |
| <span data-ttu-id="b3cc9-131">표준 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="b3cc9-131">Standard service tier</span></span>      | <span data-ttu-id="b3cc9-132">1TB</span><span class="sxs-lookup"><span data-stu-id="b3cc9-132">1 TB</span></span>              |

<span data-ttu-id="b3cc9-133">너무 많은 연결에 도달하면 다음 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="b3cc9-134">오류: 너무 많은 클라이언트가 이미 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="b3cc9-135">미리 보기 기능 제한 사항</span><span class="sxs-lookup"><span data-stu-id="b3cc9-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="b3cc9-136">크기 조정 작업</span><span class="sxs-lookup"><span data-stu-id="b3cc9-136">Scale operations</span></span>
1.  <span data-ttu-id="b3cc9-137">서비스 계층 간 서버의 동적 크기 조정은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="b3cc9-138">즉, 기본 및 표준 서비스 계층 간 전환은 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="b3cc9-139">미리 생성된 서버에서 필요 시 저장소의 동적 증가는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="b3cc9-140">서버 저장소 크기를 줄이는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="b3cc9-141">서버 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="b3cc9-141">Server version upgrades</span></span>
- <span data-ttu-id="b3cc9-142">주 데이터베이스 엔진 버전 간에 자동화된 마이그레이션은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="b3cc9-143">구독 관리</span><span class="sxs-lookup"><span data-stu-id="b3cc9-143">Subscription management</span></span>
- <span data-ttu-id="b3cc9-144">구독 및 리소스 그룹에서 미리 생성된 서버를 동적으로 이동하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="b3cc9-145">특정 시점 복원</span><span class="sxs-lookup"><span data-stu-id="b3cc9-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="b3cc9-146">다른 서비스 계층 및/또는 Compute 단위 및 저장소 크기로 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="b3cc9-147">삭제된 서버를 복원하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b3cc9-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3cc9-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b3cc9-148">Next steps</span></span>
- <span data-ttu-id="b3cc9-149">[각 가격 책정 계층에서 사용할 수 있는 기능](concepts-service-tiers.md) 이해</span><span class="sxs-lookup"><span data-stu-id="b3cc9-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="b3cc9-150">[지원되는 PostgreSQL Database 버전](concepts-supported-versions.md) 이해</span><span class="sxs-lookup"><span data-stu-id="b3cc9-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="b3cc9-151">[Azure Portal을 사용하여 PostgreSQL용 Azure 데이터베이스에서 서버를 백업 및 복원하는 방법](howto-restore-server-portal.md) 검토</span><span class="sxs-lookup"><span data-stu-id="b3cc9-151">Review [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md)</span></span>
