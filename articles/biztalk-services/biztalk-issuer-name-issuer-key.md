---
title: "aaaIssuer 이름 및 발급자 키에서 BizTalk 서비스 | Microsoft Docs"
description: "자세한 내용은 tooretrieve 발급자 이름을 지정 하는 방법 및 ACS (액세스 제어)에 BizTalk 서비스 또는 서비스 버스에 대 한 발급자 키입니다. MABS, WABS"
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="9c634-104">BizTalk 서비스: 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="9c634-105">Azure BizTalk 서비스는 hello 서비스 버스 발급자 이름 및 발급자 키 hello 액세스 제어 발급자 이름 및 발급자 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="9c634-106">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-106">Specifically:</span></span>

| <span data-ttu-id="9c634-107">작업</span><span class="sxs-lookup"><span data-stu-id="9c634-107">Task</span></span> | <span data-ttu-id="9c634-108">발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="9c634-109">Visual Studio에서 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="9c634-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="9c634-110">액세스 제어 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="9c634-111">Hello Azure BizTalk 서비스 포털 구성</span><span class="sxs-lookup"><span data-stu-id="9c634-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="9c634-112">액세스 제어 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="9c634-113">Visual Studio에서 BizTalk 어댑터 서비스 hello를 사용 하 여 LOB 릴레이 만들기</span><span class="sxs-lookup"><span data-stu-id="9c634-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="9c634-114">서비스 버스 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="9c634-115">이 항목에서는 hello 단계 tooretrieve hello 발급자 이름 및 발급자 키를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="9c634-116">액세스 제어 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="9c634-117">hello 다음 hello 액세스 제어 발급자 이름 및 발급자 키가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="9c634-118">Azure BizTalk 서비스 응용 프로그램에서 Visual Studio에서 만든: toosuccessfully tooAzure Visual Studio에서에서 BizTalk 서비스 응용 프로그램을 배포, hello 액세스 제어 발급자 이름 및 발급자 키를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="9c634-119">Azure BizTalk 서비스 포털 hello: BizTalk 서비스를 만들고 엽니다 hello BizTalk 서비스 포털에 대 한 액세스 제어 발급자 이름 및 발급자 키와 배포에 대해 자동으로 등록 됩니다 때 hello 같은 액세스 제어 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="9c634-120">가져오기 hello 액세스 제어 발급자 이름과 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="9c634-121">인증 및 get toouse ACS 발급자 이름과 발급자 키 값을 hello, hello 전체 단계 포함:</span><span class="sxs-lookup"><span data-stu-id="9c634-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="9c634-122">Hello 설치 [Azure Powershell cmdlet](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="9c634-123">Azure 계정을 추가합니다. `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="9c634-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="9c634-124">구독 이름을 반환합니다. `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="9c634-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="9c634-125">사용 중인 구독을 선택합니다. `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="9c634-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="9c634-126">새 네임스페이스를 만듭니다. `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="9c634-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="9c634-127">예:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="9c634-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="9c634-128">Hello 새 ACS 네임 스페이스를 만들면 (있음 몇 분 정도 걸릴 수 있습니다) hello 발급자 이름과 발급자 키 값 hello 연결 문자열에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="9c634-129">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="9c634-129">toosummarize:</span></span>  
<span data-ttu-id="9c634-130">발급자 이름 = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="9c634-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="9c634-131">발급자 키 = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="9c634-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="9c634-132">Hello에 더 [New-azuresbnamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9c634-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="9c634-133">서비스 버스 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="9c634-134">서비스 버스 발급자 이름 및 발급자 키는 BizTalk 어댑터 서비스에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="9c634-135">Visual Studio에서 BizTalk 서비스 프로젝트에서 hello BizTalk 어댑터 서비스 tooconnect tooan 온-프레미스의 업무 (LOB) 시스템을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="9c634-136">tooconnect, hello LOB 릴레이 만들고 LOB 시스템 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="9c634-137">이 작업을 수행 하는 경우 hello 서비스 버스 발급자 이름 및 발급자 키 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="9c634-138">tooretrieve hello 서비스 버스 발급자 이름 및 발급자 키</span><span class="sxs-lookup"><span data-stu-id="9c634-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="9c634-139">Toohello 로그인 [Azure 클래식 포털](http://go.microsoft.com/fwlink/p/?LinkID=213885)합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="9c634-140">Hello 왼쪽된 탐색 창에서 선택 **서비스 버스**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="9c634-141">네임스페이스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-141">Select your namespace.</span></span> <span data-ttu-id="9c634-142">Hello 작업 표시줄에서 선택 **연결 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="9c634-143">Hello 표시 **기본 발급자** (발급자 이름) 및 **기본 키** (발급자 키)입니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="9c634-144">이 값은 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9c634-144">Their values can be copied.</span></span>  

<span data-ttu-id="9c634-145">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="9c634-145">toosummarize:</span></span>  
<span data-ttu-id="9c634-146">발급자 이름 = 기본 발급자</span><span class="sxs-lookup"><span data-stu-id="9c634-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="9c634-147">발급자 키 = 기본 키</span><span class="sxs-lookup"><span data-stu-id="9c634-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="9c634-148">다음</span><span class="sxs-lookup"><span data-stu-id="9c634-148">Next</span></span>
<span data-ttu-id="9c634-149">추가 Azure BizTalk 서비스 항목:</span><span class="sxs-lookup"><span data-stu-id="9c634-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="9c634-150">Hello Azure BizTalk Services SDK 설치</span><span class="sxs-lookup"><span data-stu-id="9c634-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="9c634-151">자습서: Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="9c634-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="9c634-152">Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까</span><span class="sxs-lookup"><span data-stu-id="9c634-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="9c634-153">Azure BizTalk 서비스</span><span class="sxs-lookup"><span data-stu-id="9c634-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="9c634-154">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9c634-154">See Also</span></span>
* [<span data-ttu-id="9c634-155">방법: ACS 관리 서비스를 사용 하 여 tooConfigure 서비스 Id</span><span class="sxs-lookup"><span data-stu-id="9c634-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="9c634-156">BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트</span><span class="sxs-lookup"><span data-stu-id="9c634-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="9c634-157">BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전</span><span class="sxs-lookup"><span data-stu-id="9c634-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="9c634-158">BizTalk 서비스: 프로비저닝 상태 차트</span><span class="sxs-lookup"><span data-stu-id="9c634-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="9c634-159">BizTalk 서비스: 대시보드, 모니터 및 크기 조정 탭</span><span class="sxs-lookup"><span data-stu-id="9c634-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="9c634-160">BizTalk 서비스: 백업 및 복원</span><span class="sxs-lookup"><span data-stu-id="9c634-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="9c634-161">BizTalk 서비스: 제한</span><span class="sxs-lookup"><span data-stu-id="9c634-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

