---
title: "App Service Environment v1을 만드는 방법"
description: "App Service Environment v1에 대한 만들기 흐름 설명"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 400bcc08650f8a13911c05c8d0d04ddc22327dfd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-an-app-service-environment-v1"></a><span data-ttu-id="11563-103">App Service Environment v1을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="11563-103">How to Create an App Service Environment v1</span></span> 

> [!NOTE]
> <span data-ttu-id="11563-104">이 문서는 ASE(App Service Environment) v1에 관한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="11563-104">This article is about the App Service Environment v1.</span></span> <span data-ttu-id="11563-105">사용하기가 더 쉽고 더 강력한 인프라에서 실행되는 최신 버전의 App Service Environment가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-105">There is a newer version of the App Service Environment that is easier to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="11563-106">새 버전에 대한 자세한 내용은 [App Service Environment 소개](../app-service/app-service-environment/intro.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-106">To learn more about the new version start with the [Introduction to the App Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

### <a name="overview"></a><span data-ttu-id="11563-107">개요</span><span class="sxs-lookup"><span data-stu-id="11563-107">Overview</span></span>
<span data-ttu-id="11563-108">ASE(App Service Environment)는 다중 테넌트 증명(stamp)에서 사용할 수 없는 향상된 구성 기능을 제공하는 Azure App Service의 프리미엄 서비스 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="11563-108">The App Service Environment (ASE) is a Premium service option of Azure App Service that delivers an enhanced configuration capability that is not available in the multi-tenant stamps.</span></span> <span data-ttu-id="11563-109">ASE 기능은 기본적으로 고객의 가상 네트워크에 Azure 앱 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-109">The ASE feature essentially deploys the Azure App Service into a customer’s virtual network.</span></span> <span data-ttu-id="11563-110">App Service 환경에서 제공되는 기능에 대한 자세한 내용은 [App Service 환경 정의][WhatisASE] 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-110">To gain a greater understanding of the capabilities offered by App Service Environments read the [What is an App Service Environment][WhatisASE] documentation.</span></span>

### <a name="before-you-create-your-ase"></a><span data-ttu-id="11563-111">ASE를 만들기 전에</span><span class="sxs-lookup"><span data-stu-id="11563-111">Before you create your ASE</span></span>
<span data-ttu-id="11563-112">변경할 수 없다는 점을 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-112">It is important to be aware of the things you cannot change.</span></span> <span data-ttu-id="11563-113">만든 후에 ASE를 변경할 수 없는 항목은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-113">Those aspects you cannot change about your ASE after it is created are:</span></span>

* <span data-ttu-id="11563-114">위치</span><span class="sxs-lookup"><span data-stu-id="11563-114">Location</span></span>
* <span data-ttu-id="11563-115">구독</span><span class="sxs-lookup"><span data-stu-id="11563-115">Subscription</span></span>
* <span data-ttu-id="11563-116">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="11563-116">Resource Group</span></span>
* <span data-ttu-id="11563-117">사용되는 VNet</span><span class="sxs-lookup"><span data-stu-id="11563-117">VNet used</span></span>
* <span data-ttu-id="11563-118">사용되는 서브넷</span><span class="sxs-lookup"><span data-stu-id="11563-118">Subnet used</span></span> 
* <span data-ttu-id="11563-119">서브넷 크기</span><span class="sxs-lookup"><span data-stu-id="11563-119">Subnet size</span></span>

<span data-ttu-id="11563-120">VNet을 선택하고 서브넷을 지정하는 경우 향후 성장을 수용하기에 충분한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-120">When picking a VNet and specifying a subnet, make sure it is large enough to accomodate any future growth.</span></span> 

### <a name="creating-an-app-service-environment-v1"></a><span data-ttu-id="11563-121">App Service Environment v1 만들기</span><span class="sxs-lookup"><span data-stu-id="11563-121">Creating an App Service Environment v1</span></span>
<span data-ttu-id="11563-122">App Service Environment v1을 만들려면 Azure Marketplace에서 ***App Service Environment v1***을 검색하거나 새로 만들기 -> 웹 + 모바일 -> App Service Environment로 차례로 이동하여 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-122">To create an App Service Environment v1 you need to search the Azure Marketplace for ***App Service Environment v1***, or by going through New -> Web + Mobile -> App Service Environment.</span></span> <span data-ttu-id="11563-123">ASE v1을 만들려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-123">To create an ASEv1:</span></span>

1. <span data-ttu-id="11563-124">ASE의 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-124">Provide the name of your ASE.</span></span> <span data-ttu-id="11563-125">지정한 ASE 이름은 ASE에서 만드는 앱에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-125">The name that is specified for the ASE will be used for the apps created in the ASE.</span></span> <span data-ttu-id="11563-126">ASE 이름이 appsvcenvdemo인 경우 하위 도메인 이름은 .*appsvcenvdemo.p.azurewebsites.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="11563-126">If name of the ASE is appsvcenvdemo then the subdomain name would be .*appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="11563-127">따라서 *mytestapp*이라는 앱을 만든 경우 해당 주소는 *mytestapp.appsvcenvdemo.p.azurewebsites.net*으로 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-127">If you thus created an app named *mytestapp* then it would be addressable at *mytestapp.appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="11563-128">ASE의 이름에 공백을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-128">You cannot use white space in the name of your ASE.</span></span> <span data-ttu-id="11563-129">이름에 대문자를 사용한 경우 전체 도메인 이름은 해당 이름의 소문자 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-129">If you use upper case characters in the name, the domain name will be the total lowercase version of that name.</span></span> <span data-ttu-id="11563-130">ILB를 사용하는 경우 ASE 이름이 하위 도메인에서 사용되지 않고 대신 ASE를 만드는 동안에 명시적으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-130">If you use an ILB then your ASE name is not used in your subdomain but is instead explicitly stated during ASE creation</span></span>
   
    ![][1]
2. <span data-ttu-id="11563-131">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-131">Select your subscription.</span></span> <span data-ttu-id="11563-132">ASE에 사용되는 구독은 ASE에 사용되는 모든 앱을 생성하는 구독이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-132">The subscription used for your ASE is also the one that all apps in that ASE will be created with.</span></span> <span data-ttu-id="11563-133">다른 구독에 있는 VNet에 ASE를 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-133">You cannot place your ASE in a VNet that is in another subscription</span></span>
3. <span data-ttu-id="11563-134">새 리소스 그룹을 선택하거나 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-134">Select or specify a new resource group.</span></span> <span data-ttu-id="11563-135">ASE에 사용되는 리소스 그룹은 VNet에 사용되는 것과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-135">The resource group used for your ASE must be the same that is used for your VNet.</span></span> <span data-ttu-id="11563-136">기존 VNet을 선택하는 경우 ASE에 대한 리소스 그룹을 선택하는 작업은 VNet의 선택을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-136">If you select a pre-existing VNet then the resource group selection for your ASE will be updated to reflect that of your VNet.</span></span>
   
    ![][2]
4. <span data-ttu-id="11563-137">가상 네트워크 및 위치 선택을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-137">Make your Virtual Network and Location selections.</span></span> <span data-ttu-id="11563-138">새 VNet을 만들거나 기존 VNet을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-138">You can choose to create a new VNet or select a pre-existing VNet.</span></span> <span data-ttu-id="11563-139">새 VNet을 선택하면 이름 및 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-139">If you select a new VNet then you can specify a name and location.</span></span> <span data-ttu-id="11563-140">새 VNet의 주소 범위는 192.168.250.0/23이고 192.168.250.0/24로 정의된 **default**이라는 서브넷이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-140">The new VNet will have the address range 192.168.250.0/23 and a subnet named **default** that is defined as 192.168.250.0/24.</span></span> <span data-ttu-id="11563-141">또한 기존의 클래식 VNet 또는 Resource Manager VNet을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-141">You can also simply select a pre-existing Classic or Resource Manager VNet.</span></span> <span data-ttu-id="11563-142">VIP 유형은 ASE가 인터넷(외부)에서 직접 액세스할 수 있는지 또는 ILB(내부 부하 분산 장치)를 사용하는지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-142">The VIP Type selection determines if your ASE can be directly accessed from the internet (External) or if it uses an Internal Load Balancer (ILB).</span></span> <span data-ttu-id="11563-143">자세한 내용은 [App Service 환경에서 내부 부하 분산 장치 사용][ILBASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-143">To learn more about them read [Using an Internal Load Balancer with an App Service Environment][ILBASE].</span></span> <span data-ttu-id="11563-144">외부의 VIP 유형을 선택하면 시스템이 IPSSL 목적으로 만들 수 있는 외부 IP 주소의 개수를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-144">If you select a VIP type of External then you can select how many external IP addresses the system is created with for IPSSL purposes.</span></span> <span data-ttu-id="11563-145">내부를 선택하는 경우 ASE에서 사용할 하위 도메인을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-145">If you select Internal then you need to specify the subdomain that your ASE will use.</span></span> <span data-ttu-id="11563-146">공용 주소 범위 *또는* RFC1918 주소 공간(즉, 개인 주소) *중 하나*를 사용하는 가상 네트워크에 ASE를</span><span class="sxs-lookup"><span data-stu-id="11563-146">ASEs can be deployed into virtual networks that use *either* public address ranges, *or* RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="11563-147">배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-147">private addresses).</span></span> <span data-ttu-id="11563-148">공용 주소 범위를 가진 가상 네트워크를 사용하기 위해 사전에 VNet을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-148">In order to use a virtual network with a public address range, you will need to create the VNet ahead of time.</span></span> <span data-ttu-id="11563-149">기존 VNet을 선택하면 ASE를 만드는 동안 새 서브넷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-149">When you select a pre-existing VNet you will need to create a new subnet during ASE creation.</span></span> <span data-ttu-id="11563-150">**포털에서 미리 생성된 서브넷을 사용할 수 없습니다. Resource Manager 템플릿을 사용하여 ASE를 만드는 경우 기존 서브넷으로 ASE를 만들 수 있습니다.**</span><span class="sxs-lookup"><span data-stu-id="11563-150">**You cannot use a pre-created subnet in the portal. You can create an ASE with a pre-existing subnet if you create your ASE using a resource manager template.**</span></span> <span data-ttu-id="11563-151">템플릿에서 ASE를 만들려면 [템플릿에서 App Service 환경 만들기][ILBAseTemplate] 및 [템플릿에서 ILB App Service 환경 만들기][ASEfromTemplate]의 정보를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-151">To create an ASE from a template use the information here, [Creating an App Service Environment from template][ILBAseTemplate] and here, [Creating an ILB App Service Environment from template][ASEfromTemplate].</span></span>

### <a name="details"></a><span data-ttu-id="11563-152">세부 정보</span><span class="sxs-lookup"><span data-stu-id="11563-152">Details</span></span>
<span data-ttu-id="11563-153">ASE는 2개의 프런트 엔드 및 2개의 작업자를 사용하여 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-153">An ASE is created with 2 Front Ends and 2 Workers.</span></span> <span data-ttu-id="11563-154">프런트 엔드는 HTTP/HTTPS 끝점으로 작동하여 앱 호스트 역할을 갖는 작업자로 트래픽을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="11563-154">The Front Ends act as the HTTP/HTTPS endpoints and send traffic to the Workers which are the roles that host your apps.</span></span> <span data-ttu-id="11563-155">ASE를 만든 후에 수량을 조정할 수 있으며 이러한 리소스 풀에서 자동 크기 조정 규칙을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-155">You can adjust the quantity after ASE creation and can even set up autoscale rules on these resource pools.</span></span> <span data-ttu-id="11563-156">수동 크기 조정, App Service 환경 관리 및 모니터링에 대한 자세한 내용은 [App Service 환경을 구성하는 방법][ASEConfig]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-156">For more details around manual scaling, management and monitoring of an App Service Environment go here: [How to configure an App Service Environment][ASEConfig]</span></span> 

<span data-ttu-id="11563-157">ASE에서 사용하는 서브넷에는 하나의 ASE만이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-157">Only the one ASE can exist in the subnet used by the ASE.</span></span> <span data-ttu-id="11563-158">ASE 이외의 항목에는 서브넷을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-158">The subnet cannot be used for anything other than the ASE</span></span>

### <a name="after-app-service-environment-v1-creation"></a><span data-ttu-id="11563-159">App Service Environment v1을 만든 이후</span><span class="sxs-lookup"><span data-stu-id="11563-159">After App Service Environment v1 creation</span></span>
<span data-ttu-id="11563-160">ASE를 만든 후 다음을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-160">After ASE creation you can adjust:</span></span>

* <span data-ttu-id="11563-161">프런트 엔드 수(최소: 2개)</span><span class="sxs-lookup"><span data-stu-id="11563-161">Quantity of Front Ends (minimum: 2)</span></span>
* <span data-ttu-id="11563-162">작업자 수(최소: 2개)</span><span class="sxs-lookup"><span data-stu-id="11563-162">Quantity of Workers (minimum: 2)</span></span>
* <span data-ttu-id="11563-163">IP SSL에 사용 가능한 IP 주소 수</span><span class="sxs-lookup"><span data-stu-id="11563-163">Quantity of IP addresses available for IP SSL</span></span>
* <span data-ttu-id="11563-164">프런트 엔드 또는 작업자에서 사용되는 계산 리소스 크기(프런트 엔드 최소 크기는 P2)</span><span class="sxs-lookup"><span data-stu-id="11563-164">Compute resource sizes used by the Front Ends or Workers (Front End minimum size is P2)</span></span>

<span data-ttu-id="11563-165">수동 크기 조정, App Service 환경 관리 및 모니터링에 대한 자세한 내용은 [App Service 환경을 구성하는 방법][ASEConfig]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-165">There are more details around manual scaling, management and monitoring of App Service Environments here: [How to configure an App Service Environment][ASEConfig]</span></span> 

<span data-ttu-id="11563-166">자동 크기 조정에 대한 정보는 여기에 가이드가 있습니다. [App Service 환경에 대한 자동 크기 조정을 구성하는 방법][ASEAutoscale]</span><span class="sxs-lookup"><span data-stu-id="11563-166">For information on autoscaling there is a guide here: [How to configure autoscale for an App Service Environment][ASEAutoscale]</span></span>

<span data-ttu-id="11563-167">데이터베이스 및 저장소와 같은 사용자 지정 항목에 사용할 수 없는 추가 종속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-167">There are additional dependencies that are not available for customization such as the database and storage.</span></span> <span data-ttu-id="11563-168">이러한 종속성은 Azure에 의해 처리되며 시스템과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-168">These are handled by Azure and come with the system.</span></span> <span data-ttu-id="11563-169">시스템 저장소는 전체 앱 서비스 환경에 대해 최대 500GB를 지원하고 데이터베이스는 시스템 규모의 필요에 따라 Azure에서 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="11563-169">The system storage supports up to 500 GB for the entire App Service Environment and the database is adjusted by Azure as needed by the scale of the system.</span></span>

## <a name="getting-started"></a><span data-ttu-id="11563-170">시작</span><span class="sxs-lookup"><span data-stu-id="11563-170">Getting started</span></span>
<span data-ttu-id="11563-171">앱 서비스 환경에 대한 모든 문서와 지침은 [응용 프로그램 서비스 환경의 추가 정보](../app-service/app-service-app-service-environments-readme.md)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11563-171">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="11563-172">App Service Environment v1을 시작하려면 [App Service Environment v1 소개][WhatisASE]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-172">To get started with App Service Environment v1, see [Introduction to the App Service Environment v1][WhatisASE]</span></span>

<span data-ttu-id="11563-173">Azure App Service 플랫폼에 대한 자세한 내용은 [Azure App Service][AzureAppService]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="11563-173">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
