---
title: ".NET SDK를 사용하여 Azure DNS에서 DNS 영역 및 레코드 집합 만들기 | Microsoft Docs"
description: ".NET SDK를 사용하여 Azure DNS에서 DNS 영역 및 레코드 집합을 만드는 방법입니다."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: c0fb0be8da1c0ca48a4d43ea027d30a0bc17fe30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-zones-and-record-sets-using-the-net-sdk"></a><span data-ttu-id="b50d1-103">.NET SDK를 사용하여 DNS 영역 및 레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="b50d1-103">Create DNS zones and record sets using the .NET SDK</span></span>

<span data-ttu-id="b50d1-104">.NET DNS 관리 라이브러리와 함께 DNS SDK를 사용하여 DNS 영역, 레코드 집합 및 레코드를 만들거나 삭제하거나 업데이트하는 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="b50d1-105">전체 Visual Studio 프로젝트는 [여기](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="b50d1-106">서비스 주체 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="b50d1-106">Create a service principal account</span></span>

<span data-ttu-id="b50d1-107">일반적으로 고유한 사용자 자격 증명 대신 전용 계정을 통해 Azure 리소스에 대한 프로그래밍 방식의 액세스를 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="b50d1-108">이러한 전용 계정을 '서비스 주체' 계정이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="b50d1-109">Azure DNS SDK 샘플 프로젝트를 사용하려면 먼저 서비스 주체 계정을 만들고 올바른 사용 권한을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span></span>

1. <span data-ttu-id="b50d1-110">[이러한 지침](../azure-resource-manager/resource-group-authenticate-service-principal.md) 에 따라 서비스 주체 계정을 만듭니다(Azure DNS SDK 샘플 프로젝트는 암호 기반 인증을 가정함).</span><span class="sxs-lookup"><span data-stu-id="b50d1-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="b50d1-111">리소스 그룹을 만듭니다([방법은 여기에서 확인](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="b50d1-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="b50d1-112">Azure RBAC를 사용하여 서비스 주체 계정 'DNS 영역 참가자' 권한을 리소스 그룹에 부여합니다([방법은 다음과 같음](../active-directory/role-based-access-control-configure.md)).</span><span class="sxs-lookup"><span data-stu-id="b50d1-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="b50d1-113">Azure DNS SDK 샘플 프로젝트를 사용하는 경우 'program.cs' 파일을 다음과 같이 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="b50d1-114">1단계에서 사용한 대로 tenatId, clientId(계정 ID라고도 함), 비밀(서비스 주체 계정 암호) 및 subscriptionId에 대한 올바른 값을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="b50d1-115">2단계에서 선택한 리소스 그룹 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-115">Enter the resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="b50d1-116">선택한 DNS 영역 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="b50d1-117">NuGet 패키지 및 네임스페이스 선언</span><span class="sxs-lookup"><span data-stu-id="b50d1-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="b50d1-118">Azure DNS .NET SDK를 사용하려면 **Azure DNS 관리 라이브러리** NuGet 패키지 및 기타 필수 Azure 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="b50d1-119">**Visual Studio**에서 프로젝트 또는 새 프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="b50d1-120">**도구** **>** **NuGet 패키지 관리자** **>** **솔루션의 NuGet 패키지 관리...**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="b50d1-121">**찾아보기**를 클릭하고 **시험판 포함** 확인란을 사용하도록 설정한 후, 검색 상자에 **Microsoft.Azure.Management.Dns**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span></span>
4. <span data-ttu-id="b50d1-122">패키지를 선택하고 **설치** 를 클릭하여 Visual Studio 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-122">Select the package and click **Install** to add it to your Visual Studio project.</span></span>
5. <span data-ttu-id="b50d1-123">또한 위의 프로세스를 반복하여 **Microsoft.Rest.ClientRuntime.Azure.Authentication** 및 **Microsoft.Azure.Management.ResourceManager** 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="b50d1-124">네임스페이스 선언 추가</span><span class="sxs-lookup"><span data-stu-id="b50d1-124">Add namespace declarations</span></span>

<span data-ttu-id="b50d1-125">다음 네임스페이스 선언 추가</span><span class="sxs-lookup"><span data-stu-id="b50d1-125">Add the following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-the-dns-management-client"></a><span data-ttu-id="b50d1-126">DNS 관리 클라이언트 초기화</span><span class="sxs-lookup"><span data-stu-id="b50d1-126">Initialize the DNS management client</span></span>

<span data-ttu-id="b50d1-127">*DnsManagementClient* 에는 DNS 영역 및 레코드 집합 관리에 필요한 메서드 및 속성이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="b50d1-128">다음 코드는 서비스 주체 계정에 로그인하고 DnsManagementClient 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build the service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="b50d1-129">DNS 영역 만들기 또는 업데이트</span><span class="sxs-lookup"><span data-stu-id="b50d1-129">Create or update a DNS zone</span></span>

<span data-ttu-id="b50d1-130">DNS 영역을 만들려면 먼저 "영역" 개체가 DNS 영역 매개 변수를 포함하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span></span> <span data-ttu-id="b50d1-131">DNS 영역은 특정 지역에 연결되어 있지 않기 때문에 위치가 '전역'으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span></span> <span data-ttu-id="b50d1-132">이 예제에서는 [Azure Resource Manager '태그'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) 도 영역에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span></span>

<span data-ttu-id="b50d1-133">실제로 Azure DNS에서 영역을 만들거나 업데이트하려면 영역 매개 변수를 포함하는 영역 개체를 *DnsManagementClient.Zones.CreateOrUpdateAsyc* 메서드에 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="b50d1-134">DnsManagementClient는 동기('CreateOrUpdate'), 비동기('CreateOrUpdateAsync') 또는 HTTP 응답에 액세스 권한을 가진 비동기('CreateOrUpdateWithHttpMessagesAsync') 등 세 가지 작업 모드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="b50d1-135">응용 프로그램 요구 사항에 따라 이러한 모드 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="b50d1-136">Azure DNS는 [Etag](dns-getstarted-create-dnszone.md)라는 낙관적 동시성을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="b50d1-137">이 예제에서 'If-None-Match' 헤더에 "*"를 지정하면 DNS 영역이 아직 없는 경우 Azure DNS에서 만들도록 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-137">In this example, specifying "*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="b50d1-138">지정된 이름을 가진 영역이 지정된 리소스 그룹에 이미 있는 경우 호출은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-138">The call fails if a zone with the given name already exists in the given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create the actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if the zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting the http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="b50d1-139">DNS 레코드 집합 및 레코드 만들기</span><span class="sxs-lookup"><span data-stu-id="b50d1-139">Create DNS record sets and records</span></span>

<span data-ttu-id="b50d1-140">DNS 레코드는 레코드 집합으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="b50d1-141">레코드 집합은 영역 내에서 동일한 이름과 레코드 형식을 가진 레코드의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-141">A record set is a set of records with the same name and record type within a zone.</span></span>  <span data-ttu-id="b50d1-142">레코드 집합 이름은 정규화된 DNS 이름이 아닌 영역 이름에 상대적입니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span></span>

<span data-ttu-id="b50d1-143">레코드 집합을 만들거나 업데이트하려면 "RecordSet" 매개 변수 개체를 만들어서 *DnsManagementClient.RecordSets.CreateOrUpdateAsync*로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="b50d1-144">DNS 영역의 경우 동기('CreateOrUpdate'), 비동기('CreateOrUpdateAsync') 또는 HTTP 응답에 액세스 권한을 가진 비동기('CreateOrUpdateWithHttpMessagesAsync') 등 세 가지 작업 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="b50d1-145">DNS 영역의 경우 레코드 집합에 대한 작업에는 낙관적 동시성에 대한 지원이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="b50d1-146">이 예제에서는 'If-Match' 또는 'If-None-Match'가 지정되지 않았기 때문에 레코드 집합이 항상 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span></span>  <span data-ttu-id="b50d1-147">이 호출은 이 DNS 영역에 있는 동일한 이름과 레코드 형식으로 모든 기존 레코드 집합을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records to the record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata to the record set.  Similar to Azure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create the actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="b50d1-148">영역 및 레코드 집합 가져오기</span><span class="sxs-lookup"><span data-stu-id="b50d1-148">Get zones and record sets</span></span>

<span data-ttu-id="b50d1-149">*DnsManagementClient.Zones.Get* 및 *DnsManagementClient.RecordSets.Get* 메서드는 각각 개별 영역 및 레코드 집합을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="b50d1-150">RecordSets은 해당 형식, 이름 및 속해 있는 영역(및 리소스 그룹)으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span></span> <span data-ttu-id="b50d1-151">영역은 해당 이름 및 속해 있는 리소스 그룹으로 식별됩니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-151">Zones are identified by their name and the resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="b50d1-152">기존 레코드 집합 업데이트</span><span class="sxs-lookup"><span data-stu-id="b50d1-152">Update an existing record set</span></span>

<span data-ttu-id="b50d1-153">기존 DNS 레코드 집합을 업데이트하려면 먼저 레코드 집합을 검색한 후에 레코드 집합 내용을 업데이트하고 변경 내용을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span></span>  <span data-ttu-id="b50d1-154">이 예제에서는 'If-Match' 매개 변수에 있는 검색된 레코드 집합에서 'Etag'를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span></span> <span data-ttu-id="b50d1-155">동시 작업이 동시에 레코드 집합을 수정하는 경우 호출은 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-155">The call fails if a concurrent operation has modified the record set in the meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record to the local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update the record set in Azure DNS
// Note: ETAG check specified, update will be rejected if the record set has changed in the meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="b50d1-156">영역 및 레코드 집합 나열</span><span class="sxs-lookup"><span data-stu-id="b50d1-156">List zones and record sets</span></span>

<span data-ttu-id="b50d1-157">영역을 나열하려면 *DnsManagementClient.Zones.List...* 메서드를 사용합니다. 이는 여러 리소스 그룹에 걸쳐 지정된 리소스 그룹의 모든 영역 또는 지정된 Azure 구독의 모든 영역을 나열하도록 지원합니다. 레코드 집합을 나열하려면 *DnsManagementClient.RecordSets.List...* 메서드를 사용하며 이는 지정한 영역의 모든 레코드 집합 또는 특정 형식의 해당 레코드 집합만을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="b50d1-158">영역을 나열할 때 나오는 레코드 집합은 페이지를 매길 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="b50d1-159">다음 예제에서는 결과 페이지를 반복하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-159">The following example shows how to iterate through the pages of results.</span></span> <span data-ttu-id="b50d1-160">(인위적으로 작은 페이지 크기인 '2'는 페이지를 강제하는 데 사용됩니다. 실제로 이 매개 변수를 생략하고 기본 페이지 크기를 사용해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="b50d1-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) to demonstrate paging
// In practice, to improve performance you would use a large page size or just use the system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="b50d1-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b50d1-161">Next steps</span></span>

<span data-ttu-id="b50d1-162">다른 DNS 레코드 형식에 대한 예제를 비롯한 Azure DNS .NET SDK를 사용하는 방법의 추가 예제가 포함된 [Azure DNS .NET SDK 샘플 프로젝트](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b50d1-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
