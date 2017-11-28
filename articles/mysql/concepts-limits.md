---
title: "MySQL에 대 한 Azure 데이터베이스에서 aaaLimitations | Microsoft Docs"
description: "MySQL용 Azure 데이터베이스의 미리 보기 제한 사항을 설명합니다."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="90ec2-103">MySQL용 Azure 데이터베이스의 제한 사항(미리 보기)</span><span class="sxs-lookup"><span data-stu-id="90ec2-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="90ec2-104">MySQL 서비스에 대 한 hello Azure 데이터베이스는 공개 프리뷰 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="90ec2-105">hello 다음 단원에서는 용량 및 hello 데이터베이스 서비스의 기능 제한.</span><span class="sxs-lookup"><span data-stu-id="90ec2-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="90ec2-106">서비스 계층 최대값</span><span class="sxs-lookup"><span data-stu-id="90ec2-106">Service Tier Maximums</span></span>
<span data-ttu-id="90ec2-107">MySQL용 Azure 데이터베이스에는 서버를 만들 때 선택할 수 있는 여러 서비스 계층이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="90ec2-108">자세한 내용은 [각 서비스 계층에서 사용할 수 있는 기능 이해](concepts-service-tiers.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="90ec2-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="90ec2-109">최대 수는 연결, 계산 단위 및 각 서비스 계층에 있는 저장소의 hello 서비스 미리 보기 중에 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="90ec2-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="90ec2-110">**최대 연결**</span><span class="sxs-lookup"><span data-stu-id="90ec2-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="90ec2-111">기본 50 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="90ec2-112">50개 연결</span><span class="sxs-lookup"><span data-stu-id="90ec2-112">50 connections</span></span>    |
| <span data-ttu-id="90ec2-113">기본 100 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="90ec2-114">100개 연결</span><span class="sxs-lookup"><span data-stu-id="90ec2-114">100 connections</span></span>   |
| <span data-ttu-id="90ec2-115">표준 100 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="90ec2-116">200개 연결</span><span class="sxs-lookup"><span data-stu-id="90ec2-116">200 connections</span></span>   |
| <span data-ttu-id="90ec2-117">표준 200 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="90ec2-118">300개 연결</span><span class="sxs-lookup"><span data-stu-id="90ec2-118">300 connections</span></span>   |
| <span data-ttu-id="90ec2-119">표준 400 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="90ec2-120">400개 연결</span><span class="sxs-lookup"><span data-stu-id="90ec2-120">400 connections</span></span>   |
| <span data-ttu-id="90ec2-121">표준 800 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="90ec2-122">500개 연결</span><span class="sxs-lookup"><span data-stu-id="90ec2-122">500 connections</span></span>   |
| <span data-ttu-id="90ec2-123">**최대 Compute 단위**</span><span class="sxs-lookup"><span data-stu-id="90ec2-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="90ec2-124">기본 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="90ec2-124">Basic service tier</span></span>         | <span data-ttu-id="90ec2-125">100 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-125">100 Compute Units</span></span> |
| <span data-ttu-id="90ec2-126">표준 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="90ec2-126">Standard service tier</span></span>      | <span data-ttu-id="90ec2-127">800 Compute 단위</span><span class="sxs-lookup"><span data-stu-id="90ec2-127">800 Compute Units</span></span> |
| <span data-ttu-id="90ec2-128">**최대 저장소**</span><span class="sxs-lookup"><span data-stu-id="90ec2-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="90ec2-129">기본 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="90ec2-129">Basic service tier</span></span>         | <span data-ttu-id="90ec2-130">1TB</span><span class="sxs-lookup"><span data-stu-id="90ec2-130">1 TB</span></span>              |
| <span data-ttu-id="90ec2-131">표준 서비스 계층</span><span class="sxs-lookup"><span data-stu-id="90ec2-131">Standard service tier</span></span>      | <span data-ttu-id="90ec2-132">1TB</span><span class="sxs-lookup"><span data-stu-id="90ec2-132">1 TB</span></span>              |

<span data-ttu-id="90ec2-133">너무 많은 연결이 도달 하면 hello 다음 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="90ec2-134">오류 1040(08004): 너무 많은 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="90ec2-135">미리 보기 기능 제한 사항:</span><span class="sxs-lookup"><span data-stu-id="90ec2-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="90ec2-136">크기 조정 작업:</span><span class="sxs-lookup"><span data-stu-id="90ec2-136">Scale operations:</span></span>
1.  <span data-ttu-id="90ec2-137">서비스 계층 간 서버의 동적 크기 조정은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="90ec2-138">즉, 기본 및 표준 서비스 계층 간 전환은 가능하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="90ec2-139">미리 생성된 서버에서 필요 시 저장소의 동적 증가는 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="90ec2-140">서버 저장소 크기를 줄이는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="90ec2-141">서버 버전 업그레이드:</span><span class="sxs-lookup"><span data-stu-id="90ec2-141">Server version upgrades:</span></span>
- <span data-ttu-id="90ec2-142">주 데이터베이스 엔진 버전 간에 자동화된 마이그레이션은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="90ec2-143">구독 관리:</span><span class="sxs-lookup"><span data-stu-id="90ec2-143">Subscription management:</span></span>
- <span data-ttu-id="90ec2-144">구독 및 리소스 그룹에서 미리 생성된 서버를 동적으로 이동하는 것은 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="90ec2-145">특정 시점 복원:</span><span class="sxs-lookup"><span data-stu-id="90ec2-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="90ec2-146">Toodifferent 서비스 계층 및/또는 계산 단위 및 저장소 크기 복원이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="90ec2-147">삭제된 서버를 복원하는 것은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="90ec2-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90ec2-148">다음 단계:</span><span class="sxs-lookup"><span data-stu-id="90ec2-148">Next Steps:</span></span>
<span data-ttu-id="90ec2-149">[각 서비스 계층에서 사용할 수 있는 기능](concepts-service-tiers.md)
[지원되는 MySQL Database 버전](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="90ec2-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
