---
title: Azure IoT Suite FAQ | Microsoft Docs
description: "IoT Suite에 대한 질문과 대답"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="00413-103">IoT Suite에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="00413-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="00413-104">연결된 팩터리 관련 [FAQ](iot-suite-faq-cf.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00413-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="00413-105">어디에서 미리 구성된 솔루션의 소스 코드를 찾을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="00413-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="00413-106">소스 코드는 다음 GitHub 리포지토리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="00413-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="00413-107">[미리 구성된 원격 모니터링 솔루션][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="00413-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="00413-108">[예측 유지 관리 미리 구성된 솔루션][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="00413-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="00413-109">연결된 팩터리 미리 구성된 솔루션</span><span class="sxs-lookup"><span data-stu-id="00413-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="00413-110">IoT Hub 장치 관리 기능을 사용하는 미리 구성된 원격 모니터링 솔루션을 최신 버전으로 업데이트하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="00413-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="00413-111">https://www.azureiotsuite.com/ 사이트에서 미리 구성된 솔루션을 배포하는 경우 항상 최신 버전의 솔루션의 새 인스턴스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="00413-112">명령줄을 사용하여 미리 구성된 솔루션을 배포하는 경우 새 코드와 함께 기존 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="00413-113">GitHub [리포지토리][lnk-remote-monitoring-github]에서 [클라우드 배포][lnk-cloud-deployment]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00413-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="00413-114">미리 구성된 원격 모니터링 솔루션에 새 장치 메서드에 대한 지원을 어떻게 추가할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="00413-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="00413-115">[미리 구성된 솔루션 사용자 지정][lnk-customize] 문서에서 [시뮬레이터에 새 메서드에 대한 지원 추가][lnk-add-method] 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00413-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="00413-116">시뮬레이션된 장치가 desired 속성 변경을 무시하고 있는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="00413-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="00413-117">미리 구성된 원격 모니터링 솔루션에서 시뮬레이션된 장치 코드는 **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** desired 속성만을 사용하여 reported 속성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="00413-118">다른 모든 desired 속성 변경 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00413-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="00413-119">내 장치가 솔루션 대시보드의 장치 목록에 나타나지 않는 이유는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="00413-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="00413-120">솔루션 대시보드의 장치 목록은 쿼리를 사용하여 장치 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="00413-121">현재 쿼리는 10K 이상의 장치를 반환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="00413-122">쿼리에 대한 검색 조건을 더 제한적으로 설정해 보세요.</span><span class="sxs-lookup"><span data-stu-id="00413-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="00413-123">Azure 포털에서 리소스 그룹을 삭제하는 것과 azureiotsuite.com의 미리 구성된 솔루션에서 삭제를 클릭하는 것의 차이는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="00413-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="00413-124">[azureiotsuite.com][lnk-azureiotsuite]에서 미리 구성된 솔루션을 삭제하면, 미리 구성된 솔루션을 만들 때 프로비전된 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="00413-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="00413-125">리소스 그룹에 리소스를 추가하면 이들 역시 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="00413-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="00413-126">[Azure Portal][lnk-azure-portal]에서 리소스 그룹을 삭제하는 경우 해당 리소스 그룹에서 리소스만 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="00413-127">또한 [Azure 클래식 포털][lnk-classic-portal]에 미리 구성된 솔루션과 연결된 Azure Active Directory 응용 프로그램을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="00413-128">하나의 구독에 프로비전할 수 있는 IoT Hub 인스턴스는 몇 개인가요?</span><span class="sxs-lookup"><span data-stu-id="00413-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="00413-129">기본적으로 [구독당 10개의 IoT Hub][link-azuresublimits]를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="00413-130">[Azure 지원 티켓][link-azuresupportticket]을 만들어 이 제한을 높일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="00413-131">결과적으로 미리 구성된 모든 솔루션이 새 IoT Hub를 프로비전하기 때문에 지정된 구독에서 최대 10개의 미리 구성된 솔루션을 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="00413-132">하나의 구독에 프로비전할 수 있는 Azure Cosmos DB 인스턴스는 몇 개인가요?</span><span class="sxs-lookup"><span data-stu-id="00413-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="00413-133">50개입니다.</span><span class="sxs-lookup"><span data-stu-id="00413-133">Fifty.</span></span> <span data-ttu-id="00413-134">[Azure 지원 티켓][link-azuresupportticket]을 만들어서 이 한도를 높일 수 있지만, 기본적으로 구독당 Cosmos DB 인스턴스를 50개만 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="00413-135">하나의 구독에 프로비전할 수 있는 무료 Bing 지도 API는 몇 개인가요?</span><span class="sxs-lookup"><span data-stu-id="00413-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="00413-136">2개입니다.</span><span class="sxs-lookup"><span data-stu-id="00413-136">Two.</span></span> <span data-ttu-id="00413-137">두 개의 Enterprise용 내부 트랜잭션 Level 1 Bing Maps 계획을 Azure 구독에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="00413-138">원격 모니터링 솔루션이 내부 트랜젝션 Level 1 계획을 사용하여 기본으로 프로비전됩니다.</span><span class="sxs-lookup"><span data-stu-id="00413-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="00413-139">결과적으로 구독에 원격 모니터링 솔루션을 가감 없이 2개까지만 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="00413-140">정적 맵이 있는 원격 모니터링 솔루션 배포에서는 대화형 Bing 맵을 어떻게 추가하나요?</span><span class="sxs-lookup"><span data-stu-id="00413-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="00413-141">[Azure Portal][lnk-azure-portal]에서 엔터프라이즈용 Bing 맵 API QueryKey를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="00413-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="00413-142">[Azure Portal][lnk-azure-portal]에서 엔터프라이즈용 Bing 맵 API가 있는 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="00413-143">**모든 설정**을 클릭한 다음 **키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="00413-144">**MasterKey**와 **QueryKey** 등, 두 개의 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="00413-145">**QueryKey**에 대한 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="00413-146">엔터프라이즈용 Bing 맵 API 계정이 없는 경우</span><span class="sxs-lookup"><span data-stu-id="00413-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="00413-147">[Azure Portal][lnk-azure-portal]에서 + 새로 만들기를 클릭하고 엔터프라이즈용 Bing 맵 API를 검색한 다음 지침에 따라 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00413-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="00413-148">[Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github]에서 최신 코드를 풀다운합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="00413-149">저장소의 /docs/ 폴더에서 명령줄 배포 지침에 따라 로컬 또는 클라우드 배포를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="00413-150">로컬 또는 클라우드 배포를 실행한 후에는 루트 폴더에서 배포 중에 *.user.config 파일이 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="00413-151">텍스트 편집기에서 이 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="00413-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="00413-152">**QueryKey**에서 복사한 값을 포함하도록 다음 줄을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="00413-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="00413-153">DreamSpark용 Microsoft Azure가 있는 경우 사전 구성된 솔루션을 만들 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="00413-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="00413-154">현재는 [DreamSpark용 Microsoft Azure][lnk-dreamspark] 계정을 사용하여 사전 구성된 솔루션을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="00413-155">하지만 몇 분 이내에 [Azure용 평가판 계정][lnk-30daytrial]을 만들면 사전 구성된 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="00413-156">CSP(클라우드 솔루션 공급자) 구독이 있는 경우 미리 구성된 솔루션을 만들 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="00413-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="00413-157">현재는 CSP(클라우드 솔루션 공급자) 구독이 있는 미리 구성된 솔루션을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="00413-158">하지만 몇 분 이내에 [Azure용 평가판 계정][lnk-30daytrial]을 만들면 사전 구성된 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="00413-159">AAD 테넌트를 어떻게 삭제하나요?</span><span class="sxs-lookup"><span data-stu-id="00413-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="00413-160">Eric Golpe의 블로그 게시물 [Azure AD 테넌트 삭제 연습(영문)][lnk-delete-aad-tennant]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00413-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="00413-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00413-161">Next steps</span></span>

<span data-ttu-id="00413-162">미리 구성된 IoT Suite 솔루션의 몇 가지 다른 기능 및 기능을 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00413-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="00413-163">[예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="00413-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="00413-164">연결된 팩터리 미리 구성된 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="00413-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="00413-165">[처음부터 IoT 보안을 고려][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="00413-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
