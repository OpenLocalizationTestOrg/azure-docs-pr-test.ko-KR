---
title: "aaaMove Azure 리소스 toonew 구독 또는 리소스 그룹이 | Microsoft Docs"
description: "Azure 리소스 관리자 toomove 리소스 tooa 새 리소스 그룹이 나 구독을 사용 합니다."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: tomfitz
ms.openlocfilehash: 09d35f0afbbcdc0c66779f98a982d878f0807497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-resources-toonew-resource-group-or-subscription"></a><span data-ttu-id="678da-103">구독 또는 리소스 toonew 리소스 그룹 이동</span><span class="sxs-lookup"><span data-stu-id="678da-103">Move resources toonew resource group or subscription</span></span>
<span data-ttu-id="678da-104">이 항목에서는 방법을 toomove 리소스 tooeither 새 구독 또는 새 리소스 그룹 hello에 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-104">This topic shows you how toomove resources tooeither a new subscription or a new resource group in hello same subscription.</span></span> <span data-ttu-id="678da-105">Hello 포털, PowerShell, Azure CLI 또는 hello REST API toomove 리소스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-105">You can use hello portal, PowerShell, Azure CLI, or hello REST API toomove resource.</span></span> <span data-ttu-id="678da-106">이 항목의 hello 이동 작업은 Azure 지원 담당자의 모든 지원 없이 사용할 수 있는 tooyou 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-106">hello move operations in this topic are available tooyou without any assistance from Azure support.</span></span>

<span data-ttu-id="678da-107">리소스를 이동할 때는 hello 소스 그룹과 hello 대상 그룹을 모두 hello 작업 동안 잠깁니다.</span><span class="sxs-lookup"><span data-stu-id="678da-107">When moving resources, both hello source group and hello target group are locked during hello operation.</span></span> <span data-ttu-id="678da-108">쓰기 및 삭제 작업 hello 이동이 완료 될 때까지 hello 리소스 그룹에서 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="678da-108">Write and delete operations are blocked on hello resource groups until hello move completes.</span></span> <span data-ttu-id="678da-109">이 잠금에는 의미가 hello 리소스가 고정 되어 있지만 추가, 업데이트 또는 hello 리소스 그룹에 리소스를 삭제할 수 없습니다 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-109">This lock means you cannot add, update, or delete resources in hello resource groups, but it does not mean hello resources are frozen.</span></span> <span data-ttu-id="678da-110">예를 들어 SQL Server와 데이터베이스 tooa 새 리소스 그룹을 이동 하면 hello 데이터베이스를 사용 하는 응용 프로그램에 가동 중지 시간 없이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-110">For example, if you move a SQL Server and its database tooa new resource group, an application that uses hello database experiences no downtime.</span></span> <span data-ttu-id="678da-111">여전히 읽기 및 toohello 데이터베이스 쓰기 수입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-111">It can still read and write toohello database.</span></span>

<span data-ttu-id="678da-112">Hello 리소스의 hello 위치를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-112">You cannot change hello location of hello resource.</span></span> <span data-ttu-id="678da-113">Tooa 새 리소스 그룹을 이동만 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-113">Moving a resource only moves it tooa new resource group.</span></span> <span data-ttu-id="678da-114">hello 새 리소스 그룹의 다른 위치를 할 수 있지만 hello 리소스의 hello 위치를 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-114">hello new resource group may have a different location, but that does not change hello location of hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="678da-115">이 문서에서는 기존 Azure 내에서 toomove 리소스 계정 라는 메시지가 나타나지 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-115">This article describes how toomove resources within an existing Azure account offering.</span></span> <span data-ttu-id="678da-116">리소스를 사용 하 여 기존 리소스와 toowork 줄이면서 (예: 종 량 제 toopre 지불에서 업그레이드)를 제공 하 여 Azure 계정 참조 하는 경우 실제로 원하는 toochange [Azure 구독 tooanother 제안을 전환](../billing/billing-how-to-switch-azure-offer.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-116">If you actually want toochange your Azure account offering (such as upgrading from pay-as-you-go toopre-pay) while continuing toowork with your existing resources, see [Switch your Azure subscription tooanother offer](../billing/billing-how-to-switch-azure-offer.md).</span></span>
>
>

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="678da-117">리소스를 이동하기 전의 검사 목록</span><span class="sxs-lookup"><span data-stu-id="678da-117">Checklist before moving resources</span></span>
<span data-ttu-id="678da-118">리소스 이동 하기 전에 몇 가지 중요 한 단계 tooperform이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-118">There are some important steps tooperform before moving a resource.</span></span> <span data-ttu-id="678da-119">이러한 조건을 확인하면 오류를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="678da-120">hello 원본 및 대상 구독 내에 있어야 hello 동일 [Azure Active Directory 테 넌 트](../active-directory/active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-120">hello source and destination subscriptions must exist within hello same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="678da-121">동일한 두 구독 hello가 toocheck 테 넌 트 ID, Azure PowerShell 또는 Azure CLI를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-121">toocheck that both subscriptions have hello same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="678da-122">Azure PowerShell의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="678da-123">Azure CLI 2.0의 경우 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="678da-124">Hello에 대 한 Id 테 넌 트 하는 경우 동일한 hello, hello 구독에 대 한 toochange hello 디렉터리를 시작할 수 있습니다. hello 원본 및 대상 구독 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-124">If hello tenant IDs for hello source and destination subscriptions are not hello same, you can attempt toochange hello directory for hello subscription.</span></span> <span data-ttu-id="678da-125">그러나이 옵션은 사용 가능한 tooService 관리자에 게 Microsoft 계정 (조직 계정이 아님)로 로그인 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-125">However, this option is only available tooService Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="678da-126">tooattempt toohello 로그인 hello 디렉터리를 변경 하 고 [클래식 포털](https://manage.windowsazure.com/)를 선택 하 고 **설정**, hello 구독을 선택 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-126">tooattempt changing hello directory, log in toohello [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select hello subscription.</span></span> <span data-ttu-id="678da-127">경우 hello **디렉터리 편집** 아이콘을 사용할 수 있는 toochange 선택 hello Azure Active Directory에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-127">If hello **Edit Directory** icon is available, select it toochange hello associated Azure Active Directory.</span></span>

  ![디렉터리 편집](./media/resource-group-move-resources/edit-directory.png)

  <span data-ttu-id="678da-129">이 아이콘을 사용할 수 없는 경우 지원 toomove hello 리소스 tooa 새 테 넌 트에 게 문의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-129">If that icon is not available, you must contact support toomove hello resources tooa new tenant.</span></span>

2. <span data-ttu-id="678da-130">hello 서비스는 hello 기능 toomove 리소스 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-130">hello service must enable hello ability toomove resources.</span></span> <span data-ttu-id="678da-131">이 항목에서는 리소스 이동이 가능한 서비스와 그렇지 않은 서비스 목록을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="678da-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="678da-132">hello 대상 구독 hello 리소스 이동의 hello 리소스 공급자에 대 한 등록 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-132">hello destination subscription must be registered for hello resource provider of hello resource being moved.</span></span> <span data-ttu-id="678da-133">해당 hello 라는 오류가 나타나면 not, **리소스 종류에 대 한 구독이 등록 되지 않습니다**합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-133">If not, you receive an error stating that hello **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="678da-134">리소스 tooa 새 구독을 이동할 때이 문제를 발생할 수 있지만 해당 리소스 종류와 해당 구독 사용 되지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-134">You might encounter this problem when moving a resource tooa new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="678da-135">toolearn toocheck 등록 상태를 hello 및 리소스 공급자를 등록 하는 방법 참조 [리소스 공급자 및 형식](resource-manager-supported-services.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-135">toolearn how toocheck hello registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="when-toocall-support"></a><span data-ttu-id="678da-136">Toocall를 지 원하는 경우</span><span class="sxs-lookup"><span data-stu-id="678da-136">When toocall support</span></span>
<span data-ttu-id="678da-137">이 항목에 표시 된 hello 셀프 서비스 작업을 통해 가장 많은 리소스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-137">You can move most resources through hello self-service operations shown in this topic.</span></span> <span data-ttu-id="678da-138">Hello 셀프 서비스 작업을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-138">Use hello self-service operations to:</span></span>

* <span data-ttu-id="678da-139">Resource Manager 리소스를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="678da-140">클래식 리소스 toohello에 따라 이동 [클래식 배포 제한 사항](#classic-deployment-limitations)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-140">Move classic resources according toohello [classic deployment limitations](#classic-deployment-limitations).</span></span>

<span data-ttu-id="678da-141">다음을 수행해야 할 때 지원을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-141">Call support when you need to:</span></span>

* <span data-ttu-id="678da-142">리소스 tooa 새 Azure 계정 (및 Azure Active Directory 테 넌 트)를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-142">Move your resources tooa new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="678da-143">클래식 리소스를 이동 하지만 hello 제한 되는 동안 문제가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-143">Move classic resources but are having trouble with hello limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="678da-144">이동을 사용하는 서비스</span><span class="sxs-lookup"><span data-stu-id="678da-144">Services that enable move</span></span>
<span data-ttu-id="678da-145">지금은 이동 tooboth 새 리소스 그룹 및 구독을 사용할 수 있는 서비스는 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-145">For now, hello services that enable moving tooboth a new resource group and subscription are:</span></span>

* <span data-ttu-id="678da-146">API 관리</span><span class="sxs-lookup"><span data-stu-id="678da-146">API Management</span></span>
* <span data-ttu-id="678da-147">앱 서비스 앱(웹앱) - [앱 서비스 제한](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="678da-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="678da-148">Application Insights</span><span class="sxs-lookup"><span data-stu-id="678da-148">Application Insights</span></span>
* <span data-ttu-id="678da-149">자동화</span><span class="sxs-lookup"><span data-stu-id="678da-149">Automation</span></span>
* <span data-ttu-id="678da-150">배치</span><span class="sxs-lookup"><span data-stu-id="678da-150">Batch</span></span>
* <span data-ttu-id="678da-151">Bing 지도</span><span class="sxs-lookup"><span data-stu-id="678da-151">Bing Maps</span></span>
* <span data-ttu-id="678da-152">CDN</span><span class="sxs-lookup"><span data-stu-id="678da-152">CDN</span></span>
* <span data-ttu-id="678da-153">클라우드 서비스 - [클래식 배포 제한 사항](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="678da-153">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="678da-154">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="678da-154">Cognitive Services</span></span>
* <span data-ttu-id="678da-155">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="678da-155">Content Moderator</span></span>
* <span data-ttu-id="678da-156">데이터 카탈로그</span><span class="sxs-lookup"><span data-stu-id="678da-156">Data Catalog</span></span>
* <span data-ttu-id="678da-157">데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="678da-157">Data Factory</span></span>
* <span data-ttu-id="678da-158">데이터 레이크 분석</span><span class="sxs-lookup"><span data-stu-id="678da-158">Data Lake Analytics</span></span>
* <span data-ttu-id="678da-159">데이터 레이크 저장소</span><span class="sxs-lookup"><span data-stu-id="678da-159">Data Lake Store</span></span>
* <span data-ttu-id="678da-160">DNS</span><span class="sxs-lookup"><span data-stu-id="678da-160">DNS</span></span>
* <span data-ttu-id="678da-161">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="678da-161">Azure Cosmos DB</span></span>
* <span data-ttu-id="678da-162">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="678da-162">Event Hubs</span></span>
* <span data-ttu-id="678da-163">HDInsight 클러스터 - [HDInsight 제한 사항](#hdinsight-limitations) 참조</span><span class="sxs-lookup"><span data-stu-id="678da-163">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="678da-164">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="678da-164">IoT Hubs</span></span>
* <span data-ttu-id="678da-165">키 자격 증명 모음</span><span class="sxs-lookup"><span data-stu-id="678da-165">Key Vault</span></span>
* <span data-ttu-id="678da-166">부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="678da-166">Load Balancers</span></span>
* <span data-ttu-id="678da-167">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="678da-167">Logic Apps</span></span>
* <span data-ttu-id="678da-168">기계 학습</span><span class="sxs-lookup"><span data-stu-id="678da-168">Machine Learning</span></span>
* <span data-ttu-id="678da-169">미디어 서비스</span><span class="sxs-lookup"><span data-stu-id="678da-169">Media Services</span></span>
* <span data-ttu-id="678da-170">모바일 고객 관리</span><span class="sxs-lookup"><span data-stu-id="678da-170">Mobile Engagement</span></span>
* <span data-ttu-id="678da-171">알림 허브</span><span class="sxs-lookup"><span data-stu-id="678da-171">Notification Hubs</span></span>
* <span data-ttu-id="678da-172">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="678da-172">Operational Insights</span></span>
* <span data-ttu-id="678da-173">운영 관리</span><span class="sxs-lookup"><span data-stu-id="678da-173">Operations Management</span></span>
* <span data-ttu-id="678da-174">Power BI</span><span class="sxs-lookup"><span data-stu-id="678da-174">Power BI</span></span>
* <span data-ttu-id="678da-175">Redis 캐시</span><span class="sxs-lookup"><span data-stu-id="678da-175">Redis Cache</span></span>
* <span data-ttu-id="678da-176">스케줄러</span><span class="sxs-lookup"><span data-stu-id="678da-176">Scheduler</span></span>
* <span data-ttu-id="678da-177">검색</span><span class="sxs-lookup"><span data-stu-id="678da-177">Search</span></span>
* <span data-ttu-id="678da-178">서버 관리</span><span class="sxs-lookup"><span data-stu-id="678da-178">Server Management</span></span>
* <span data-ttu-id="678da-179">서비스 버스</span><span class="sxs-lookup"><span data-stu-id="678da-179">Service Bus</span></span>
* <span data-ttu-id="678da-180">서비스 패브릭</span><span class="sxs-lookup"><span data-stu-id="678da-180">Service Fabric</span></span>
* <span data-ttu-id="678da-181">저장소</span><span class="sxs-lookup"><span data-stu-id="678da-181">Storage</span></span>
* <span data-ttu-id="678da-182">저장소(클래식) - [클래식 배포 제한 사항](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="678da-182">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="678da-183">Stream Analytics - 실행 중 상태일 때는 Stream Analytics 작업을 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-183">Stream Analytics - Stream Analytics jobs cannot be moved when in running state.</span></span>
* <span data-ttu-id="678da-184">SQL 데이터베이스 서버-hello 데이터베이스 및 서버에에서 있어야 hello 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-184">SQL Database server - hello database and server must reside in hello same resource group.</span></span> <span data-ttu-id="678da-185">SQL Server를 이동하면 모든 해당 데이터베이스도 함께 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-185">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="678da-186">트래픽 관리자</span><span class="sxs-lookup"><span data-stu-id="678da-186">Traffic Manager</span></span>
* <span data-ttu-id="678da-187">가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="678da-187">Virtual Machines</span></span>
* <span data-ttu-id="678da-188">주요 자격 증명 모음-toonew 같은 구독에서 리소스 그룹 이동에에서 저장 된 인증서로 가상 컴퓨터를 사용 하지만 구독 간 이동 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-188">Virtual Machines with certificate stored in Key Vault - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="678da-189">가상 컴퓨터(클래식) - [클래식 배포 제한 사항](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="678da-189">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="678da-190">가상 컴퓨터 확장 집합</span><span class="sxs-lookup"><span data-stu-id="678da-190">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="678da-191">Virtual Networks - 현재 피어링된 Virtual Network는 VNet 피어링을 사용하지 않도록 설정할 때까지 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-191">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="678da-192">한 번 해제, 가상 네트워크를 성공적으로 이동할 수 있는 hello 그리고 hello VNet 피어 링을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-192">Once disabled, hello Virtual Network can be moved successfully and hello VNet peering can be enabled.</span></span> <span data-ttu-id="678da-193">또한 가상 네트워크는 hello 가상 네트워크에 어떤 서브넷 리소스 탐색 링크로 포함 된 경우 이동된 tooa 다른 구독 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-193">In addition, a Virtual Network cannot be moved tooa different subscription if hello Virtual Network contains any subnet with resource navigation links.</span></span> <span data-ttu-id="678da-194">예를 들어, Virtual Network 서브넷은 Microsoft.Cache redis 리소스가 이 서브넷에 배포된 경우 리소스 탐색 링크를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-194">For example, a Virtual Network subnet has a resource navigation link when a Microsoft.Cache redis resource is deployed into this subnet.</span></span>
* <span data-ttu-id="678da-195">VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="678da-195">VPN Gateway</span></span>


## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="678da-196">이동을 사용하지 않는 서비스</span><span class="sxs-lookup"><span data-stu-id="678da-196">Services that do not enable move</span></span>
<span data-ttu-id="678da-197">현재 사용 하지 않는 리소스를 이동 하는 hello 서비스는 같습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-197">hello services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="678da-198">AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="678da-198">AD Domain Services</span></span>
* <span data-ttu-id="678da-199">AD 하이브리드 상태 관리 서비스</span><span class="sxs-lookup"><span data-stu-id="678da-199">AD Hybrid Health Service</span></span>
* <span data-ttu-id="678da-200">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="678da-200">Application Gateway</span></span>
* <span data-ttu-id="678da-201">Managed Disks를 포함하는 Virtual Machines의 가용성 집합</span><span class="sxs-lookup"><span data-stu-id="678da-201">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="678da-202">BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="678da-202">BizTalk Services</span></span>
* <span data-ttu-id="678da-203">컨테이너 서비스</span><span class="sxs-lookup"><span data-stu-id="678da-203">Container Service</span></span>
* <span data-ttu-id="678da-204">Express 경로</span><span class="sxs-lookup"><span data-stu-id="678da-204">Express Route</span></span>
* <span data-ttu-id="678da-205">DevTest Labs-toonew 같은 구독에서 리소스 그룹 이동을 사용할 수 있지만 상호 구독 이동 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-205">DevTest Labs - Move toonew resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="678da-206">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="678da-206">Dynamics LCS</span></span>
* <span data-ttu-id="678da-207">Managed Disks에서 만든 이미지</span><span class="sxs-lookup"><span data-stu-id="678da-207">Images created from Managed Disks</span></span>
* <span data-ttu-id="678da-208">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="678da-208">Managed Disks</span></span>
* <span data-ttu-id="678da-209">Managed Applications</span><span class="sxs-lookup"><span data-stu-id="678da-209">Managed Applications</span></span>
* <span data-ttu-id="678da-210">복구 서비스 자격 증명 모음-하지 hello 계산, 네트워크 및 저장소 리소스 이동 연관지 않습니다 복구 서비스를 hello도 자격 증명 모음을 참조 하십시오. [복구 서비스 제한 사항](#recovery-services-limitations)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-210">Recovery Services vault - also do not move hello Compute, Network, and Storage resources associated with hello Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="678da-211">보안</span><span class="sxs-lookup"><span data-stu-id="678da-211">Security</span></span>
* <span data-ttu-id="678da-212">Managed Disks에서 만든 스냅숏</span><span class="sxs-lookup"><span data-stu-id="678da-212">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="678da-213">StorSimple 장치 관리자</span><span class="sxs-lookup"><span data-stu-id="678da-213">StorSimple Device Manager</span></span>
* <span data-ttu-id="678da-214">Managed Disks를 포함하는 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="678da-214">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="678da-215">가상 네트가상 네트워크(클래식) - [클래식 배포 제한 사항](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="678da-215">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="678da-216">Marketplace 리소스에서 만든 Virtual Machines는 구독 간에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-216">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="678da-217">리소스 toobe hello 현재 구독에 프로 비전을 해제 하 고 hello 새 구독에 다시 배포할 필요</span><span class="sxs-lookup"><span data-stu-id="678da-217">Resource needs toobe deprovisioned in hello current subscription and deployed again in hello new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="678da-218">앱 서비스 제한</span><span class="sxs-lookup"><span data-stu-id="678da-218">App Service limitations</span></span>
<span data-ttu-id="678da-219">앱 서비스 앱으로 작업할 경우에는 앱 서비스 계획만 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-219">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="678da-220">옵션은 toomove 앱 서비스 앱:</span><span class="sxs-lookup"><span data-stu-id="678da-220">toomove App Service apps, your options are:</span></span>

* <span data-ttu-id="678da-221">해당 리소스 그룹 tooa 새 리소스 그룹에 없는 응용 프로그램 서비스 리소스 hello 앱 서비스 계획 및 다른 모든 앱 서비스 리소스를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-221">Move hello App Service plan and all other App Service resources in that resource group tooa new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="678da-222">이 요구 사항은 이동 해야 하는 방법에는 응용 프로그램 서비스 리소스 hello 연결 되지 않은 앱 서비스 계획 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-222">This requirement means you must move even hello App Service resources that are not associated with hello App Service plan.</span></span>
* <span data-ttu-id="678da-223">Hello 앱 tooa 다른 리소스 그룹을 이동 하지만 hello 원본 리소스 그룹에 모든 앱 서비스 계획을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-223">Move hello apps tooa different resource group, but keep all App Service plans in hello original resource group.</span></span>

<span data-ttu-id="678da-224">hello 앱 서비스 계획에서 tooreside 않아도 hello 앱 toofunction hello에 대 한 hello 응용 프로그램으로 동일한 리소스 그룹 올바르게 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-224">hello App Service plan does not need tooreside in hello same resource group as hello app for hello app toofunction correctly.</span></span>

<span data-ttu-id="678da-225">예를 들어 리소스 그룹에 다음 사항이 포함된 경우:</span><span class="sxs-lookup"><span data-stu-id="678da-225">For example, if your resource group contains:</span></span>

* <span data-ttu-id="678da-226">**plan-a**와 연결된 **web-a**</span><span class="sxs-lookup"><span data-stu-id="678da-226">**web-a** which is associated with **plan-a**</span></span>
* <span data-ttu-id="678da-227">**plan-b**와 연결된 **web-b**</span><span class="sxs-lookup"><span data-stu-id="678da-227">**web-b** which is associated with **plan-b**</span></span>

<span data-ttu-id="678da-228">옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-228">Your options are:</span></span>

* <span data-ttu-id="678da-229">**web-a**, **plan-a**, **web-b** 및 **plan-b** 이동</span><span class="sxs-lookup"><span data-stu-id="678da-229">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="678da-230">**web-a** 및 **web-b** 이동</span><span class="sxs-lookup"><span data-stu-id="678da-230">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="678da-231">**web-a**</span><span class="sxs-lookup"><span data-stu-id="678da-231">Move **web-a**</span></span>
* <span data-ttu-id="678da-232">**web-b**</span><span class="sxs-lookup"><span data-stu-id="678da-232">Move **web-b**</span></span>

<span data-ttu-id="678da-233">다른 모든 조합에는 App Service 계획 이동 시 그대로 남겨 둘 수 없는 리소스 형식(App Service 리소스 형식)을 남겨두는 것이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-233">All other combinations involve leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="678da-234">를 웹 앱의 앱 서비스 계획 보다 다른 리소스 그룹에 상주 하지만 toomove tooa 새 리소스 그룹 모두를 원하는 경우에 두 단계로 hello 이동을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-234">If your web app resides in a different resource group than its App Service plan but you want toomove both tooa new resource group, you must perform hello move in two steps.</span></span> <span data-ttu-id="678da-235">예:</span><span class="sxs-lookup"><span data-stu-id="678da-235">For example:</span></span>

* <span data-ttu-id="678da-236">**web-a**가 **web-group**에 상주하는 경우</span><span class="sxs-lookup"><span data-stu-id="678da-236">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="678da-237">**plan-a**가 **plan-group**에 상주하는 경우</span><span class="sxs-lookup"><span data-stu-id="678da-237">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="678da-238">원하는 **웹 a** 및 **계획 a** 에 tooreside **결합 그룹**</span><span class="sxs-lookup"><span data-stu-id="678da-238">You want **web-a** and **plan-a** tooreside in **combined-group**</span></span>

<span data-ttu-id="678da-239">tooaccomplish이 이동, 순서 따르면 hello에서 두 개의 별도 이동 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-239">tooaccomplish this move, perform two separate move operations in hello following sequence:</span></span>

1. <span data-ttu-id="678da-240">Hello 이동 **웹 a** 너무**그룹 계획**</span><span class="sxs-lookup"><span data-stu-id="678da-240">Move hello **web-a** too**plan-group**</span></span>
2. <span data-ttu-id="678da-241">이동 **웹 a** 및 **계획 a** 너무**결합 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-241">Move **web-a** and **plan-a** too**combined-group**.</span></span>

<span data-ttu-id="678da-242">앱 서비스 인증서 tooa 새 리소스 그룹 또는 아무 문제 없이 구독을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-242">You can move an App Service Certificate tooa new resource group or subscription without any issues.</span></span> <span data-ttu-id="678da-243">그러나 웹 응용 프로그램 외부에서 구매한 toohello 앱을 업로드 하는 SSL 인증서가 포함 된 경우 이동 hello 웹 응용 프로그램 하기 전에 hello 인증서를 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-243">However, if your web app includes an SSL certificate that you purchased externally and uploaded toohello app, you must delete hello certificate before moving hello web app.</span></span> <span data-ttu-id="678da-244">예를 들어 hello 다음 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-244">For example, you can perform hello following steps:</span></span>

1. <span data-ttu-id="678da-245">Hello 웹 앱에서 업로드 하는 hello 인증서를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-245">Delete hello uploaded certificate from hello web app</span></span>
2. <span data-ttu-id="678da-246">Hello 웹 응용 프로그램 이동</span><span class="sxs-lookup"><span data-stu-id="678da-246">Move hello web app</span></span>
3. <span data-ttu-id="678da-247">웹 응용 프로그램을 toohello hello 인증서 업로드</span><span class="sxs-lookup"><span data-stu-id="678da-247">Upload hello certificate toohello web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="678da-248">Recovery Services 제한 사항</span><span class="sxs-lookup"><span data-stu-id="678da-248">Recovery Services limitations</span></span>
<span data-ttu-id="678da-249">저장소, 네트워크에 대 한 이동 가능 하지 또는 계산 리소스는 Azure Site Recovery와 tooset 재해 복구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-249">Move is not enabled for Storage, Network, or Compute resources used tooset up disaster recovery with Azure Site Recovery.</span></span>

<span data-ttu-id="678da-250">예를 들어 온-프레미스 컴퓨터 tooa 저장소 계정 (Storage1)의 복제 설정 가정 하 고 hello 보호 된 컴퓨터 toocome를 tooAzure 장애 조치 후 가상 컴퓨터 (v m 1) (네트워크 1) tooa 가상 네트워크를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-250">For example, suppose you have set up replication of your on-premises machines tooa storage account (Storage1) and want hello protected machine toocome up after failover tooAzure as a virtual machine (VM1) attached tooa virtual network (Network1).</span></span> <span data-ttu-id="678da-251">이러한 Azure 리소스가-VM1, Storage1 이동할 수 없습니다 및 네트워크 1-리소스 간에 그룹 hello 내에서 동일한 구독 또는 구독 전반에 걸쳐 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-251">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within hello same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="678da-252">HDInsight 제한 사항</span><span class="sxs-lookup"><span data-stu-id="678da-252">HDInsight limitations</span></span>

<span data-ttu-id="678da-253">HDInsight 클러스터 tooa 새 구독 또는 리소스 그룹을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-253">You can move HDInsight clusters tooa new subscription or resource group.</span></span> <span data-ttu-id="678da-254">그러나 구독 hello 네트워킹 리소스 (예: hello 가상 네트워크, NIC 또는 부하 분산 장치) HDInsight 클러스터를 연결 된 toohello 간에 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-254">However, you cannot move across subscriptions hello networking resources linked toohello HDInsight cluster (such as hello virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="678da-255">또한 tooa 새 리소스 그룹 hello 클러스터에 대 한 연결 된 tooa 가상 컴퓨터가 있는 NIC를 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-255">In addition, you cannot move tooa new resource group a NIC that is attached tooa virtual machine for hello cluster.</span></span>

<span data-ttu-id="678da-256">HDInsight 클러스터 tooa 새 구독을 이동할 때 먼저 다른 리소스 (예: hello 저장소 계정)를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-256">When moving an HDInsight cluster tooa new subscription, first move other resources (like hello storage account).</span></span> <span data-ttu-id="678da-257">그런 다음 자체적으로 hello HDInsight 클러스터를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-257">Then, move hello HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="678da-258">클래식 배포 제한 사항</span><span class="sxs-lookup"><span data-stu-id="678da-258">Classic deployment limitations</span></span>
<span data-ttu-id="678da-259">hello hello 클래식 모델을 통해 배포 된 리소스를 이동 하기 위한 옵션에 따라 달라 hello 리소스 tooa 새 구독 또는 구독 내에서 이동 하려는 여부.</span><span class="sxs-lookup"><span data-stu-id="678da-259">hello options for moving resources deployed through hello classic model differ based on whether you are moving hello resources within a subscription or tooa new subscription.</span></span>

### <a name="same-subscription"></a><span data-ttu-id="678da-260">동일한 구독</span><span class="sxs-lookup"><span data-stu-id="678da-260">Same subscription</span></span>
<span data-ttu-id="678da-261">동일한 구독 제한에 따라 hello 적용 hello 내에서 한 리소스 그룹 tooanother 리소스 그룹에서 리소스를 이동할 때:</span><span class="sxs-lookup"><span data-stu-id="678da-261">When moving resources from one resource group tooanother resource group within hello same subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="678da-262">가상 네트워크(클래식)은 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-262">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="678da-263">Hello 클라우드 서비스와 가상 컴퓨터 (클래식)를 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-263">Virtual machines (classic) must be moved with hello cloud service.</span></span>
* <span data-ttu-id="678da-264">클라우드 서비스 hello 이동 모든 가상 컴퓨터를 포함 하는 경우에 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-264">Cloud service can only be moved when hello move includes all its virtual machines.</span></span>
* <span data-ttu-id="678da-265">한 번에 하나의 클라우드 서비스만 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-265">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="678da-266">한 번에 하나의 저장소 계정(클래식)만 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-266">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="678da-267">저장소 계정 (클래식) hello에서 이동할 수 없는 가상 컴퓨터 또는 클라우드 서비스와 동일한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-267">Storage account (classic) cannot be moved in hello same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="678da-268">toomove 클래식 리소스 tooa 새 리소스 그룹 내 동일한 구독 hello, hello 통해 hello 표준 이동 작업을 사용 하 여 [포털](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), 또는 [REST API](#use-rest-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-268">toomove classic resources tooa new resource group within hello same subscription, use hello standard move operations through hello [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="678da-269">사용 하면 리소스 관리자 리소스를 이동 하기 위한 사용 하 여 동일한 작업을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-269">You use hello same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="678da-270">새 구독</span><span class="sxs-lookup"><span data-stu-id="678da-270">New subscription</span></span>
<span data-ttu-id="678da-271">Tooa 새 구독 리소스를 이동할 때는 hello 다음 제한 사항이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="678da-271">When moving resources tooa new subscription, hello following restrictions apply:</span></span>

* <span data-ttu-id="678da-272">Hello에서 hello 구독에 있는 모든 클래식 리소스를 이동 해야 동일한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-272">All classic resources in hello subscription must be moved in hello same operation.</span></span>
* <span data-ttu-id="678da-273">hello 대상 구독에 다른 모든 클래식 리소스를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-273">hello target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="678da-274">hello 이동 클래식 이동에 대 한 별도 REST API를 통해 요청할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-274">hello move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="678da-275">클래식 리소스 tooa 새 구독을 이동할 때 hello 표준 리소스 관리자 이동 명령이 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-275">hello standard Resource Manager move commands do not work when moving classic resources tooa new subscription.</span></span>

<span data-ttu-id="678da-276">toomove 클래식 리소스 tooa 새 구독을 사용 하 여 hello REST 작업을 특정 tooclassic 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-276">toomove classic resources tooa new subscription, use hello REST operations that are specific tooclassic resources.</span></span> <span data-ttu-id="678da-277">나머지 toouse hello 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-277">toouse REST, perform hello following steps:</span></span>

1. <span data-ttu-id="678da-278">확인 원본 구독 hello 구독 간에에서 참여할 수 있습니다 하는 경우 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-278">Check if hello source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="678da-279">다음 작업 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-279">Use hello following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="678da-280">Hello 요청 본문에 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-280">In hello request body, include:</span></span>

  ```json
  {
    "role": "source"
  }
  ```

     <span data-ttu-id="678da-281">hello 유효성 검사 작업에 대 한 hello 응답 형식에 따라 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-281">hello response for hello validation operation is in hello following format:</span></span>

  ```json
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="678da-282">확인은 hello 대상 구독의 구독 간에에서 참여할 수 있는 경우 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-282">Check if hello destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="678da-283">다음 작업 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-283">Use hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="678da-284">Hello 요청 본문에 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-284">In hello request body, include:</span></span>

  ```json
  {
    "role": "target"
  }
  ```

     <span data-ttu-id="678da-285">hello 응답 hello hello 원본 구독 유효성 검사와 동일한 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-285">hello response is in hello same format as hello source subscription validation.</span></span>
3. <span data-ttu-id="678da-286">두 구독 유효성 검사를 통과 하는 경우 모든 클래식 리소스 하나의 구독만 tooanother 구독에서 작업 하는 hello로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-286">If both subscriptions pass validation, move all classic resources from one subscription tooanother subscription with hello following operation:</span></span>

  ```HTTP
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="678da-287">Hello 요청 본문에 다음을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-287">In hello request body, include:</span></span>

  ```json
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="678da-288">hello 작업은 몇 분 동안 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-288">hello operation may run for several minutes.</span></span>

## <a name="use-portal"></a><span data-ttu-id="678da-289">포털 사용</span><span class="sxs-lookup"><span data-stu-id="678da-289">Use portal</span></span>
<span data-ttu-id="678da-290">toomove 리소스 이러한 리소스를 포함 하는 hello 리소스 그룹을 선택 하 고 hello 선택 **이동** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-290">toomove resources, select hello resource group containing those resources, and then select hello **Move** button.</span></span>

![리소스 이동](./media/resource-group-move-resources/select-move.png)

<span data-ttu-id="678da-292">Hello 리소스 tooa 새 리소스 그룹이 나 새 구독을 이동 하는 지 여부를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-292">Select whether you are moving hello resources tooa new resource group or a new subscription.</span></span>

<span data-ttu-id="678da-293">Hello 리소스 toomove 및 hello 대상 리소스 그룹을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-293">Select hello resources toomove and hello destination resource group.</span></span> <span data-ttu-id="678da-294">이러한 리소스와 선택에 대 한 tooupdate 스크립트 할 승인 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-294">Acknowledge that you need tooupdate scripts for these resources and select **OK**.</span></span> <span data-ttu-id="678da-295">Hello 이전 단계에서 hello 편집 구독 아이콘을 선택한 경우 hello 대상 구독을 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-295">If you selected hello edit subscription icon in hello previous step, you must also select hello destination subscription.</span></span>

![대상 선택](./media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="678da-297">**알림**, 작업이 실행 되 고 이동 하는 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-297">In **Notifications**, you see that hello move operation is running.</span></span>

![이동 상태 표시](./media/resource-group-move-resources/show-status.png)

<span data-ttu-id="678da-299">완료 되 면 hello 결과 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="678da-299">When it has completed, you are notified of hello result.</span></span>

![이동 결과 표시](./media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="678da-301">PowerShell 사용</span><span class="sxs-lookup"><span data-stu-id="678da-301">Use PowerShell</span></span>
<span data-ttu-id="678da-302">toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 `Move-AzureRmResource` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-302">toomove existing resources tooanother resource group or subscription, use hello `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="678da-303">첫 번째 예제와 hello 방법을 toomove 한 리소스 tooa 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-303">hello first example shows how toomove one resource tooa new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="678da-304">hello 방법을 예제와 두 번째 toomove 여러 리소스 tooa 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-304">hello second example shows how toomove multiple resources tooa new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="678da-305">toomove tooa 새 구독을 hello에 대 한 값이 포함 `DestinationSubscriptionId` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-305">toomove tooa new subscription, include a value for hello `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="678da-306">요청 tooconfirm toomove hello 원하는 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-306">You are asked tooconfirm that you want toomove hello specified resources.</span></span>

```powershell
Confirm
Are you sure you want toomove these resources toohello resource group
'/subscriptions/{guid}/resourceGroups/newRG' hello resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="678da-307">Azure CLI 2.0 사용</span><span class="sxs-lookup"><span data-stu-id="678da-307">Use Azure CLI 2.0</span></span>
<span data-ttu-id="678da-308">toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 `az resource move` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-308">toomove existing resources tooanother resource group or subscription, use hello `az resource move` command.</span></span> <span data-ttu-id="678da-309">Hello 리소스 hello 리소스 toomove의 Id를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-309">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="678da-310">다음 명령을 hello로 리소스 Id를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-310">You can get resource IDs with hello following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="678da-311">다음 예제는 hello toomove 저장소 tooa 새 리소스 그룹을 고려 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="678da-311">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="678da-312">Hello에 `--ids` 매개 변수를 hello 리소스 Id toomove 공백으로 구분 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-312">In hello `--ids` parameter, provide a space-separated list of hello resource IDs toomove.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="678da-313">toomove tooa 새 구독을 hello 제공 `--destination-subscription-id` 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-313">toomove tooa new subscription, provide hello `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="678da-314">Azure CLI 1.0 사용</span><span class="sxs-lookup"><span data-stu-id="678da-314">Use Azure CLI 1.0</span></span>
<span data-ttu-id="678da-315">toomove 기존 리소스 tooanother 리소스 그룹이 나 hello를 사용 하 여 구독 `azure resource move` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="678da-315">toomove existing resources tooanother resource group or subscription, use hello `azure resource move` command.</span></span> <span data-ttu-id="678da-316">Hello 리소스 hello 리소스 toomove의 Id를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-316">Provide hello resource IDs of hello resources toomove.</span></span> <span data-ttu-id="678da-317">다음 명령을 hello로 리소스 Id를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678da-317">You can get resource IDs with hello following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="678da-318">반환 형식에 따라 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="678da-318">Which returns hello following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="678da-319">다음 예제는 hello toomove 저장소 tooa 새 리소스 그룹을 고려 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="678da-319">hello following example shows how toomove a storage account tooa new resource group.</span></span> <span data-ttu-id="678da-320">Hello에 `-i` 매개 변수를 hello 리소스 Id toomove 쉼표로 구분 된 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-320">In hello `-i` parameter, provide a comma-separated list of hello resource IDs toomove.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="678da-321">요청 tooconfirm toomove hello 원하는 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-321">You are asked tooconfirm that you want toomove hello specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="678da-322">REST API 사용</span><span class="sxs-lookup"><span data-stu-id="678da-322">Use REST API</span></span>
<span data-ttu-id="678da-323">toomove 기존 리소스 tooanother 리소스 그룹 또는 구독을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-323">toomove existing resources tooanother resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version}
```

<span data-ttu-id="678da-324">Hello 요청 본문에서 hello 대상 리소스 그룹 및 리소스 toomove hello 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-324">In hello request body, you specify hello target resource group and hello resources toomove.</span></span> <span data-ttu-id="678da-325">Hello 이동 REST 작업을 수행 하는 방법에 대 한 자세한 내용은 참조 [리소스 이동](https://msdn.microsoft.com/library/azure/mt218710.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-325">For more information about hello move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="678da-326">다음 단계</span><span class="sxs-lookup"><span data-stu-id="678da-326">Next steps</span></span>
* <span data-ttu-id="678da-327">구독을 관리 하기 위한 PowerShell cmdlet에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 리소스 관리자와](powershell-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-327">toolearn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="678da-328">구독을 관리 하기 위한 Azure CLI 명령에 대 한 toolearn 참조 [hello를 사용 하 여 리소스 관리자와 Azure CLI](xplat-cli-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-328">toolearn about Azure CLI commands for managing your subscription, see [Using hello Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="678da-329">구독을 관리 하기 위한 포털 기능에 대 한 toolearn 참조 [hello Azure 포털 toomanage 리소스를 사용 하 여](resource-group-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-329">toolearn about portal features for managing your subscription, see [Using hello Azure portal toomanage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="678da-330">toolearn 논리적 구성이 tooyour 리소스를 적용 하는 방법에 대 한 참조 [를 사용 하 여 태그 tooorganize 리소스](resource-group-using-tags.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="678da-330">toolearn about applying a logical organization tooyour resources, see [Using tags tooorganize your resources](resource-group-using-tags.md).</span></span>
