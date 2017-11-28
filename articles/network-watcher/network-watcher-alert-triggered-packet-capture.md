---
title: "aaaUse 패킷 캡처 toodo 자동 관리 경고 및 Azure 함수를 사용 하 여 모니터링 네트워크 | Microsoft Docs"
description: "이 문서에서 설명 하는 경고 toocreate Azure 네트워크 감시자가 있는 패킷 캡처를 실행 하는 방법"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="262d6-103">경고 및 Azure Functions를 통한 사전 네트워크 모니터링을 위해 패킷 캡처 사용</span><span class="sxs-lookup"><span data-stu-id="262d6-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="262d6-104">네트워크 감시자 패킷 캡처 가상 컴퓨터 내부 및 외부로 tootrack 트래픽 캡처 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="262d6-105">hello 캡처 파일에 있을 수 정의 된 필터 tootrack 트래픽 toomonitor 한다는 것을 hello만 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="262d6-106">이 데이터는 다음 저장소 blob에 아니면 hello 게스트 컴퓨터에 로컬로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="262d6-107">이 기능은 Azure Functions와 같은 다른 자동화 시나리오에서 원격으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="262d6-108">패킷 캡처 제공 기능 toorun 사전 캡처에 따라 hello 네트워크 변칙을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="262d6-109">또한 네트워크 침입에 대한 정보를 가져오는 네트워크 통계를 수집하는 것을 포함하여 클라이언트 서버 간 통신을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="262d6-110">Azure에 배포된 리소스는 연중 무휴(24/7) 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="262d6-111">모든 리소스 24/7의 hello 상태를, 직원 능동적으로 모니터링할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="262d6-112">예를 들어 오전 2시에 문제가 발생하면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="262d6-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="262d6-113">네트워크 감시자를 사용 하 여 경고 및 hello Azure 에코 시스템 내에서 함수 사전으로 응답할 수 있습니다 hello 데이터 및 도구 toosolve 문제 네트워크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![시나리오][scenario]

## <a name="prerequisites"></a><span data-ttu-id="262d6-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="262d6-115">Prerequisites</span></span>

* <span data-ttu-id="262d6-116">최신 버전의 hello [Azure PowerShell](/powershell/azure/install-azurerm-ps)합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="262d6-117">Network Watcher의 기존 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="262d6-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="262d6-118">[Network Watcher 인스턴스](network-watcher-create.md)가 아직 없는 경우에는 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="262d6-119">Hello에 기존 가상 컴퓨터 네트워크 감시자 hello와 동일한 지역 [Windows 확장](../virtual-machines/windows/extensions-nwa.md) 또는 [Linux 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="262d6-120">시나리오</span><span class="sxs-lookup"><span data-stu-id="262d6-120">Scenario</span></span>

<span data-ttu-id="262d6-121">이 예제에서는 VM은, 평소 보다 더 많은 TCP 세그먼트 보내고 경고를 발생 시킬 toobe 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="262d6-122">여기서는 TCP 세그먼트가 예로 사용되지만 경고 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="262d6-123">경고가 표시 될 때 원하는 tooreceive 패킷 수준 데이터 toounderstand 이유 통신 증가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="262d6-124">그런 다음 tooreturn hello 가상 컴퓨터 tooregular 통신 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="262d6-125">이 시나리오에서는 Network Watcher의 기존 인스턴스가 있고 유효한 가상 컴퓨터를 포함하는 리소스 그룹이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="262d6-126">다음 목록 hello은 일어나는 hello 워크플로에 대 한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="262d6-127">경고는 VM에서 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="262d6-128">hello 경고는 webhook 통해 Azure 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="262d6-129">사용자가 Azure 함수 hello 경고를 처리 하 고 네트워크 감시자 패킷 캡처 세션을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="262d6-130">hello 패킷 캡처 hello VM에서 실행 되 고 트래픽을 수집 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="262d6-131">hello 패킷 캡처 파일을 업로드 tooa 저장소 계정을 검토 하 고 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="262d6-132">tooautomate이이 프로세스를 생성 하 고 hello 사고가 발생 하는 경우 경고 우리의 VM tootrigger에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="262d6-133">또한 함수 toocall을 네트워크 감시자를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="262d6-134">이 시나리오는 다음 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-134">This scenario does hello following:</span></span>

* <span data-ttu-id="262d6-135">패킷 캡처를 시작하는 Azure 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="262d6-136">가상 컴퓨터에서 경고 규칙을 만들고 hello 경고 규칙 toocall hello Azure 함수를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="262d6-137">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="262d6-137">Create an Azure function</span></span>

<span data-ttu-id="262d6-138">hello 첫 번째 단계 toocreate Azure 함수 tooprocess hello 경고 이며 패킷 캡처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="262d6-139">Hello에 [Azure 포털](https://portal.azure.com)선택, **새로** > **계산** > **함수 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![함수 앱 만들기][1-1]

2. <span data-ttu-id="262d6-141">Hello에 **함수 앱** 블레이드에서 hello 다음 값을 입력 한 다음 선택 **확인** toocreate hello 앱:</span><span class="sxs-lookup"><span data-stu-id="262d6-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="262d6-142">**설정**</span><span class="sxs-lookup"><span data-stu-id="262d6-142">**Setting**</span></span> | <span data-ttu-id="262d6-143">**값**</span><span class="sxs-lookup"><span data-stu-id="262d6-143">**Value**</span></span> | <span data-ttu-id="262d6-144">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="262d6-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="262d6-145">**앱 이름**</span><span class="sxs-lookup"><span data-stu-id="262d6-145">**App name**</span></span>|<span data-ttu-id="262d6-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="262d6-146">PacketCaptureExample</span></span>|<span data-ttu-id="262d6-147">hello 함수 앱의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="262d6-148">**구독**</span><span class="sxs-lookup"><span data-stu-id="262d6-148">**Subscription**</span></span>|<span data-ttu-id="262d6-149">[구독] hello toocreate hello 함수 앱에 대 한 구독.</span><span class="sxs-lookup"><span data-stu-id="262d6-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="262d6-150">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="262d6-150">**Resource Group**</span></span>|<span data-ttu-id="262d6-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="262d6-151">PacketCaptureRG</span></span>|<span data-ttu-id="262d6-152">hello 리소스 그룹 toocontain hello 함수는 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="262d6-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="262d6-153">**호스팅 계획**</span><span class="sxs-lookup"><span data-stu-id="262d6-153">**Hosting Plan**</span></span>|<span data-ttu-id="262d6-154">소비 계획</span><span class="sxs-lookup"><span data-stu-id="262d6-154">Consumption Plan</span></span>| <span data-ttu-id="262d6-155">hello 유형의 함수 앱 사용을 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="262d6-156">옵션은 소비 계획 또는 Azure App Service 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="262d6-157">**위치**:</span><span class="sxs-lookup"><span data-stu-id="262d6-157">**Location**</span></span>|<span data-ttu-id="262d6-158">미국 중부</span><span class="sxs-lookup"><span data-stu-id="262d6-158">Central US</span></span>| <span data-ttu-id="262d6-159">어떤 toocreate hello 함수 앱의 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="262d6-160">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="262d6-160">**Storage Account**</span></span>|<span data-ttu-id="262d6-161">{autogenerated}</span><span class="sxs-lookup"><span data-stu-id="262d6-161">{autogenerated}</span></span>| <span data-ttu-id="262d6-162">범용 저장소에 필요한 Azure 함수 hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="262d6-163">Hello에 **PacketCaptureExample 기능 앱** 블레이드를 **함수** > **사용자 정의 함수**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="262d6-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="262d6-164">선택 **HttpTrigger Powershell**, hello 남은 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="262d6-165">마지막으로, toocreate hello 함수를 선택 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="262d6-166">**설정**</span><span class="sxs-lookup"><span data-stu-id="262d6-166">**Setting**</span></span> | <span data-ttu-id="262d6-167">**값**</span><span class="sxs-lookup"><span data-stu-id="262d6-167">**Value**</span></span> | <span data-ttu-id="262d6-168">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="262d6-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="262d6-169">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="262d6-169">**Scenario**</span></span>|<span data-ttu-id="262d6-170">실험적</span><span class="sxs-lookup"><span data-stu-id="262d6-170">Experimental</span></span>|<span data-ttu-id="262d6-171">시나리오 유형</span><span class="sxs-lookup"><span data-stu-id="262d6-171">Type of scenario</span></span>|
    |<span data-ttu-id="262d6-172">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="262d6-172">**Name your function**</span></span>|<span data-ttu-id="262d6-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="262d6-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="262d6-174">Hello 함수의 이름</span><span class="sxs-lookup"><span data-stu-id="262d6-174">Name of hello function</span></span>|
    |<span data-ttu-id="262d6-175">**권한 부여 수준**</span><span class="sxs-lookup"><span data-stu-id="262d6-175">**Authorization level**</span></span>|<span data-ttu-id="262d6-176">함수</span><span class="sxs-lookup"><span data-stu-id="262d6-176">Function</span></span>|<span data-ttu-id="262d6-177">Hello 함수에 대 한 권한 수준</span><span class="sxs-lookup"><span data-stu-id="262d6-177">Authorization level for hello function</span></span>|

![함수 예제][functions1]

> [!NOTE]
> <span data-ttu-id="262d6-179">hello PowerShell 템플릿 실험적이 며 완벽 하 게 지원이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="262d6-180">사용자 지정 단계를 수행 하는 hello 설명 및이 예제에 대 한 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="262d6-181">모듈 추가</span><span class="sxs-lookup"><span data-stu-id="262d6-181">Add modules</span></span>

<span data-ttu-id="262d6-182">네트워크 감시자 PowerShell cmdlet toouse hello 최신 PowerShell 모듈 toohello 함수 앱을 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="262d6-183">설치 된 hello 최신 Azure PowerShell 모듈을 통해 로컬 컴퓨터, hello 다음 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="262d6-184">이 예제에서는 Azure PowerShell 모듈의 로컬 경로 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="262d6-185">이러한 폴더는 이후 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-185">These folders are used in a later step.</span></span> <span data-ttu-id="262d6-186">이 시나리오에 사용 되는 hello 모듈은:</span><span class="sxs-lookup"><span data-stu-id="262d6-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="262d6-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="262d6-187">AzureRM.Network</span></span>

    * <span data-ttu-id="262d6-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="262d6-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="262d6-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="262d6-189">AzureRM.Resources</span></span>

    ![PowerShell 폴더][functions5]

1. <span data-ttu-id="262d6-191">선택 **앱 설정을 함수** > **tooApp 서비스 편집기 이동**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![함수 앱 설정][functions2]

1. <span data-ttu-id="262d6-193">마우스 오른쪽 단추로 클릭 hello **AlertPacketCapturePowershell** 폴더를 다음 라는 폴더를 만듭니다 **azuremodules**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="262d6-194">필요한 각 모듈에 대한 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-194">Create a subfolder for each module that you need.</span></span>

    ![폴더 및 하위 폴더][functions3]

    * <span data-ttu-id="262d6-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="262d6-196">AzureRM.Network</span></span>

    * <span data-ttu-id="262d6-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="262d6-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="262d6-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="262d6-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="262d6-199">마우스 오른쪽 단추로 클릭 hello **AzureRM.Network** 하위 폴더를 선택한 후 **파일 업로드**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="262d6-200">Azure tooyour 이동 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="262d6-201">Hello 로컬에서 **AzureRM.Network** 폴더 hello 폴더에 모든 hello 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="262d6-202">그런 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="262d6-203">**AzureRM.Profile** 및 **AzureRM.Resources**에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![파일 업로드][functions6]

1. <span data-ttu-id="262d6-205">완료 한 후, 각 폴더에는 로컬 컴퓨터에서 PowerShell 모듈 파일 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![PowerShell 파일][functions7]

### <a name="authentication"></a><span data-ttu-id="262d6-207">인증</span><span class="sxs-lookup"><span data-stu-id="262d6-207">Authentication</span></span>

<span data-ttu-id="262d6-208">인증 해야 toouse hello PowerShell cmdlet을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="262d6-209">Hello 함수 응용 프로그램에서 인증을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="262d6-210">tooconfigure 인증 환경 변수를 구성 하 고 암호화 된 키 파일 toohello 함수 앱을 업로드 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="262d6-211">이 시나리오는 방법의 한 예를 제공 합니다. Azure 함수로 tooimplement 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="262d6-212">있는 경우 다른 방법으로 toodo이</span><span class="sxs-lookup"><span data-stu-id="262d6-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="262d6-213">암호화된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="262d6-213">Encrypted credentials</span></span>

<span data-ttu-id="262d6-214">PowerShell 스크립트 뒤 hello 라는 키 파일을 만들어 **PassEncryptKey.key**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="262d6-215">또한 제공 되는 hello 암호의 암호화 된 버전을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="262d6-216">이 암호는 hello 인증에 사용 되는 hello Azure Active Directory 응용 프로그램에 대해 정의 된 동일한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="262d6-217">Hello 함수 응용 프로그램의 응용 프로그램 서비스 편집기 hello 라는 폴더를 만들어 **키** 아래 **AlertPacketCapturePowerShell**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="262d6-218">그런 다음 hello 업로드 **PassEncryptKey.key** hello 이전 PowerShell 샘플에서 만든 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![함수 키][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="262d6-220">환경 변수의 값 검색</span><span class="sxs-lookup"><span data-stu-id="262d6-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="262d6-221">hello 최종 요구 사항은 tooset hello 환경 변수를 인증에 대 한 필요한 tooaccess hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="262d6-222">hello 다음은 만들어진 hello 환경 변수.</span><span class="sxs-lookup"><span data-stu-id="262d6-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="262d6-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="262d6-223">AzureClientID</span></span>

* <span data-ttu-id="262d6-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="262d6-224">AzureTenant</span></span>

* <span data-ttu-id="262d6-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="262d6-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="262d6-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="262d6-226">AzureClientID</span></span>

<span data-ttu-id="262d6-227">hello 클라이언트 ID는 hello Azure Active Directory에서 응용 프로그램의 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="262d6-228">응용 프로그램 toouse 없는 경우 다음 예제에서는 toocreate hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="262d6-229">hello 있어야 hello 응용 프로그램을 만들 때 사용 하는 hello 암호 hello 키 파일을 저장할 때 앞에서 만든 동일한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="262d6-230">Hello Azure 포털에서에서 선택 **구독**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="262d6-231">Hello 구독 toouse를 선택한 다음 선택 **액세스 제어 (IAM)**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![함수 IAM][functions9]

1. <span data-ttu-id="262d6-233">Hello 계정 toouse를 선택한 다음 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="262d6-234">복사 hello 응용 프로그램 id입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-234">Copy hello Application ID.</span></span>

    ![함수 응용 프로그램 ID][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="262d6-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="262d6-236">AzureTenant</span></span>

<span data-ttu-id="262d6-237">Hello 다음 PowerShell 예제를 실행 하 여 hello 테 넌 트 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="262d6-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="262d6-238">AzureCredPassword</span></span>

<span data-ttu-id="262d6-239">hello hello AzureCredPassword 환경 변수 값은 다음 PowerShell 샘플 hello 실행에서 얻을 수 있는 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="262d6-240">이 예제는 hello 앞에 표시 된 것 동일한 hello는 **자격 증명을 암호화** 섹션.</span><span class="sxs-lookup"><span data-stu-id="262d6-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="262d6-241">필요한 값 hello hello의 hello 출력이 `$Encryptedpassword` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="262d6-242">이것이 hello PowerShell 스크립트를 사용 하 여 암호화 hello 서비스 사용자 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="262d6-243">Hello 환경 변수를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-243">Store hello environment variables</span></span>

1. <span data-ttu-id="262d6-244">Toohello 함수 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-244">Go toohello function app.</span></span> <span data-ttu-id="262d6-245">그런 후 **함수 앱 설정** > **앱 설정 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![앱 설정 구성][functions11]

1. <span data-ttu-id="262d6-247">Hello 환경 변수 및 해당 값 toohello 응용 프로그램 설정을 추가 하 고 다음 선택 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![앱 설정][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="262d6-249">PowerShell toohello 함수 추가</span><span class="sxs-lookup"><span data-stu-id="262d6-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="262d6-250">Hello Azure 함수 내에서 네트워크 감시자를 호출 하는 시간 toomake 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="262d6-251">이 함수의 구현은 hello는 hello 요구 사항에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="262d6-252">그러나 hello 코드의 hello 일반적인 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="262d6-253">입력 매개 변수를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-253">Process input parameters.</span></span>
2. <span data-ttu-id="262d6-254">쿼리 기존 패킷을 tooverify 제한 캡처하고 이름 충돌을 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="262d6-255">적절한 매개 변수를 사용하여 패킷 캡처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="262d6-256">완료될 때까지 패킷 캡처를 주기적으로 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="262d6-257">Hello 패킷 캡처 세션이 완료 될 hello 사용자에 게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="262d6-258">hello 다음 예제는 hello 함수에서 사용할 수 있는 PowerShell 코드.</span><span class="sxs-lookup"><span data-stu-id="262d6-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="262d6-259">에 대 한 대체 toobe 해야 하는 값이 없는 **subscriptionId**, **resourceGroupName**, 및 **storageAccountName**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="262d6-260">Hello 함수 URL을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="262d6-261">함수를 만든 후 hello 함수와 관련 된 경고 toocall hello URL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="262d6-262">tooget이이 값을 함수 앱에서 hello 함수 URL 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Hello 함수 URL 찾기][functions13]

2. <span data-ttu-id="262d6-264">함수에서 사용 하는 앱에 대 한 hello 함수 URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-264">Copy hello function URL for your function app.</span></span>

    ![Hello 함수 URL 복사][2]

<span data-ttu-id="262d6-266">Hello webhook POST 요청의 hello 페이로드에 사용자 지정 속성을 필요한 경우 너무 참조[Azure 메트릭 경고에는 webhook 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="262d6-267">VM에서 경고 구성</span><span class="sxs-lookup"><span data-stu-id="262d6-267">Configure an alert on a VM</span></span>

<span data-ttu-id="262d6-268">특정 메트릭을 할당 되는 임계값을 초과할 때 경고가 구성 된 toonotify 개인 될 수 있습니다 tooit 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="262d6-269">이 예제에서는 hello 경고는 hello에 전송 된 TCP 세그먼트 있지만 다른 많은 메트릭에 대 한 hello 경고를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="262d6-270">이 예제에서는 경고에는 구성 된 toocall webhook toocall hello 함수는.</span><span class="sxs-lookup"><span data-stu-id="262d6-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="262d6-271">Hello 경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="262d6-271">Create hello alert rule</span></span>

<span data-ttu-id="262d6-272">Tooan 기존 가상 컴퓨터를 이동 하 고 경고 규칙을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="262d6-273">경고 구성에 대한 보다 자세한 설명서는 [Azure 서비스에 대한 Azure Monitor에서 경고 만들기 - Azure Portal](../monitoring-and-diagnostics/insights-alerts-portal.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="262d6-274">다음 hello에 대 한 값에는 hello 입력 **경고 규칙** 블레이드에서 다음을 선택 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="262d6-275">**설정**</span><span class="sxs-lookup"><span data-stu-id="262d6-275">**Setting**</span></span> | <span data-ttu-id="262d6-276">**값**</span><span class="sxs-lookup"><span data-stu-id="262d6-276">**Value**</span></span> | <span data-ttu-id="262d6-277">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="262d6-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="262d6-278">**Name**</span><span class="sxs-lookup"><span data-stu-id="262d6-278">**Name**</span></span>|<span data-ttu-id="262d6-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="262d6-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="262d6-280">Hello 경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="262d6-281">**설명**</span><span class="sxs-lookup"><span data-stu-id="262d6-281">**Description**</span></span>|<span data-ttu-id="262d6-282">전송된 TCP 세그먼트가 임계값을 초과함</span><span class="sxs-lookup"><span data-stu-id="262d6-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="262d6-283">hello 경고 규칙에 대 한 hello 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="262d6-284">**메트릭**</span><span class="sxs-lookup"><span data-stu-id="262d6-284">**Metric**</span></span>|<span data-ttu-id="262d6-285">전송된 TCP 세그먼트</span><span class="sxs-lookup"><span data-stu-id="262d6-285">TCP segments sent</span></span>| <span data-ttu-id="262d6-286">hello 메트릭 toouse tootrigger hello 경고입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="262d6-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="262d6-287">**Condition**</span></span>|<span data-ttu-id="262d6-288">다음보다 큼</span><span class="sxs-lookup"><span data-stu-id="262d6-288">Greater than</span></span>| <span data-ttu-id="262d6-289">hello 조건 toouse hello 메트릭을 평가 하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="262d6-290">**임계값**</span><span class="sxs-lookup"><span data-stu-id="262d6-290">**Threshold**</span></span>|<span data-ttu-id="262d6-291">100</span><span class="sxs-lookup"><span data-stu-id="262d6-291">100</span></span>| <span data-ttu-id="262d6-292">hello 경고를 트리거하는 hello 메트릭의 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="262d6-293">이 값은 사용자 환경에 대 한 유효한 값 tooa 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="262d6-294">**기간**</span><span class="sxs-lookup"><span data-stu-id="262d6-294">**Period**</span></span>|<span data-ttu-id="262d6-295">지난 5 분 동안 hello를 통해</span><span class="sxs-lookup"><span data-stu-id="262d6-295">Over hello last five minutes</span></span>| <span data-ttu-id="262d6-296">Hello 임계값 메트릭 hello에 대 한 어떤 toolook hello 기간을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="262d6-297">**웹후크**</span><span class="sxs-lookup"><span data-stu-id="262d6-297">**Webhook**</span></span>|<span data-ttu-id="262d6-298">[함수 앱에서 웹후크 URL]</span><span class="sxs-lookup"><span data-stu-id="262d6-298">[webhook URL from function app]</span></span>| <span data-ttu-id="262d6-299">hello 이전 단계에서 만든 hello 함수 응용 프로그램에서 hello webhook URL입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="262d6-300">hello TCP 세그먼트 메트릭은 기본적으로 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="262d6-301">에 대 한 자세한 방법에 대 한 방문 하 여 추가 메트릭을 tooenable [모니터링을 활성화 및 진단](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="262d6-302">Hello 결과 검토</span><span class="sxs-lookup"><span data-stu-id="262d6-302">Review hello results</span></span>

<span data-ttu-id="262d6-303">Hello 조건을 hello 경고 트리거에 대 한 패킷 캡처가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="262d6-304">TooNetwork 감시자에서 이동한 다음 선택 **패킷 캡처**합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="262d6-305">이 페이지에서는 hello 패킷 캡처 파일 링크 toodownload hello 패킷 캡처를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![패킷 캡처 보기][functions14]

<span data-ttu-id="262d6-307">Hello 캡처 파일을 로컬에 저장 하는 경우 toohello 가상 컴퓨터에 로그인 하 여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="262d6-308">Azure Storage 계정에서 파일을 다운로드하는 방법에 대한 지침은 [.NET을 사용하여 Azure Blob Storage 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="262d6-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="262d6-309">사용할 수 있는 다른 도구는 [저장소 탐색기](http://storageexplorer.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="262d6-310">캡처를 다운로드했으면 **.cap** 파일을 읽을 수 있는 도구를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="262d6-311">다음은 이러한 도구의 tootwo 링크:</span><span class="sxs-lookup"><span data-stu-id="262d6-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="262d6-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="262d6-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="262d6-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="262d6-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="262d6-314">다음 단계</span><span class="sxs-lookup"><span data-stu-id="262d6-314">Next steps</span></span>

<span data-ttu-id="262d6-315">어떻게 tooview 패킷 캡처합니다 방문에 알아봅니다 [wireshark 패킷 캡처 분석](network-watcher-deep-packet-inspection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="262d6-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
