---
title: "외부 Azure App Service Environment 만들기"
description: "앱 또는 독립 실행형을 만드는 동안 App Service Environment를 만드는 방법 설명"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 2dfe531facbe84aac65c5f787851c015de719fee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-external-app-service-environment"></a><span data-ttu-id="ef483-103">외부 App Service Environment 만들기</span><span class="sxs-lookup"><span data-stu-id="ef483-103">Create an External App Service environment</span></span> #

<span data-ttu-id="ef483-104">Azure App Service Environment는 Azure App Service를 Azure VNet(Virtual Network)의 서브넷에 배포한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="ef483-105">ASE(App Service Environment)에는 두 가지 배포 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-105">There are two ways to deploy an App Service environment (ASE):</span></span>

- <span data-ttu-id="ef483-106">외부 ASE라고도 하는 외부 IP 주소의 VIP 사용</span><span class="sxs-lookup"><span data-stu-id="ef483-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="ef483-107">내부 끝점이 ILB(내부 부하 분산 장치)이기 때문에 ILB ASE라고도 하는 내부 IP 주소의 VIP 사용</span><span class="sxs-lookup"><span data-stu-id="ef483-107">With the VIP on an internal IP address, often called an ILB ASE because the internal endpoint is an internal load balancer (ILB).</span></span>

<span data-ttu-id="ef483-108">이 문서에서는 외부 ASE를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-108">This article shows you how to create an External ASE.</span></span> <span data-ttu-id="ef483-109">ASE의 개요는 [App Service Environment에 대한 소개][Intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-109">For an overview of the ASE, see [An introduction to the App Service Environment][Intro].</span></span> <span data-ttu-id="ef483-110">ILB ASE를 만드는 방법에 대한 자세한 내용은 [ILB ASE 만들기 및 사용][MakeILBASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-110">For information on how to create an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="before-you-create-your-ase"></a><span data-ttu-id="ef483-111">ASE를 만들기 전에</span><span class="sxs-lookup"><span data-stu-id="ef483-111">Before you create your ASE</span></span> ##

<span data-ttu-id="ef483-112">ASE를 만든 후에는 다음을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-112">After you create your ASE, you can't change the following:</span></span>

- <span data-ttu-id="ef483-113">위치</span><span class="sxs-lookup"><span data-stu-id="ef483-113">Location</span></span>
- <span data-ttu-id="ef483-114">구독</span><span class="sxs-lookup"><span data-stu-id="ef483-114">Subscription</span></span>
- <span data-ttu-id="ef483-115">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="ef483-115">Resource group</span></span>
- <span data-ttu-id="ef483-116">사용되는 VNet</span><span class="sxs-lookup"><span data-stu-id="ef483-116">VNet used</span></span>
- <span data-ttu-id="ef483-117">사용되는 서브넷</span><span class="sxs-lookup"><span data-stu-id="ef483-117">Subnet used</span></span>
- <span data-ttu-id="ef483-118">서브넷 크기</span><span class="sxs-lookup"><span data-stu-id="ef483-118">Subnet size</span></span>

> [!NOTE]
> <span data-ttu-id="ef483-119">VNet을 선택하고 서브넷을 지정하는 경우 향후 성장을 수용하기에 충분한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-119">When you choose a VNet and specify a subnet, make sure that it's large enough to accommodate future growth.</span></span> <span data-ttu-id="ef483-120">주소 128개를 포함할 수 있는 `/25` 크기를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-120">We recommend a size of `/25` with 128 addresses.</span></span>
>

## <a name="three-ways-to-create-an-ase"></a><span data-ttu-id="ef483-121">ASE를 만드는 세 가지 방법</span><span class="sxs-lookup"><span data-stu-id="ef483-121">Three ways to create an ASE</span></span> ##

<span data-ttu-id="ef483-122">ASE를 만드는 세 가지 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-122">There are three ways to create an ASE:</span></span>

- <span data-ttu-id="ef483-123">**App Service 계획을 만들 때**.</span><span class="sxs-lookup"><span data-stu-id="ef483-123">**While creating an App Service plan**.</span></span> <span data-ttu-id="ef483-124">이 메서드는 한 번에 ASE 및 App Service 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-124">This method creates the ASE and the App Service plan in one step.</span></span>
- <span data-ttu-id="ef483-125">**독립 실행형 작업으로**.</span><span class="sxs-lookup"><span data-stu-id="ef483-125">**As a standalone action**.</span></span> <span data-ttu-id="ef483-126">이 메서드는 내부에 아무것도 포함되지 않은 ASE인 독립 실행형 ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-126">This method creates a standalone ASE, which is an ASE with nothing in it.</span></span> <span data-ttu-id="ef483-127">이 메서드는 ASE를 만드는 더 고급 수준의 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-127">This method is a more advanced process to create an ASE.</span></span> <span data-ttu-id="ef483-128">ILB를 사용하여 ASE를 만들 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-128">You use it to create an ASE with an ILB.</span></span>
- <span data-ttu-id="ef483-129">**Azure Resource Manager 템플릿에서**.</span><span class="sxs-lookup"><span data-stu-id="ef483-129">**From an Azure Resource Manager template**.</span></span> <span data-ttu-id="ef483-130">이 메서드는 고급 사용자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-130">This method is for advanced users.</span></span> <span data-ttu-id="ef483-131">자세한 내용은 [템플릿에서 ASE 만들기][MakeASEfromTemplate]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-131">For more information, see [Create an ASE from a template][MakeASEfromTemplate].</span></span>

<span data-ttu-id="ef483-132">외부 ASE에는 공용 VIP가 있습니다. 즉, ASE의 앱에 대한 모든 HTTP/HTTPS 트래픽이 인터넷 액세스가 가능한 IP 주소에 도달합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-132">An External ASE has a public VIP, which means that all HTTP/HTTPS traffic to the apps in the ASE hits an internet-accessible IP address.</span></span> <span data-ttu-id="ef483-133">ILB를 사용하는 ASE에는 ASE에서 사용하는 서브넷의 IP 주소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-133">An ASE with an ILB has an IP address from the subnet used by the ASE.</span></span> <span data-ttu-id="ef483-134">ILB ASE에 호스팅된 앱은 인터넷에 직접 노출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-134">The apps hosted in an ILB ASE aren't exposed directly to the internet.</span></span>

## <a name="create-an-ase-and-an-app-service-plan-together"></a><span data-ttu-id="ef483-135">ASE 및 App Service 계획 만들기</span><span class="sxs-lookup"><span data-stu-id="ef483-135">Create an ASE and an App Service plan together</span></span> ##

<span data-ttu-id="ef483-136">App Service 계획은 앱의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-136">The App Service plan is a container of apps.</span></span> <span data-ttu-id="ef483-137">App Service에서 앱을 만드는 경우 App Service 계획을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-137">When you create an app in App Service, you choose or create an App Service plan.</span></span> <span data-ttu-id="ef483-138">컨테이너 모델 환경은 App Service 계획을 포함하고 App Service 계획은 앱을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-138">The container model environments hold App Service plans, and App Service plans hold apps.</span></span>

<span data-ttu-id="ef483-139">App Service 계획을 만들면서 ASE를 만드는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-139">To create an ASE while you create an App Service plan:</span></span>

1. <span data-ttu-id="ef483-140">[Azure Portal](https://portal.azure.com/)에서 **새로 만들기** > **웹 + 모바일** > **웹앱**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-140">In the [Azure portal](https://portal.azure.com/), select **New** > **Web + Mobile** > **Web App**.</span></span>

    ![웹앱 만들기][1]

2. <span data-ttu-id="ef483-142">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-142">Select your subscription.</span></span> <span data-ttu-id="ef483-143">앱 및 ASE는 동일한 구독에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-143">The app and the ASE are created in the same subscriptions.</span></span>

3. <span data-ttu-id="ef483-144">리소스 그룹을 선택하거나 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-144">Select or create a resource group.</span></span> <span data-ttu-id="ef483-145">리소스 그룹을 사용하여 관련된 Azure 리소스를 하나의 단위로 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-145">With resource groups, you can manage related Azure resources as a unit.</span></span> <span data-ttu-id="ef483-146">리소스 그룹은 앱에 대해 역할 기반 액세스 제어 규칙을 설정하려는 경우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-146">Resource groups also are useful when you establish Role-Based Access Control rules for your apps.</span></span> <span data-ttu-id="ef483-147">자세한 내용은 [Azure Resource Manager 개요][ARMOverview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-147">For more information, see the [Azure Resource Manager overview][ARMOverview].</span></span>

4. <span data-ttu-id="ef483-148">App Service 계획을 선택한 다음 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-148">Select the App Service plan, and then select **Create New**.</span></span>

    ![새 App Service 계획][2]

5. <span data-ttu-id="ef483-150">**위치** 드롭다운 목록에서 ASE를 만들려는 영역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-150">In the **Location** drop-down list, select the region where you want to create the ASE.</span></span> <span data-ttu-id="ef483-151">기존 ASE를 선택하는 경우 새 ASE가 생성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-151">If you select an existing ASE, a new ASE isn't created.</span></span> <span data-ttu-id="ef483-152">App Service 계획이 선택한 ASE에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-152">The App Service plan is created in the ASE that you selected.</span></span> 

6. <span data-ttu-id="ef483-153">**가격 책정 계층**을 선택하고, **격리** 가격 책정 SKU 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-153">Select **Pricing tier**, and choose one of the **Isolated** pricing SKUs.</span></span> <span data-ttu-id="ef483-154">**격리** SKU 카드를 선택하고 ASE가 아닌 위치를 선택하면 새 ASE가 해당 위치에 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-154">If you choose an **Isolated** SKU card and a location that's not an ASE, a new ASE is created in that location.</span></span> <span data-ttu-id="ef483-155">ASE를 만드는 프로세스를 시작하려면 **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-155">To start the process to create an ASE, select **Select**.</span></span> <span data-ttu-id="ef483-156">**격리** SKU는 ASE에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-156">The **Isolated** SKU is available only in conjunction with an ASE.</span></span> <span data-ttu-id="ef483-157">또한 **격리**가 아닌 ASE의 다른 가격 책정 SKU를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-157">You also can't use any other pricing SKU in an ASE other than **Isolated**.</span></span>

    ![가격 책정 계층 선택][3]

7. <span data-ttu-id="ef483-159">ASE의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-159">Enter the name for your ASE.</span></span> <span data-ttu-id="ef483-160">이 이름은 앱에 주소를 지정할 수 있는 이름에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-160">This name is used in the addressable name for your apps.</span></span> <span data-ttu-id="ef483-161">ASE의 이름이 _appsvcenvdemo_인 경우 도메인 이름은 *.appsvcenvdemo.p.azurewebsites.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-161">If the name of the ASE is _appsvcenvdemo_, the domain name is *.appsvcenvdemo.p.azurewebsites.net*.</span></span> <span data-ttu-id="ef483-162">*mytestapp*이라는 앱을 만든 경우 mytestapp.appsvcenvdemo.p.azurewebsites.net으로 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-162">If you create an app named *mytestapp*, it's addressable at mytestapp.appsvcenvdemo.p.azurewebsites.net.</span></span> <span data-ttu-id="ef483-163">이름에 공백을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-163">You can't use white space in the name.</span></span> <span data-ttu-id="ef483-164">대문자를 사용한 경우 도메인 이름은 해당 이름의 소문자 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-164">If you use uppercase characters, the domain name is the total lowercase version of that name.</span></span>

    ![새 App Service 계획 이름][4]

8. <span data-ttu-id="ef483-166">Azure 가상 네트워킹 세부 정보를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-166">Specify your Azure virtual networking details.</span></span> <span data-ttu-id="ef483-167">**새로 만들기** 또는 **기존 항목 선택** 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-167">Select either **Create New** or **Select Existing**.</span></span> <span data-ttu-id="ef483-168">선택한 영역에 VNet이 있는 경우에만 기존 VNet을 선택할 수 있는 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-168">The option to select an existing VNet is available only if you have a VNet in the selected region.</span></span> <span data-ttu-id="ef483-169">**새로 만들기**를 선택한 경우 VNet에 대한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-169">If you select **Create New**, enter a name for the VNet.</span></span> <span data-ttu-id="ef483-170">해당 이름으로 새로운 Resource Manager VNet이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-170">A new Resource Manager VNet with that name is created.</span></span> <span data-ttu-id="ef483-171">선택한 지역의 주소 공간 `192.168.250.0/23`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-171">It uses the address space `192.168.250.0/23` in the selected region.</span></span> <span data-ttu-id="ef483-172">**기존 항목 선택**을 선택하는 경우 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-172">If you select **Select Existing**, you need to:</span></span>

    <span data-ttu-id="ef483-173">a.</span><span class="sxs-lookup"><span data-stu-id="ef483-173">a.</span></span> <span data-ttu-id="ef483-174">여러 개의 항목이 있는 경우 VNet 주소 블록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-174">Select the VNet address block, if you have more than one.</span></span>

    <span data-ttu-id="ef483-175">b.</span><span class="sxs-lookup"><span data-stu-id="ef483-175">b.</span></span> <span data-ttu-id="ef483-176">새 서브넷 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-176">Enter a new subnet name.</span></span>

    <span data-ttu-id="ef483-177">c.</span><span class="sxs-lookup"><span data-stu-id="ef483-177">c.</span></span> <span data-ttu-id="ef483-178">서브넷의 크기를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-178">Select the size of the subnet.</span></span> <span data-ttu-id="ef483-179">*ASE의 향후 증가에 맞게 충분히 큰 크기를 설정해야 합니다.*</span><span class="sxs-lookup"><span data-stu-id="ef483-179">*Remember to select a size large enough to accommodate future growth of your ASE.*</span></span> <span data-ttu-id="ef483-180">권장되는 크기는 `/25`입니다. 여기에는 128개의 주소가 있고 최대 크기의 ASE를 다룰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-180">We recommend `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="ef483-181">예를 들어 16개의 주소만을 사용할 수 있기 때문에 `/28`은 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-181">We don't recommend `/28`, for example, because only 16 addresses are available.</span></span> <span data-ttu-id="ef483-182">인프라는 최소 5개의 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-182">Infrastructure uses at least five addresses.</span></span> <span data-ttu-id="ef483-183">`/28` 서브넷에서 11개 인스턴스의 최대 확장이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-183">In a `/28` subnet, you're left with a maximum scaling of 11 instances.</span></span>

    <span data-ttu-id="ef483-184">d.</span><span class="sxs-lookup"><span data-stu-id="ef483-184">d.</span></span> <span data-ttu-id="ef483-185">서브넷 IP 범위를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-185">Select the subnet IP range.</span></span>

9. <span data-ttu-id="ef483-186">**만들기**를 선택하여 ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-186">Select **Create** to create the ASE.</span></span> <span data-ttu-id="ef483-187">App Service 계획 및 앱이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-187">This process also creates the App Service plan and the app.</span></span> <span data-ttu-id="ef483-188">ASE, App Service 계획 및 앱은 동일한 구독 및 동일한 리소스 그룹에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-188">The ASE, App Service plan, and app are all under the same subscription and also in the same resource group.</span></span> <span data-ttu-id="ef483-189">ASE에 별도 리소스 그룹이 필요하거나 ILB ASE가 필요한 경우 단계에 따라 단독으로 ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-189">If your ASE needs a separate resource group or if you need an ILB ASE, follow the steps to create an ASE by itself.</span></span>

## <a name="create-an-ase-by-itself"></a><span data-ttu-id="ef483-190">단독으로 ASE 만들기</span><span class="sxs-lookup"><span data-stu-id="ef483-190">Create an ASE by itself</span></span> ##

<span data-ttu-id="ef483-191">ASE 독립 실행형을 만드는 경우 내부에는 아무것도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-191">If you create an ASE standalone, it has nothing in it.</span></span> <span data-ttu-id="ef483-192">빈 ASE도 여전히 인프라에 대한 월별 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-192">An empty ASE still incurs a monthly charge for the infrastructure.</span></span> <span data-ttu-id="ef483-193">ILB를 사용하여 ASE를 만들거나 고유한 리소스 그룹에서ASE를 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-193">Follow these steps to create an ASE with an ILB or to create an ASE in its own resource group.</span></span> <span data-ttu-id="ef483-194">ASE를 만든 후에 기본 프로세스를 사용하여 앱을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-194">After you create your ASE, you can create apps in it by using the normal process.</span></span> <span data-ttu-id="ef483-195">위치로 새 ASE를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-195">Select your new ASE as the location.</span></span>

1. <span data-ttu-id="ef483-196">Azure Marketplace에서 **App Service Environment**를 검색하거나 **새로 만들기** > **웹 모바일** > **App Service Environment**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-196">Search the Azure Marketplace for **App Service Environment**, or select **New** > **Web Mobile** > **App Service Environment**.</span></span> 

2. <span data-ttu-id="ef483-197">ASE의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-197">Enter the name of your ASE.</span></span> <span data-ttu-id="ef483-198">이 이름은 ASE에서 만든 앱에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-198">This name is used for the apps created in the ASE.</span></span> <span data-ttu-id="ef483-199">이름이 *mynewdemoase*인 경우 하위 도메인 이름은 *.mynewdemoase.p.azurewebsites.net*입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-199">If the name is *mynewdemoase*, the subdomain name is *.mynewdemoase.p.azurewebsites.net*.</span></span> <span data-ttu-id="ef483-200">*mytestapp*이라는 앱을 만든 경우 mytestapp.mynewdemoase.p.azurewebsites.net으로 주소를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-200">If you create an app named *mytestapp*, it's addressable at mytestapp.mynewdemoase.p.azurewebsites.net.</span></span> <span data-ttu-id="ef483-201">이름에 공백을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-201">You can't use white space in the name.</span></span> <span data-ttu-id="ef483-202">대문자를 사용한 경우 도메인 이름은 해당 이름의 소문자 버전이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-202">If you use uppercase characters, the domain name is the total lowercase version of the name.</span></span> <span data-ttu-id="ef483-203">ILB를 사용하는 경우 ASE 이름이 하위 도메인에서 사용되지 않는 대신 ASE를 만드는 동안에 명시적으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-203">If you use an ILB, your ASE name isn't used in your subdomain but is instead explicitly stated during ASE creation.</span></span>

    ![ASE 이름 지정][5]

3. <span data-ttu-id="ef483-205">사용 중인 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-205">Select your subscription.</span></span> <span data-ttu-id="ef483-206">또한 이 구독은 ASE의 모든 앱이 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-206">This subscription is also the one that all apps in the ASE use.</span></span> <span data-ttu-id="ef483-207">다른 구독에 있는 VNet에 ASE를 배치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-207">You can't put your ASE in a VNet that's in another subscription.</span></span>

4. <span data-ttu-id="ef483-208">새 리소스 그룹을 선택하거나 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-208">Select or specify a new resource group.</span></span> <span data-ttu-id="ef483-209">ASE에 사용되는 리소스 그룹은 VNet에 사용되는 것과 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-209">The resource group used for your ASE must be the same one that's used for your VNet.</span></span> <span data-ttu-id="ef483-210">기존 VNet을 선택하는 경우 ASE에 대한 리소스 그룹을 선택하는 작업은 VNet의 선택을 반영하도록 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-210">If you select an existing VNet, the resource group selection for your ASE is updated to reflect that of your VNet.</span></span> <span data-ttu-id="ef483-211">*Resource Manager 템플릿을 사용하는 경우 VNet 리소스 그룹과 다른 리소스 그룹으로 ASE를 만들 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="ef483-211">*You can create an ASE with a resource group that is different from the VNet resource group if you use a Resource Manager template.*</span></span> <span data-ttu-id="ef483-212">템플릿에서 ASE를 만들려면 [템플릿에서 App Service Environment 만들기][MakeASEfromTemplate]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-212">To create an ASE from a template, see [Create an App Service environment from a template][MakeASEfromTemplate].</span></span>

    ![리소스 그룹 선택][6]

5. <span data-ttu-id="ef483-214">VNet 및 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-214">Select your VNet and location.</span></span> <span data-ttu-id="ef483-215">새 VNet을 만들거나 기존 VNet을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-215">You can create a new VNet or select an existing VNet:</span></span> 

    * <span data-ttu-id="ef483-216">새 VNet을 선택하면 이름 및 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-216">If you select a new VNet, you can specify a name and location.</span></span> <span data-ttu-id="ef483-217">새 VNet의 주소 범위는 192.168.250.0/23이고 default라는 서브넷이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-217">The new VNet has the address range 192.168.250.0/23 and a subnet named default.</span></span> <span data-ttu-id="ef483-218">서브넷은 192.168.250.0/24로 정의되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-218">The subnet is defined as 192.168.250.0/24.</span></span> <span data-ttu-id="ef483-219">Resource Manager VNet만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-219">You can only select a Resource Manager VNet.</span></span> <span data-ttu-id="ef483-220">**VIP 형식**을 선택하면 ASE가 인터넷(외부)에서 직접 액세스할 수 있는지 또는 ILB를 사용하는지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-220">The **VIP Type** selection determines if your ASE can be directly accessed from the internet (External) or if it uses an ILB.</span></span> <span data-ttu-id="ef483-221">이러한 옵션에 대한 자세한 내용은 [App Service Environment에서 내부 부하 분산 장치 만들기 및 사용][MakeILBASE]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-221">To learn more about these options, see [Create and use an internal load balancer with an App Service environment][MakeILBASE].</span></span> 

      * <span data-ttu-id="ef483-222">**VIP 형식**에 **외부**를 선택하면 시스템이 IP 기반 SSL 목적으로 만들 수 있는 외부 IP 주소의 개수를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-222">If you select **External** for the **VIP Type**, you can select how many external IP addresses the system is created with for IP-based SSL purposes.</span></span> 
    
      * <span data-ttu-id="ef483-223">**VIP 형식**에 **내부**를 선택하면 ASE가 사용하는 도메인을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-223">If you select **Internal** for the **VIP Type**, you must specify the domain that your ASE uses.</span></span> <span data-ttu-id="ef483-224">공개 또는 개인 주소 범위를 사용하는 VNet으로 ASE를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-224">You can deploy an ASE into a VNet that uses public or private address ranges.</span></span> <span data-ttu-id="ef483-225">공용 주소 범위를 가진 VNet을 사용하려면 사전에 VNet을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-225">To use a VNet with a public address range, you need to create the VNet ahead of time.</span></span> 
    
    * <span data-ttu-id="ef483-226">기존 VNet을 선택한 경우 새 서브넷은 ASE를 만들 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-226">If you select an existing VNet, a new subnet is created when the ASE is created.</span></span> <span data-ttu-id="ef483-227">*포털에서 미리 생성된 서브넷을 사용할 수 없습니다. Resource Manager 템플릿을 사용하는 경우 기존 서브넷으로 ASE를 만들 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="ef483-227">*You can't use a pre-created subnet in the portal. You can create an ASE with an existing subnet if you use a Resource Manager template.*</span></span> <span data-ttu-id="ef483-228">템플릿에서 ASE를 만들려면 [템플릿에서 App Service Environment 만들기][MakeASEfromTemplate]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-228">To create an ASE from a template, see [Create an App Service Environment from a template][MakeASEfromTemplate].</span></span>

## <a name="app-service-environment-v1"></a><span data-ttu-id="ef483-229">App Service 환경 v1</span><span class="sxs-lookup"><span data-stu-id="ef483-229">App Service Environment v1</span></span> ##

<span data-ttu-id="ef483-230">여전히 ASEv1(첫 번째 버전의 App Service Environment)의 인스턴스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-230">You can still create instances of the first version of App Service Environment (ASEv1).</span></span> <span data-ttu-id="ef483-231">해당 프로세스를 시작하려면 Marketplace에서 **App Service Environment v1**을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-231">To start that process, search the Marketplace for **App Service Environment v1**.</span></span> <span data-ttu-id="ef483-232">독립 실행형 ASE를 만드는 동일한 방식으로 ASE를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-232">You create the ASE in the same way that you create the standalone ASE.</span></span> <span data-ttu-id="ef483-233">완료되면 ASEv1에 두 개의 프런트 엔드 및 두 명의 작업자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-233">When it's finished, your ASEv1 has two front ends and two workers.</span></span> <span data-ttu-id="ef483-234">ASEv1을 사용하면 프런트 엔드와 작업자를 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-234">With ASEv1, you must manage the front ends and workers.</span></span> <span data-ttu-id="ef483-235">이는 App Service 계획을 만들 때 자동으로 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-235">They're not automatically added when you create your App Service plans.</span></span> <span data-ttu-id="ef483-236">프런트 엔드는 HTTP/HTTPS 끝점으로 작동하여 작업자로 트래픽을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-236">The front ends act as the HTTP/HTTPS endpoints and send traffic to the workers.</span></span> <span data-ttu-id="ef483-237">작업자는 사용자 앱을 호스트하는 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-237">The workers are the roles that host your apps.</span></span> <span data-ttu-id="ef483-238">ASE를 만든 후 프런트 엔드 및 작업자의 수량을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ef483-238">You can adjust the quantity of front ends and workers after you create your ASE.</span></span> 

<span data-ttu-id="ef483-239">ASEv1에 대해 자세히 알아보려면 [App Service Environment v1 소개][ASEv1Intro]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-239">To learn more about ASEv1, see [Introduction to the App Service Environment v1][ASEv1Intro].</span></span> <span data-ttu-id="ef483-240">ASEv1의 크기 조정, 관리 및 모니터링에 대한 자세한 내용은 [App Service Environment를 구성하는 방법][ConfigureASEv1]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ef483-240">For more information on scaling, managing, and monitoring ASEv1, see [How to configure an App Service Environment][ConfigureASEv1].</span></span>

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
