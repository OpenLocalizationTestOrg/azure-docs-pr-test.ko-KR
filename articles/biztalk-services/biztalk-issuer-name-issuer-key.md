---
title: "BizTalk 서비스의 발급자 이름 및 발급자 키 | Microsoft Docs"
description: "BizTalk 서비스에서 서비스 버스 또는 액세스 제어(ACS)에 대한 발급자 이름 및 발급자 키를 검색하는 방법에 대해 알아봅니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="14905-104">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="14905-105">Azure BizTalk 서비스는 서비스 버스 발급자 이름 및 발급자 키와 액세스 제어 발급자 이름 및 발급자 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="14905-106">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14905-106">Specifically:</span></span>

| <span data-ttu-id="14905-107">작업</span><span class="sxs-lookup"><span data-stu-id="14905-107">Task</span></span> | <span data-ttu-id="14905-108">발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="14905-109">Visual Studio에서 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="14905-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="14905-110">액세스 제어 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="14905-111">Azure BizTalk 서비스 포털 구성</span><span class="sxs-lookup"><span data-stu-id="14905-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="14905-112">액세스 제어 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="14905-113">Visual Studio에서 BizTalk 어댑터 서비스로 LOB 릴레이 만들기</span><span class="sxs-lookup"><span data-stu-id="14905-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="14905-114">서비스 버스 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="14905-115">이 토픽에서는 발급자 이름 및 발급자 키를 검색하는 단계를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="14905-116">액세스 제어 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="14905-117">액세스 제어 발급자 이름 및 발급자 키는 다음에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14905-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="14905-118">Visual Studio에서 만든 Azure BizTalk 서비스 응용 프로그램: Visual Studio의 BizTalk 서비스 응용 프로그램을 Azure에 배포하려면 액세스 제어 발급자 이름 및 발급자 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="14905-119">Azure BizTalk 서비스 포털: BizTalk 서비스를 만들고 BizTalk 서비스 포털에 로그인하면 배포를 위해 액세스 제어 발급자 이름 및 액세스 제어 발급자 키가 동일한 액세스 제어 값으로 자동으로 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="14905-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="14905-120">액세스 제어 발급자 이름 및 발급자 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="14905-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="14905-121">인증을 위해 ACS를 사용하고 발급자 이름 및 발급자 키 값을 가져오는 전체 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="14905-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="14905-122">[Azure PowerShell cmdlet](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="14905-123">Azure 계정을 추가합니다. `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="14905-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="14905-124">구독 이름을 반환합니다. `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="14905-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="14905-125">사용 중인 구독을 선택합니다. `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="14905-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="14905-126">새 네임스페이스를 만듭니다. `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="14905-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="14905-127">예:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="14905-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="14905-128">새 ACS 네임스페이스를 만들면(몇 분 정도 걸릴 수 있음) 발급자 이름 및 발급자 키 값이 연결 문자열에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="14905-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="14905-129">요약하면</span><span class="sxs-lookup"><span data-stu-id="14905-129">To summarize:</span></span>  
<span data-ttu-id="14905-130">발급자 이름 = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="14905-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="14905-131">발급자 키 = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="14905-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="14905-132">[New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet에 대한 추가 정보</span><span class="sxs-lookup"><span data-stu-id="14905-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="14905-133">서비스 버스 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="14905-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="14905-134">서비스 버스 발급자 이름 및 발급자 키는 BizTalk 어댑터 서비스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14905-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="14905-135">Visual Studio의 BizTalk 서비스 프로젝트에서 BizTalk 어댑터 서비스를 사용하여 온-프레미스 LOB(기간 업무) 시스템에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="14905-136">연결하려면 LOB 릴레이를 만들고 LOB 시스템 세부 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="14905-137">이 작업을 수행할 때에도 서비스 버스 발급자 이름 및 발급자 키를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="14905-138">서비스 버스 발급자 이름 및 발급자 키를 검색하려면</span><span class="sxs-lookup"><span data-stu-id="14905-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="14905-139">[Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="14905-140">왼쪽 탐색 창에서 **Service Bus**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="14905-141">네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-141">Select your namespace.</span></span> <span data-ttu-id="14905-142">작업 표시줄에서 **연결 정보**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="14905-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="14905-143">그러면 **기본 발급자**(발급자 이름) 및 **기본 키**(발급자 키)가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="14905-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="14905-144">이 값은 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14905-144">Their values can be copied.</span></span>  

<span data-ttu-id="14905-145">요약하면</span><span class="sxs-lookup"><span data-stu-id="14905-145">To summarize:</span></span>  
<span data-ttu-id="14905-146">발급자 이름 = 기본 발급자</span><span class="sxs-lookup"><span data-stu-id="14905-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="14905-147">발급자 키 = 기본 키</span><span class="sxs-lookup"><span data-stu-id="14905-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="14905-148">다음</span><span class="sxs-lookup"><span data-stu-id="14905-148">Next</span></span>
<span data-ttu-id="14905-149">추가 Azure BizTalk 서비스 항목:</span><span class="sxs-lookup"><span data-stu-id="14905-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="14905-150">Azure BizTalk 서비스 SDK 설치</span><span class="sxs-lookup"><span data-stu-id="14905-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="14905-151">자습서: Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="14905-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="14905-152">Azure BizTalk 서비스 SDK로 시작하는 방법</span><span class="sxs-lookup"><span data-stu-id="14905-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="14905-153">Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="14905-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="14905-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="14905-154">See Also</span></span>
* [<span data-ttu-id="14905-155">방법: ACS 관리 서비스를 사용하여 서비스 ID 구성</span><span class="sxs-lookup"><span data-stu-id="14905-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="14905-156">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="14905-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="14905-157">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="14905-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="14905-158">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="14905-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="14905-159">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="14905-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="14905-160">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="14905-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="14905-161">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="14905-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

