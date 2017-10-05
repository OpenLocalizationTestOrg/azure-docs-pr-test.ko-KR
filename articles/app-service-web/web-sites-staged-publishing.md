---
title: "Azure App Service에서 웹앱에 대한 스테이징 환경 설정| Microsoft Docs"
description: "Azure 앱 서비스에서 웹앱에 대한 준비된 개시를 사용하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: ca27c55eaaceb3109b1450c550330dfc416fdf55
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="4a89b-103">Azure App Service에서 스테이징 환경 설정</span><span class="sxs-lookup"><span data-stu-id="4a89b-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="4a89b-104">웹앱, Linux의 웹앱, 모바일 백 엔드 및 API 앱을 [App Service](http://go.microsoft.com/fwlink/?LinkId=529714)에 배포할 때 **표준** 또는 **프리미엄** App Service 계획 모드에서 실행하면 기본 프로덕션 슬롯 대신 별도의 배포 슬롯에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="4a89b-105">배포 슬롯은 실제로 고유한 호스트 이름이 있는 라이브 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="4a89b-106">앱 콘텐츠 및 구성 요소는 프로덕션 슬롯을 포함하여 두 배포 슬롯 간에 교환될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="4a89b-107">응용 프로그램을 배포 슬롯에 배포하면 다음과 같은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="4a89b-108">프로덕션 슬롯과 교환하기 전에 준비 배포 슬롯에서 앱 변경 사항의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="4a89b-109">먼저 슬롯으로 앱을 배포하고 프로덕션으로 교환하기 때문에 프로덕션으로 교환되기 전에 슬롯에 있는 모든 인스턴스가 준비되어 있는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="4a89b-110">따라서 앱을 배포할 때 가동 중지가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="4a89b-111">트래픽 리디렉션은 중단 없이 원활하게 수행되며 교환 작업으로 인해 삭제되는 요청은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="4a89b-112">사전 교환 유효성 검사가 필요하지 않은 경우 [자동 교환](#Auto-Swap) 을 구성하여 이 전체 워크플로를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="4a89b-113">교환 후에는 이전의 준비된 앱이 들어 있던 슬롯 안에 이전의 프로덕션 앱이 들어갑니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="4a89b-114">프로덕션 슬롯과 교환한 변경 내용이 예상과 다른 경우 같은 교환 작업을 즉시 수행하여 "마지막 양호 상태"로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="4a89b-115">각 앱 서비스 계획 모드는 다양한 수의 배포 슬롯을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="4a89b-116">앱 모드가 지원하는 슬롯의 수를 알아보려면 [App Service 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="4a89b-117">앱에 여러 슬롯이 있을 때에는 모드를 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="4a89b-118">프로덕션이 아닌 슬롯에 대해 크기 조정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="4a89b-119">연결된 리소스 관리는 프로덕션이 아닌 슬롯에 대해 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="4a89b-120">특별히 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715) 에서는 프로덕션이 아닌 슬롯을 다른 앱 서비스 계획으로 일시적으로 전환함으로써 프로덕션 슬롯에 미칠 수 있는 영향을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="4a89b-121">프로덕션 슬롯이 아닌 경우에는 두 슬롯을 교환하려면 프로덕션 슬롯과 같은 모드로 다시 한 번 공유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="4a89b-122">배포 슬롯 추가</span><span class="sxs-lookup"><span data-stu-id="4a89b-122">Add a deployment slot</span></span>
<span data-ttu-id="4a89b-123">여러 배포 슬롯을 사용하려면 앱이 **표준** 또는 **프리미엄** 모드에서 실행 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="4a89b-124">[Azure Portal](https://portal.azure.com/)에서 앱의 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="4a89b-125">**배포 슬롯** 옵션을 선택한 후 **슬롯 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![새 배포 슬롯 추가][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="4a89b-127">앱이 **표준** 또는 **프리미엄** 모드가 아닌 경우 준비된 게시를 사용하려면 지원 모델을 나타내는 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="4a89b-128">이때 **업그레이드**를 선택할 수 있는 옵션이 제공되고 계속하기 전에 앱의 **크기 조정** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="4a89b-129">**슬롯 추가** 블레이드에서 슬롯에 이름을 지정하고, 다른 기존 배포 슬롯으로부터 앱 구성을 복제할 것인지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="4a89b-130">확인 표시를 클릭하여 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-130">Click the check mark to continue.</span></span>
   
    ![구성 원본][ConfigurationSource1]
   
    <span data-ttu-id="4a89b-132">슬롯을 처음 추가할 때는 두 가지 선택만 가능합니다. 프로덕션의 기본 슬롯으로부터 구성을 복제하거나, 구성을 아예 복제하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="4a89b-133">여러 개의 슬롯을 만든 후에는 프로덕션이 아닌 슬롯으로부터 구성을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![구성 원본][MultipleConfigurationSources]
4. <span data-ttu-id="4a89b-135">앱의 리소스 블레이드에서 **배포 슬롯**을 클릭한 다음 배포 슬롯을 클릭하여 해당 슬롯의 리소스 블레이드를 엽니다. 그러면 다른 앱과 마찬가지로 메트릭 집합 및 구성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="4a89b-136">배포 슬롯을 보고 있다는 사실을 상기시키기 위해 블레이드 상단에 슬롯 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![배포 슬롯 제목][StagingTitle]
5. <span data-ttu-id="4a89b-138">슬롯의 블레이드에서 앱 URL을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="4a89b-139">배포 슬롯은 고유의 호스트 이름을 가지고 있고 Live App이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="4a89b-140">배포 슬롯에 대한 공용 액세스를 제한하려면 [앱 서비스 웹 앱 – 비 프로덕션 배포 슬롯에 대한 웹 액세스 차단](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="4a89b-141">배포 슬롯을 만든 후 콘텐츠가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="4a89b-142">다른 리포지토리 분기 또는 아예 다른 리포지토리로부터 슬롯에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="4a89b-143">슬롯의 구성을 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="4a89b-144">게시 프로필을 사용하거나 콘텐츠 업데이트를 위해 배포 슬롯에 연결된 배포 자격 증명을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="4a89b-145">예를 들어 [git를 사용하여 이 슬롯에 게시](app-service-deploy-local-git.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="4a89b-146">배포 슬롯의 구성</span><span class="sxs-lookup"><span data-stu-id="4a89b-146">Configuration for deployment slots</span></span>
<span data-ttu-id="4a89b-147">다른 배포 슬롯으로부터 구성을 복제할 때 복제된 구성을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="4a89b-148">또한, 교환 후(특정 슬롯) 다른 구성 요소는 동일한 슬롯에 남아 있지만 일부 구성 요소는 교환(특정 슬롯 아님)에 따라 콘텐츠를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="4a89b-149">다음 목록은 슬롯을 교환할 때 변경되는 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="4a89b-150">**교환된 설정**:</span><span class="sxs-lookup"><span data-stu-id="4a89b-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="4a89b-151">프레임워크 버전, 32/64비트, 웹 소켓과 같은 일반 설정</span><span class="sxs-lookup"><span data-stu-id="4a89b-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="4a89b-152">앱 설정(슬롯에 맞도록 구성할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="4a89b-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="4a89b-153">연결 설정(슬롯에 맞도록 구성할 수 있음)</span><span class="sxs-lookup"><span data-stu-id="4a89b-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="4a89b-154">처리기 매핑</span><span class="sxs-lookup"><span data-stu-id="4a89b-154">Handler mappings</span></span>
* <span data-ttu-id="4a89b-155">모니터링 및 진단 설정</span><span class="sxs-lookup"><span data-stu-id="4a89b-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="4a89b-156">WebJob 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="4a89b-156">WebJobs content</span></span>

<span data-ttu-id="4a89b-157">**교환되지 않은 설정**:</span><span class="sxs-lookup"><span data-stu-id="4a89b-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="4a89b-158">게시 끝점</span><span class="sxs-lookup"><span data-stu-id="4a89b-158">Publishing endpoints</span></span>
* <span data-ttu-id="4a89b-159">사용자 지정 도메인 이름</span><span class="sxs-lookup"><span data-stu-id="4a89b-159">Custom Domain Names</span></span>
* <span data-ttu-id="4a89b-160">SSL 인증서 및 바인딩</span><span class="sxs-lookup"><span data-stu-id="4a89b-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="4a89b-161">크기 조정 설정</span><span class="sxs-lookup"><span data-stu-id="4a89b-161">Scale settings</span></span>
* <span data-ttu-id="4a89b-162">WebJob 스케줄러</span><span class="sxs-lookup"><span data-stu-id="4a89b-162">WebJobs schedulers</span></span>

<span data-ttu-id="4a89b-163">슬롯에 맞도록(교환되지 않음) 앱 설정 또는 연결 문자열을 구성하려면 특정 슬롯에 대해 **응용 프로그램 설정** 블레이드에 액세스한 다음 슬롯에 맞아야 하는 구성 요소에 대한 **슬롯 설정** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="4a89b-164">특정 슬롯으로 구성 요소를 표시하면 앱과 연결된 모든 배포 슬롯에서 교환할 수 없도록 요소를 설정하는 효과가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![슬롯 설정][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="4a89b-166">배포 슬롯 교환</span><span class="sxs-lookup"><span data-stu-id="4a89b-166">Swap deployment slots</span></span> 
<span data-ttu-id="4a89b-167">앱 리소스 블레이드의 **개요** 또는 **배포 슬롯** 보기에서 배포 슬롯을 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a89b-168">배포 슬롯에서 프로덕션으로 앱을 교환하기 전에 특정 슬롯이 아닌 모든 설정이 해당 교환 대상에서 원하는 대로 정확히 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="4a89b-169">배포 슬롯을 교환하려면 앱의 명령 모음 또는 배포 슬롯의 명령 모음에서 **교환** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![교환 단추][SwapButtonBar]

2. <span data-ttu-id="4a89b-171">교환 원본 및 교환 대상이 제대로 설정되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="4a89b-172">일반적으로 교환 대상은 프로덕션 슬롯입니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="4a89b-173">**확인** 을 클릭하여 작업을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="4a89b-174">작업을 마치면 배포 슬롯이 교환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![전체 교환](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="4a89b-176">**미리 보기가 있는 교환** 교환 유형의 경우 [미리 보기가 있는 교환(다단계 교환)](#Multi-Phase)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="4a89b-177">미리 보기가 있는 교환(다단계 교환)</span><span class="sxs-lookup"><span data-stu-id="4a89b-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="4a89b-178">미리 보기가 있는 교환 또는 다단계 교환은 연결 문자열과 같은 슬롯 관련 구성 요소의 유효성 검사를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="4a89b-179">업무상 중요한 워크로드의 경우 프로덕션 슬롯의 구성이 적용될 때 앱이 예상대로 동작하는지 확인하려고 할 것입니다. 이러한 유효성 검사는 앱이 프로덕션으로 교환되기 *전에* 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="4a89b-180">미리 보기가 있는 교환이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="4a89b-181">미리 보기가 있는 교환은 Linux의 웹앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="4a89b-182">**미리 보기가 있는 교환** 옵션을 사용할 경우([배포 슬롯 교환](#Swap)) App Service에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-182">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="4a89b-183">대상 슬롯(예: 프로덕션)의 기존 워크로드가 영향을 받지 않도록 해당 슬롯을 변경되지 않은 상태로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-183">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="4a89b-184">슬롯별 연결 문자열 및 앱 설정을 포함하는 대상 슬롯의 구성 요소를 원본 슬롯에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-184">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="4a89b-185">앞에서 언급한 이러한 구성 요소를 사용하여 원본 슬롯에서 작업자 프로세스를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-185">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="4a89b-186">교환을 완료한 경우: 준비되기 전 원본 슬롯을 대상 슬롯으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-186">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="4a89b-187">대상 슬롯은 수동 교환에서와 같이 원본 슬롯으로 이동됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-187">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="4a89b-188">교환을 취소한 경우: 원본 슬롯의 구성 요소를 원본 슬롯에 다시 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-188">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="4a89b-189">앱이 대상 슬롯의 구성에서 동작하는 방식을 정확하게 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-189">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="4a89b-190">유효성 검사를 완료하면 별도 단계에서 교환을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-190">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="4a89b-191">이 단계는 원본 슬롯이 이미 원하는 구성으로 준비되고 클라이언트에서 가동 중지 시간이 발생하지 않는다는 추가적인 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-191">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="4a89b-192">다단계 교환에 사용 가능한 Azure PowerShell cmdlet 샘플은 배포 슬롯 섹션에 대한 Azure PowerShell cmdlet에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-192">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="4a89b-193">자동 교환 구성</span><span class="sxs-lookup"><span data-stu-id="4a89b-193">Configure Auto Swap</span></span>
<span data-ttu-id="4a89b-194">자동 교환은 앱의 최종 사용자를 위해 중단 시간 및 콜드 부팅이 발생하지 않는 앱을 지속적으로 배포하려는 DevOps 시나리오를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-194">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="4a89b-195">배포 슬롯이 자동 교환에 대해 프로덕션에 구성될 때, 해당 슬롯에 이미 준비된 후에 해당 슬롯에 코드 업데이트를 푸시할 때마다 App Service가 앱을 프로덕션으로 자동 교환합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a89b-196">슬롯에 대해 자동 교환을 사용할 때 슬롯 구성은 정확히 대상 슬롯(일반적으로 프로덕션 슬롯)에 의도한 구성이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-196">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="4a89b-197">자동 교환은 Linux의 웹앱에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="4a89b-198">슬롯에 대한 자동 교환 구성은 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="4a89b-199">다음 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-199">Follow the steps below:</span></span>

1. <span data-ttu-id="4a89b-200">**배포 슬롯**에서 비프로덕션 슬롯을 선택하고 해당 슬롯의 리소스 블레이드에서 **응용 프로그램 설정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="4a89b-201">**자동 교환**은 **켜기**로 선택하고 **자동 교환 슬롯**에서 원하는 대상 슬롯을 선택한 다음 명령 모음에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-201">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="4a89b-202">슬롯에 대한 구성은 정확히 대상 슬롯에 의도한 구성이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-202">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="4a89b-203">작업이 완료되면 **알림** 탭에 **성공**이 녹색으로 깜박입니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-203">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="4a89b-204">앱에 대한 자동 교환을 테스트하려면 먼저 **자동 교환 슬롯** 에서 비프로덕션 대상 슬롯을 선택하여 기능에 익숙해져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-204">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="4a89b-205">해당 배포 슬롯에 코드 푸시를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-205">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="4a89b-206">자동 교환은 짧은 시간 후에 발생하며 업데이트는 대상 슬롯의 URL에 반영됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-206">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="4a89b-207">교환 후 프로덕션 앱을 롤백하려면</span><span class="sxs-lookup"><span data-stu-id="4a89b-207">To rollback a production app after swap</span></span>
<span data-ttu-id="4a89b-208">슬롯 교환 후 프로덕션에서 오류가 발견되면 같은 두 슬롯을 즉시 교환하여 슬롯을 교환 전 상태로 롤백하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-208">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="4a89b-209">교환하기 전에 사용자 지정 준비</span><span class="sxs-lookup"><span data-stu-id="4a89b-209">Custom warm-up before swap</span></span>
<span data-ttu-id="4a89b-210">일부 앱에는 사용자 지정 준비 작업이 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="4a89b-211">web.config의 `applicationInitialization` 구성 요소를 사용하면 요청을 받기 전에 수행할 사용자 지정 초기화 작업을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-211">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="4a89b-212">스왑 작업은 이 사용자 지정 준비가 완료될 때까지 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-212">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="4a89b-213">샘플 web.config 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="4a89b-214">배포 슬롯을 삭제하려면</span><span class="sxs-lookup"><span data-stu-id="4a89b-214">To delete a deployment slot</span></span>
<span data-ttu-id="4a89b-215">배포 슬롯의 블레이드에서 배포 슬롯의 블레이드를 열고 **개요**(기본 페이지)를 클릭한 후 명령 모음에서 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-215">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![배포 슬롯 삭제][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="4a89b-217">배포 슬롯용 Azure PowerShell cmdlet</span><span class="sxs-lookup"><span data-stu-id="4a89b-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="4a89b-218">Azure PowerShell은 Windows PowerShell을 통해 Azure를 관리하기 위한 cmdlet을 제공하는 모듈로, Azure App Service에서 배포 슬롯을 관리하는 기능도 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-218">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="4a89b-219">Azure PowerShell을 설치 및 구성하는 방법과 Azure 구독에 Azure PowerShell을 인증하는 방법에 대한 자세한 내용은 [Microsoft Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="4a89b-220">웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="4a89b-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="4a89b-221">배포 슬롯 만들기</span><span class="sxs-lookup"><span data-stu-id="4a89b-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="4a89b-222">미리 보기가 있는 교환(다단계 교환) 시작 및 대상 슬롯 구성을 원본 슬롯에 적용</span><span class="sxs-lookup"><span data-stu-id="4a89b-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="4a89b-223">보류 중인 교환(검토가 있는 교환) 취소 및 원본 슬롯 구성 복원</span><span class="sxs-lookup"><span data-stu-id="4a89b-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="4a89b-224">배포 슬롯 교환</span><span class="sxs-lookup"><span data-stu-id="4a89b-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="4a89b-225">배포 슬롯 삭제</span><span class="sxs-lookup"><span data-stu-id="4a89b-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="4a89b-226">배포 슬롯에 대한 Azure CLI(Azure 명령줄 인터페이스) 명령</span><span class="sxs-lookup"><span data-stu-id="4a89b-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="4a89b-227">Azure CLI는 Azure 작업을 위한 플랫폼 간 명령을 제공하며, App Service 배포 슬롯을 관리하는 기능을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-227">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="4a89b-228">Azure CLI 설치 및 구성 지침과 Azure CLI를 Azure 구독에 연결하는 방법에 대한 자세한 내용은 [Azure CLI 설치 및 구성](../cli-install-nodejs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-228">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="4a89b-229">Azure CLI에서 Azure 앱 서비스에 사용할 수 있는 명령을 나열하려면 `azure site -h`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-229">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="4a89b-230">배포 슬롯에 대한 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 명령의 경우 [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a89b-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="4a89b-231">azure site list</span><span class="sxs-lookup"><span data-stu-id="4a89b-231">azure site list</span></span>
<span data-ttu-id="4a89b-232">현재 구독의 앱 관련 정보를 확인하려면 다음 예에서와 같이 **azure site list**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-232">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="4a89b-233">azure site create</span><span class="sxs-lookup"><span data-stu-id="4a89b-233">azure site create</span></span>
<span data-ttu-id="4a89b-234">배포 슬롯을 만들려면 다음 예에서와 같이 **azure site create**를 호출하고 기존 앱의 이름과 만들 슬롯의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-234">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="4a89b-235">새 슬롯의 소스 제어를 사용하도록 설정하려면 다음 예에서와 같이 **--git** 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-235">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="4a89b-236">azure site swap</span><span class="sxs-lookup"><span data-stu-id="4a89b-236">azure site swap</span></span>
<span data-ttu-id="4a89b-237">업데이트된 배포 슬롯을 프로덕션 앱으로 만들려면 다음 예에서와 같이 **azure site swap** 명령을 사용하여 교환 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-237">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="4a89b-238">이때 프로덕션 앱에는 중단 시간이나 콜드 부팅이 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-238">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="4a89b-239">azure site delete</span><span class="sxs-lookup"><span data-stu-id="4a89b-239">azure site delete</span></span>
<span data-ttu-id="4a89b-240">더 이상 필요하지 않은 배포 슬롯을 삭제하려면 다음 예에서와 같이 **azure site delete** 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-240">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="4a89b-241">작업에서 웹앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-241">See a web app in action.</span></span> <span data-ttu-id="4a89b-242">[앱 서비스 체험](https://azure.microsoft.com/try/app-service/) 에서는 신용 카드와 약정 없이 수명이 짧은 스타터 앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a89b-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4a89b-243">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4a89b-243">Next Steps</span></span>
<span data-ttu-id="4a89b-244">[Azure App Service 웹앱 - 비프로덕션 배포 슬롯에 대한 웹 액세스 차단(영문)](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Linux의 App Service 소개](./app-service-linux-intro.md)
[Microsoft Azure 평가판](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="4a89b-244">[Azure App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction to App Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

