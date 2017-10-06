---
title: aaaAzure IoT Suite FAQ | Microsoft Docs
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
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="3a804-103">IoT Suite에 대한 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="3a804-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="3a804-104">참고 항목, 연결 된 팩터리 특정 hello [FAQ](iot-suite-faq-cf.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="3a804-105">미리 구성 하는 hello 솔루션에 대 한 hello 소스 코드는 어디서 찾을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="3a804-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="3a804-106">hello 소스 코드는 다음 GitHub 리포지토리에 hello에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="3a804-107">[미리 구성된 원격 모니터링 솔루션][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="3a804-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="3a804-108">[예측 유지 관리 미리 구성된 솔루션][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="3a804-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="3a804-109">연결된 팩터리 미리 구성된 솔루션</span><span class="sxs-lookup"><span data-stu-id="3a804-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="3a804-110">Toohello 최신 버전의 hello 원격 모니터링 미리 구성 된 솔루션 사용 하 여 hello IoT Hub 장치 관리 기능을 업데이트 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="3a804-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="3a804-111">Hello https://www.azureiotsuite.com/ 사이트에서 미리 구성 된 솔루션을 배포 하는 경우 항상 hello hello 솔루션의 최신 버전의 새 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="3a804-112">Hello 명령줄을 사용 하는 미리 구성 된 솔루션을 배포 하는 경우에 새로운 코드와 함께 기존 배포를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="3a804-113">참조 [배포 클라우드] [ lnk-cloud-deployment] hello GitHub에서에서 [리포지토리][lnk-remote-monitoring-github]합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="3a804-114">새 장치 메서드 toohello 원격 모니터링 미리 구성 된 솔루션에 대 한 지원을 추가 하려면 어떻게 해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="3a804-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="3a804-115">Hello 섹션을 참조 [새 메서드 toohello 시뮬레이터에 대 한 지원을 추가] [ lnk-add-method] hello에 [미리 구성 된 솔루션을 사용자 지정] [ lnk-customize] 문서.</span><span class="sxs-lookup"><span data-stu-id="3a804-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="3a804-116">hello 시뮬레이션 된 장치를 무시 하 고 원하는 속성 변경 내용 이유?</span><span class="sxs-lookup"><span data-stu-id="3a804-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="3a804-117">Hello에는 솔루션 미리 구성 원격 모니터링, 시뮬레이션 된 hello 장치 코드만 사용 하 여 hello **Desired.Config.TemperatureMeanValue** 및 **Desired.Config.TelemetryInterval** 원하는 속성 tooupdate hello 속성을 보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="3a804-118">다른 모든 desired 속성 변경 요청은 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="3a804-119">내 장치가 hello hello 솔루션 대시보드 장치 목록에 나타나지 않으면 이유?</span><span class="sxs-lookup"><span data-stu-id="3a804-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="3a804-120">hello hello 솔루션 대시보드 장치 목록에는 장치는 쿼리 tooreturn hello 목록을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="3a804-121">현재 쿼리는 10K 이상의 장치를 반환할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="3a804-122">쿼리에 대 한 검색 조건을 hello 더 제한적인 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="3a804-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="3a804-123">Hello azureiotsuite.com에 미리 구성 된 솔루션에서 Azure 포털을 삭제 하는 hello에서 리소스 그룹을 삭제할 차이?</span><span class="sxs-lookup"><span data-stu-id="3a804-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="3a804-124">Hello 미리 구성 된 솔루션을 삭제 하면 [azureiotsuite.com][lnk-azureiotsuite], hello 미리 구성 된 솔루션을 만든 경우 프로 비전 된 모든 hello 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="3a804-125">추가 리소스 toohello 리소스 그룹을 추가한 경우 이러한 리소스도 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="3a804-126">Hello에 hello 리소스 그룹을 삭제 하는 경우 [Azure 포털][lnk-azure-portal]만 해당 리소스 그룹의 hello 리소스를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="3a804-127">또한 toodelete hello Azure Active Directory 응용 프로그램 hello에 미리 구성 하는 hello 솔루션과 관련 된 해야 [Azure 클래식 포털][lnk-classic-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="3a804-128">하나의 구독에 프로비전할 수 있는 IoT Hub 인스턴스는 몇 개인가요?</span><span class="sxs-lookup"><span data-stu-id="3a804-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="3a804-129">기본적으로 [구독당 10개의 IoT Hub][link-azuresublimits]를 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="3a804-130">만들 수는 [Azure 지원 티켓] [ link-azuresupportticket] tooraise이 한이도입니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="3a804-131">결과적으로 모든 미리 구성 된 솔루션은 새 IoT 허브를 프로 비전 이후 수 too10 프로 비전 미리 지정된 된 구독에서 솔루션을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="3a804-132">하나의 구독에 프로비전할 수 있는 Azure Cosmos DB 인스턴스는 몇 개인가요?</span><span class="sxs-lookup"><span data-stu-id="3a804-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="3a804-133">50개입니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-133">Fifty.</span></span> <span data-ttu-id="3a804-134">만들 수는 [Azure 지원 티켓] [ link-azuresupportticket] tooraise 제한이 있지만 기본적으로 하나만 제공할 수 있습니다 구독 당 50 개의 Cosmos DB 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="3a804-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="3a804-135">하나의 구독에 프로비전할 수 있는 무료 Bing 지도 API는 몇 개인가요?</span><span class="sxs-lookup"><span data-stu-id="3a804-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="3a804-136">2개입니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-136">Two.</span></span> <span data-ttu-id="3a804-137">두 개의 Enterprise용 내부 트랜잭션 Level 1 Bing Maps 계획을 Azure 구독에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="3a804-138">원격 모니터링 솔루션 hello hello 내부 트랜잭션 수준 1 계획과 기본적으로 프로 비전 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="3a804-139">결과적으로, 솔루션에서 수정 없이 구독을 모니터링 하 고 원격 tootwo를 하나만 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="3a804-140">정적 맵이 있는 원격 모니터링 솔루션 배포에서는 대화형 Bing 맵을 어떻게 추가하나요?</span><span class="sxs-lookup"><span data-stu-id="3a804-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="3a804-141">[Azure Portal][lnk-azure-portal]에서 엔터프라이즈용 Bing 맵 API QueryKey를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="3a804-142">Toohello hello에 엔터프라이즈에 대 한 Bing Maps API 인 리소스 그룹 이동 [Azure 포털][lnk-azure-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="3a804-143">**모든 설정**을 클릭한 다음 **키 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="3a804-144">**MasterKey**와 **QueryKey** 등, 두 개의 키를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="3a804-145">Hello 값을 복사 **QueryKey**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="3a804-146">엔터프라이즈용 Bing 맵 API 계정이 없는 경우</span><span class="sxs-lookup"><span data-stu-id="3a804-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="3a804-147">Hello에서 새로 만든 [Azure 포털] [ lnk-azure-portal] 클릭 하 여 + 새 toocreate 프롬프트 엔터프라이즈 및 수행에 대 한 Bing Maps API를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="3a804-148">Hello hello에서 최신 코드를 끌어올 [Azure IoT-원격 액세스 모니터링][lnk-remote-monitoring-github]합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="3a804-149">실행 중인 로컬 또는 클라우드 hello 명령줄 배포 지침 hello 저장소 hello /docs/ 폴더에 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="3a804-150">클라우드 배포를 봐 hello에 대 한 루트 폴더의 또는 로컬 실행 한 후 *. user.config 파일 배포 중에 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="3a804-151">텍스트 편집기에서 이 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="3a804-152">복사한 tooinclude hello 값 변경 hello 다음 줄에서는 프로그램 **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="3a804-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="3a804-153">DreamSpark용 Microsoft Azure가 있는 경우 사전 구성된 솔루션을 만들 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3a804-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="3a804-154">현재는 [DreamSpark용 Microsoft Azure][lnk-dreamspark] 계정을 사용하여 사전 구성된 솔루션을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="3a804-155">하지만 몇 분 이내에 [Azure용 평가판 계정][lnk-30daytrial]을 만들면 사전 구성된 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="3a804-156">CSP(클라우드 솔루션 공급자) 구독이 있는 경우 미리 구성된 솔루션을 만들 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="3a804-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="3a804-157">현재는 CSP(클라우드 솔루션 공급자) 구독이 있는 미리 구성된 솔루션을 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="3a804-158">하지만 몇 분 이내에 [Azure용 평가판 계정][lnk-30daytrial]을 만들면 사전 구성된 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a804-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="3a804-159">AAD 테넌트를 어떻게 삭제하나요?</span><span class="sxs-lookup"><span data-stu-id="3a804-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="3a804-160">Eric Golpe의 블로그 게시물 [Azure AD 테넌트 삭제 연습(영문)][lnk-delete-aad-tennant]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a804-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="3a804-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a804-161">Next steps</span></span>

<span data-ttu-id="3a804-162">탐색할 수도 있습니다 hello 중 일부 다른 기능 및 hello IoT Suite 미리 구성 된 솔루션의 기능:</span><span class="sxs-lookup"><span data-stu-id="3a804-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="3a804-163">[예측 정비 사전 구성 솔루션 개요][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="3a804-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="3a804-164">연결된 팩터리 미리 구성된 솔루션 개요</span><span class="sxs-lookup"><span data-stu-id="3a804-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="3a804-165">[Hello 접지에서 IoT 보안][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="3a804-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

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
