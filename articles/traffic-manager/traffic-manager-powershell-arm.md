---
title: "aaaUsing PowerShell toomanage azure에서 트래픽 관리자 | Microsoft Docs"
description: "Azure Resource Manager과 함께 Traffic Manager용 powershell 사용"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="4b72b-103">PowerShell toomanage 트래픽 관리자를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="4b72b-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="4b72b-104">Azure 리소스 관리자는 Azure에서 서비스에 대 한 hello 기본 설정된 관리 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="4b72b-105">Azure Resource Manager 기반 API 및 도구를 사용하여 Azure Traffic Manager 프로파일을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="4b72b-106">리소스 모델</span><span class="sxs-lookup"><span data-stu-id="4b72b-106">Resource model</span></span>

<span data-ttu-id="4b72b-107">Azure Traffic Manager는 Traffic Manager 프로필을 호출하는 설정 모음을 사용하여 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="4b72b-108">이 프로필에 DNS 설정, 트래픽 라우팅 설정, 끝점 모니터링 설정을 포함 하 고 서비스 끝점 toowhich 트래픽 목록은 라우팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="4b72b-109">각 Traffic Manager 프로필은 'TrafficManagerProfiles' 유형의 리소스로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="4b72b-110">Hello REST API 수준에서 각 프로필에 대 한 hello URI는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="4b72b-111">Azure PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="4b72b-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="4b72b-112">이러한 지침은 Microsoft Azure PowerShell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="4b72b-113">hello 다음 문서에서는 설명 어떻게 tooinstall 및 Azure PowerShell을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="4b72b-114">어떻게 tooinstall Azure PowerShell 및 구성</span><span class="sxs-lookup"><span data-stu-id="4b72b-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="4b72b-115">이 문서의 hello 예제에서는 기존 리소스 그룹 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="4b72b-116">다음 명령을 hello를 사용 하 여 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="4b72b-117">Azure Resource Manager를 사용하려면 모든 리소스 그룹에 위치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="4b72b-118">이 위치는 해당 리소스 그룹에 생성 된 리소스에 대 한 hello 기본으로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="4b72b-119">그러나 트래픽 관리자 프로필 리소스, 글로벌 국가별 하지 않으므로 hello 다양 한 리소스 그룹 위치에 아무런 영향을 주지 Azure 트래픽 관리자.</span><span class="sxs-lookup"><span data-stu-id="4b72b-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="4b72b-120">Traffic Manager 프로필 만들기</span><span class="sxs-lookup"><span data-stu-id="4b72b-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="4b72b-121">toocreate 트래픽 관리자 프로필을 사용 하 여 hello `New-AzureRmTrafficManagerProfile` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b72b-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="4b72b-122">다음 표에서 hello hello 매개 변수를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="4b72b-123">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4b72b-123">Parameter</span></span> | <span data-ttu-id="4b72b-124">설명</span><span class="sxs-lookup"><span data-stu-id="4b72b-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4b72b-125">이름</span><span class="sxs-lookup"><span data-stu-id="4b72b-125">Name</span></span> |<span data-ttu-id="4b72b-126">트래픽 관리자 프로필 리소스 hello에 대 한 hello 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="4b72b-127">프로필에 hello 동일한 리소스 그룹 이름은 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="4b72b-128">이 이름은 hello DNS 이름 DNS 쿼리에 사용 되는 별개입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="4b72b-129">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4b72b-129">ResourceGroupName</span></span> |<span data-ttu-id="4b72b-130">hello 리소스 그룹 포함 hello 프로필 리소스의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="4b72b-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="4b72b-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="4b72b-132">Hello 트래픽 라우팅을 사용 하는 방법 toodetermine 끝점 DNS 쿼리 응답에서 반환 되를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="4b72b-133">가능한 값은 '성능', '가중' 또는 '우선 순위'입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="4b72b-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="4b72b-134">RelativeDnsName</span></span> |<span data-ttu-id="4b72b-135">이 트래픽 관리자 프로필에서 제공 하는 hello DNS 이름의 hello 호스트 이름 부분을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="4b72b-136">이 값은 hello 프로필의 Azure 트래픽 관리자 tooform hello 정규화 된 도메인 이름 (FQDN)에서 사용 하는 hello DNS 도메인 이름으로 결합 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="4b72b-137">예를 들어 'contoso.trafficmanager.net입니다.'은 'contoso' hello 값 설정</span><span class="sxs-lookup"><span data-stu-id="4b72b-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="4b72b-138">TTL</span><span class="sxs-lookup"><span data-stu-id="4b72b-138">TTL</span></span> |<span data-ttu-id="4b72b-139">DNS 시간 to Live (TTL) hello 초 단위로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="4b72b-140">이 ttl hello 로컬 DNS 확인자 및 DNS 클라이언트가 트래픽 관리자 프로필에 대 한 시간 toocache DNS 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="4b72b-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="4b72b-141">MonitorProtocol</span></span> |<span data-ttu-id="4b72b-142">Hello 프로토콜 toouse toomonitor 끝점 상태를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="4b72b-143">가능한 값은 ‘HTTP’ 및 ‘HTTPS’입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="4b72b-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="4b72b-144">MonitorPort</span></span> |<span data-ttu-id="4b72b-145">Toomonitor 끝점 상태를 사용 하는 hello TCP 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="4b72b-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="4b72b-146">MonitorPath</span></span> |<span data-ttu-id="4b72b-147">끝점 상태에 대 한 tooprobe를 사용 하는 hello 경로 상대 toohello 끝점 도메인 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="4b72b-148">hello cmdlet azure에서 트래픽 관리자 프로필을 만들고 해당 프로필 개체 tooPowerShell를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="4b72b-149">이 시점에서 hello 프로필에는 끝점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="4b72b-150">Tooa 트래픽 관리자 프로필 끝점을 추가 하는 방법에 대 한 자세한 내용은 참조 [트래픽 관리자 끝점 추가](#adding-traffic-manager-endpoints)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="4b72b-151">Traffic Manager 프로필 가져오기</span><span class="sxs-lookup"><span data-stu-id="4b72b-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="4b72b-152">tooretrieve 기존 트래픽 관리자 프로필 개체를 사용 하 여 hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b72b-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="4b72b-153">이 cmdlet은 Traffic Manager 프로필 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="4b72b-154">Traffic Manager 프로필 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b72b-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="4b72b-155">Traffic Manager 프로필을 수정하려면 3 단계 프로세스를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="4b72b-156">사용 하 여 검색 hello 프로필 `Get-AzureRmTrafficManagerProfile` 반환한 hello 프로필을 사용 하거나 `New-AzureRmTrafficManagerProfile`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="4b72b-157">Hello 프로필을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-157">Modify hello profile.</span></span> <span data-ttu-id="4b72b-158">끝점을 추가 및 제거하거나 끝점 또는 프로필 매개 변수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="4b72b-159">이러한 변경은 오프라인 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-159">These changes are off-line operations.</span></span> <span data-ttu-id="4b72b-160">Hello 로컬 개체 hello 프로필을 나타내는 메모리에만 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="4b72b-161">Hello를 사용 하 여 변경 내용을 커밋하여 `Set-AzureRmTrafficManagerProfile` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b72b-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="4b72b-162">Hello 프로필의 RelativeDnsName 제외 하 고 모든 프로필 속성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="4b72b-163">toochange RelativeDnsName hello, 프로필 및 새 이름으로 새 프로필을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="4b72b-164">다음 예제는 hello toochange 프로필의 TTL hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="4b72b-165">Traffic Manager 끝점에는 세 가지 종류가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="4b72b-166">**Azure 끝점** 은 Azure에서 호스팅되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="4b72b-167">**외부 끝점**은 Azure 외부에서 호스트되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="4b72b-168">**끝점에 중첩 된** 은 트래픽 관리자 프로필의 사용 되는 tooconstruct 중첩 된 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="4b72b-169">중첩 끝점은 복잡한 응용 프로그램에 대한 고급 트래픽 라우팅 구성을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="4b72b-170">세 가지 경우 모두, 끝점은 두 가지 방법으로 추가될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="4b72b-171">앞에서 설명한 3 단계 프로세스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="4b72b-172">이 방법의 장점은 hello는 단일 업데이트에서 여러 끝점 변경을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="4b72b-173">Hello 새로 AzureRmTrafficManagerEndpoint cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="4b72b-174">이 cmdlet은 단일 작업으로 끝점 tooan 기존 트래픽 관리자 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="4b72b-175">Azure 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="4b72b-176">Azure 끝점는 Azure에서 호스팅되는 서비스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="4b72b-177">두 가지 유형의 Azure 끝점이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="4b72b-178">Azure 웹앱</span><span class="sxs-lookup"><span data-stu-id="4b72b-178">Azure Web Apps</span></span>
2. <span data-ttu-id="4b72b-179">Azure PublicIpAddress 리소스 (연결 된 tooa 부하 분산 장치 또는 가상 컴퓨터 NIC 일 수 있음).</span><span class="sxs-lookup"><span data-stu-id="4b72b-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="4b72b-180">hello PublicIpAddress toobe 트래픽 관리자에서 사용 되는 할당 된 DNS 이름이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="4b72b-181">각 경우에 다음이 해당됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-181">In each case:</span></span>

* <span data-ttu-id="4b72b-182">hello 서비스의 hello 'targetResourceId' 매개 변수를 사용 하 여 지정 `Add-AzureRmTrafficManagerEndpointConfig` 또는 `New-AzureRmTrafficManagerEndpoint`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="4b72b-183">hello 'Target' 및 'EndpointLocation'에서 암시 된 hello TargetResourceId 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="4b72b-184">'가중치' hello 지정 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="4b72b-185">가중치는 hello 프로필은 구성 된 toouse hello '가 중' 트래픽 라우팅 방법을 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="4b72b-186">그렇지 않으면 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="4b72b-187">를 지정 하는 경우 hello 값 1에서 1000 사이의 숫자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="4b72b-188">hello 기본값은 '1'입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-188">hello default value is '1'.</span></span>
* <span data-ttu-id="4b72b-189">지정 하 여 hello 'Priority' 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="4b72b-190">우선 순위는 hello 프로필은 구성 된 toouse hello 'Priority' 트래픽 라우팅 방법을 하는 경우에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="4b72b-191">그렇지 않으면 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="4b72b-192">유효한 값은 상위 우선 순위를 나타내는 값이 낮은 1 too1000에서은 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="4b72b-193">한 끝점에 대해 지정한 경우 모든 끝점에 대해 지정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="4b72b-194">생략 하면 기본값은 '1'에서 시작 하는 hello 끝점이 표시 되지 hello 순서로 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="4b72b-195">예시 1: `Add-AzureRmTrafficManagerEndpointConfig`을 사용하여 웹앱 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="4b72b-196">이 예제에서는에서는 트래픽 관리자 프로필을 만들고 추가 hello를 사용 하 여 두 개의 웹 응용 프로그램 끝점 `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b72b-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4b72b-197">예시 2: `New-AzureRmTrafficManagerEndpoint`을 사용하여 publicIpAddress 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4b72b-198">이 예제에서는 공용 IP 주소 리소스 toohello 트래픽 관리자 프로필을 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="4b72b-199">hello 공용 IP 주소를 구성 하는 DNS 이름이 있어야 하 고 어느 toohello NIC VM 또는 tooa 부하 분산 장치에 바인딩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="4b72b-200">외부 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-200">Adding External Endpoints</span></span>

<span data-ttu-id="4b72b-201">트래픽 관리자 외부 끝점 toodirect 트래픽 tooservices Azure 외부에서 호스팅된 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="4b72b-202">Azure 끝점과 마찬가지로 외부 끝점은 `Add-AzureRmTrafficManagerEndpointConfig` 뒤 이어 `Set-AzureRmTrafficManagerProfile` 또는 `New-AzureRMTrafficManagerEndpoint`을 사용하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="4b72b-203">외부 끝점을 지정하는 경우:</span><span class="sxs-lookup"><span data-stu-id="4b72b-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="4b72b-204">hello 'Target' 매개 변수를 사용 하 여 hello 끝점 도메인 이름을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="4b72b-205">Hello 'Performance' 트래픽 라우팅 메서드를 사용 하는 경우에 hello 'EndpointLocation'가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="4b72b-206">그렇지 않은 경우 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-206">Otherwise it is optional.</span></span> <span data-ttu-id="4b72b-207">hello 값 이어야 합니다는 [올바른 Azure 지역 이름](https://azure.microsoft.com/regions/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="4b72b-208">hello '가중치' 및 'Priority'는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="4b72b-209">예시 1: `Add-AzureRmTrafficManagerEndpointConfig`과 `Set-AzureRmTrafficManagerProfile`를 사용하여 외부 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="4b72b-210">이 예에서 만든 트래픽 관리자 프로필, 두 개의 외부 끝점을 추가 하 hello 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4b72b-211">예시 2: `New-AzureRmTrafficManagerEndpoint`을 사용하여 외부 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4b72b-212">이 예제에서는 외부 끝점 tooan 기존 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="4b72b-213">hello 프로필 및 리소스 그룹 이름을 사용 하 여 hello 프로필을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="4b72b-214">'중첩' 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="4b72b-215">각 트래픽 관리자 프로필은 단일 트래픽 라우팅 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="4b72b-216">그러나 단일 트래픽 관리자 프로필에서 제공 hello 라우팅 보다 더 정교한 트래픽 라우팅이 필요로 하는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="4b72b-217">둘 이상의 트래픽 라우팅 방법의 트래픽 관리자 프로필 toocombine hello 혜택을 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="4b72b-218">중첩 된 프로필을 사용 하면 더 큰 toooverride hello 기본 트래픽 관리자 동작 toosupport 및 더 복잡 한 응용 프로그램 배포.</span><span class="sxs-lookup"><span data-stu-id="4b72b-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="4b72b-219">자세한 예시는 [중첩 Traffic Manager 프로필](traffic-manager-nested-profiles.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4b72b-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="4b72b-220">중첩 된 끝점 hello 부모 프로필을 특정 끝점 형식 'NestedEndpoints'를 사용 하 여 구성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="4b72b-221">중첩된 끝점을 지정하는 경우:</span><span class="sxs-lookup"><span data-stu-id="4b72b-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="4b72b-222">hello 'targetResourceId' 매개 변수를 사용 하 여 hello 끝점을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="4b72b-223">Hello 'Performance' 트래픽 라우팅 메서드를 사용 하는 경우에 hello 'EndpointLocation'가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="4b72b-224">그렇지 않은 경우 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-224">Otherwise it is optional.</span></span> <span data-ttu-id="4b72b-225">hello 값 이어야 합니다는 [올바른 Azure 지역 이름](http://azure.microsoft.com/regions/)합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="4b72b-226">'가중치' hello 되며 'Priority' Azure 끝점의 경우와 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="4b72b-227">hello 'MinChildEndpoints' 매개 변수는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="4b72b-228">hello 기본값은 '1'입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-228">hello default value is '1'.</span></span> <span data-ttu-id="4b72b-229">사용 가능한 끝점 수가 hello이이 임계값에 미달할 hello 자식 프로필 '저하' 및 트래픽 toohello hello 부모 프로필의 다른 끝점으로 넘깁니다 hello 부모 프로필 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="4b72b-230">예시 1: `Add-AzureRmTrafficManagerEndpointConfig`과 `Set-AzureRmTrafficManagerProfile`를 사용하여 중첩 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="4b72b-231">이 예에서 만든 새로운 트래픽 관리자 자식 및 부모 프로필, 중첩된 끝점 toohello 부모로 hello 하위 항목 추가 하 hello 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="4b72b-232">이 예에서는 간단한 설명을 위해 우리는 다른 끝점 toohello 자식 또는 부모 프로필 추가 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4b72b-233">예시 2: `New-AzureRmTrafficManagerEndpoint`을 사용하여 중첩 끝점 추가</span><span class="sxs-lookup"><span data-stu-id="4b72b-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4b72b-234">이 예제에서는 중첩 된 끝점 tooan 기존 부모 프로필 기존 자식 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="4b72b-235">hello 프로필 및 리소스 그룹 이름을 사용 하 여 hello 프로필을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="4b72b-236">Traffic Manager 끝점 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b72b-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="4b72b-237">기존 트래픽 관리자 끝점은 두 가지 방법으로 tooupdate:</span><span class="sxs-lookup"><span data-stu-id="4b72b-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="4b72b-238">사용 하 여 hello 트래픽 관리자 프로필 가져오기 `Get-AzureRmTrafficManagerProfile`, hello 프로필 내 hello 끝점 속성을 업데이트 하 고 사용 하 여 hello 변경 내용 커밋 `Set-AzureRmTrafficManagerProfile`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="4b72b-239">이 메서드는 한 번에 둘 이상의 끝점 수 tooupdate는 hello 장점이.</span><span class="sxs-lookup"><span data-stu-id="4b72b-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="4b72b-240">사용 하 여 hello 트래픽 관리자 끝점 가져오기 `Get-AzureRmTrafficManagerEndpoint`, hello 끝점 속성을 업데이트 하 고 사용 하 여 hello 변경 내용 커밋 `Set-AzureRmTrafficManagerEndpoint`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="4b72b-241">이 메서드는 hello 프로필에서 끝점 배열 hello에 대 한 인덱싱이 필요 하지 않습니다 때문에 더 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="4b72b-242">예시 1: `Get-AzureRmTrafficManagerProfile`과 `Set-AzureRmTrafficManagerProfile`를 사용하여 끝점 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b72b-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="4b72b-243">이 예제에서는 기존 프로필 내에서 두 개의 끝점에서 hello 우선 순위를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="4b72b-244">예시 2: `Get-AzureRmTrafficManagerEndpoint`과 `Set-AzureRmTrafficManagerEndpoint`를 사용하여 끝점 업데이트</span><span class="sxs-lookup"><span data-stu-id="4b72b-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="4b72b-245">이 예제에서는 기존 프로필에 있는 단일 끝점의 hello 가중치를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="4b72b-246">끝점 및 프로필 활성화 및 비활성화</span><span class="sxs-lookup"><span data-stu-id="4b72b-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="4b72b-247">트래픽 관리자를 사용 하도록 설정 및 해제, 설정 및 해제의 전체 프로필을 만들 수 있으며 개별 끝점 toobe를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="4b72b-248">가져오기/업데이트/설정 hello 끝점 또는 프로필 리소스에서 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="4b72b-249">toostreamline 이러한 일반적인 작업에도 전용된 cmdlet을 통해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="4b72b-250">예제 1: Traffic Manager 프로필 활성화 및 비활성화</span><span class="sxs-lookup"><span data-stu-id="4b72b-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="4b72b-251">tooenable 트래픽 관리자 프로필을 사용 하 여 `Enable-AzureRmTrafficManagerProfile`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="4b72b-252">hello 프로필은 프로필 개체를 사용 하 여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="4b72b-253">hello 프로필 개체 또는 전달할 수 있습니다 hello 파이프라인을 통해 hello를 사용 하 여 '-TrafficManagerProfile' 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="4b72b-254">이 예제에서는 hello 프로필 hello 프로필 및 리소스 그룹 이름으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="4b72b-255">트래픽 관리자 프로필 toodisable:</span><span class="sxs-lookup"><span data-stu-id="4b72b-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="4b72b-256">hello 사용 안 함 AzureRmTrafficManagerProfile cmdlet 확인 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4b72b-257">Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="4b72b-258">예제 2: Traffic Manager 끝점 활성화 및 비활성화</span><span class="sxs-lookup"><span data-stu-id="4b72b-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="4b72b-259">tooenable 트래픽 관리자 끝점을 사용 하 여 `Enable-AzureRmTrafficManagerEndpoint`합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="4b72b-260">두 가지 방법으로 toospecify hello 끝점</span><span class="sxs-lookup"><span data-stu-id="4b72b-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="4b72b-261">Hello 또는 hello 파이프라인을 통해 전달 되는 TrafficManagerEndpoint 개체를 사용 하 여 '-TrafficManagerEndpoint' 매개 변수</span><span class="sxs-lookup"><span data-stu-id="4b72b-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="4b72b-262">Hello 끝점 이름, 끝점 유형, 프로필 이름 및 리소스 그룹 이름을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="4b72b-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="4b72b-263">마찬가지로, toodisable 트래픽 관리자 끝점:</span><span class="sxs-lookup"><span data-stu-id="4b72b-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="4b72b-264">와 마찬가지로 `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet 확인 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4b72b-265">Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="4b72b-266">Traffic Manager 끝점 삭제</span><span class="sxs-lookup"><span data-stu-id="4b72b-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="4b72b-267">tooremove 개별 끝점을 사용 하 여 hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b72b-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="4b72b-268">이 cmdlet은 확인 프롬프트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4b72b-269">Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="4b72b-270">Traffic Manager 프로필 삭제</span><span class="sxs-lookup"><span data-stu-id="4b72b-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="4b72b-271">toodelete 트래픽 관리자 프로필을 사용 하 여 hello `Remove-AzureRmTrafficManagerProfile` hello 프로필 및 리소스 그룹 이름을 지정 하는 cmdlet:</span><span class="sxs-lookup"><span data-stu-id="4b72b-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="4b72b-272">이 cmdlet은 확인 프롬프트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="4b72b-273">Hello를 사용 하 여이 프롬프트를 보류 될 수 있습니다 '-Force' 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="4b72b-274">삭제 하는 hello 프로필 toobe 프로필 개체를 사용 하 여 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="4b72b-275">이 순서는 파이프될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b72b-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="4b72b-276">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4b72b-276">Next steps</span></span>

[<span data-ttu-id="4b72b-277">Traffic Manager 모니터링</span><span class="sxs-lookup"><span data-stu-id="4b72b-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="4b72b-278">Traffic Manager 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="4b72b-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
