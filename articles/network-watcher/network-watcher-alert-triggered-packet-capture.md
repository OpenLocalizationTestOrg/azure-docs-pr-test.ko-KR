---
title: "패킷 캡처를 사용하여 경고 및 Azure Functions로 자동 관리 네트워크 모니터링 수행 | Microsoft Docs"
description: "이 문서에서는 Azure Network Watcher에서 경고로 트리거된 패킷 캡처를 만드는 방법을 설명합니다."
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
ms.openlocfilehash: b813172fc1fc1cc683f463f05370c95bfec10f8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="43643-103">경고 및 Azure Functions를 통한 사전 네트워크 모니터링을 위해 패킷 캡처 사용</span><span class="sxs-lookup"><span data-stu-id="43643-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="43643-104">Network Watcher 패킷 캡처는 가상 컴퓨터 간에 트래픽을 추적하는 캡처 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-104">Network Watcher packet capture creates capture sessions to track traffic in and out of virtual machines.</span></span> <span data-ttu-id="43643-105">캡처 파일은 모니터링할 트래픽만 추적하도록 정의된 필터를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-105">The capture file can have a filter that is defined to track only the traffic that you want to monitor.</span></span> <span data-ttu-id="43643-106">이 데이터는 저장소 BLOB이나 게스트 컴퓨터에 로컬로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-106">This data is then stored in a storage blob or locally on the guest machine.</span></span>

<span data-ttu-id="43643-107">이 기능은 Azure Functions와 같은 다른 자동화 시나리오에서 원격으로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="43643-108">패킷 캡처는 정의된 네트워크 예외에 따라 사전 캡처를 실행하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-108">Packet capture gives you the capability to run proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="43643-109">또한 네트워크 침입에 대한 정보를 가져오는 네트워크 통계를 수집하는 것을 포함하여 클라이언트 서버 간 통신을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="43643-110">Azure에 배포된 리소스는 연중 무휴(24/7) 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="43643-111">사용자 또는 직원은 연중 무휴 실행되는 모든 리소스의 상태를 적극적으로 모니터링할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-111">You and your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="43643-112">예를 들어 오전 2시에 문제가 발생하면 어떻게 할까요?</span><span class="sxs-lookup"><span data-stu-id="43643-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="43643-113">Azure 에코시스템 내에서 Network Watcher, Alerting 및 Functions를 사용하면 데이터와 도구에 미리 응답함으로써 네트워크 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-113">By using Network Watcher, alerting, and functions from within the Azure ecosystem, you can proactively respond with the data and tools to solve problems in your network.</span></span>

![시나리오][scenario]

## <a name="prerequisites"></a><span data-ttu-id="43643-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="43643-115">Prerequisites</span></span>

* <span data-ttu-id="43643-116">최신 버전의 [Azure PowerShell](/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="43643-116">The latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="43643-117">Network Watcher의 기존 인스턴스.</span><span class="sxs-lookup"><span data-stu-id="43643-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="43643-118">[Network Watcher 인스턴스](network-watcher-create.md)가 아직 없는 경우에는 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="43643-119">[Windows 확장](../virtual-machines/windows/extensions-nwa.md) 또는 [Linux 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)이 있고 Network Watcher와 동일한 지역에 기존 가상 컴퓨터가 있음</span><span class="sxs-lookup"><span data-stu-id="43643-119">An existing virtual machine in the same region as Network Watcher with the [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="43643-120">시나리오</span><span class="sxs-lookup"><span data-stu-id="43643-120">Scenario</span></span>

<span data-ttu-id="43643-121">이 예제에서는 VM이 평소보다 더 많은 TCP 세그먼트를 보내고 있으며 이를 경고하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-121">In this example, your VM is sending more TCP segments than usual, and you want to be alerted.</span></span> <span data-ttu-id="43643-122">여기서는 TCP 세그먼트가 예로 사용되지만 경고 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="43643-123">경고를 보낸 경우, 통신이 증가한 이유를 알기 위해 패킷 수준 데이터를 수신하려고 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-123">When you are alerted, you want to receive packet-level data to understand why communication has increased.</span></span> <span data-ttu-id="43643-124">그런 후에는 가상 컴퓨터를 일반 통신으로 반환하는 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-124">Then you can take steps to return the virtual machine to regular communication.</span></span>

<span data-ttu-id="43643-125">이 시나리오에서는 Network Watcher의 기존 인스턴스가 있고 유효한 가상 컴퓨터를 포함하는 리소스 그룹이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="43643-126">다음 목록은 수행되는 워크플로 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-126">The following list is an overview of the workflow that takes place:</span></span>

1. <span data-ttu-id="43643-127">경고는 VM에서 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="43643-128">경고는 웹후크를 통해 Azure Function을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-128">The alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="43643-129">Azure Function은 경고를 처리하고 Network Watcher 패킷 캡처 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-129">Your Azure function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="43643-130">패킷 캡처는 VM에서 실행되고 트래픽을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-130">The packet capture runs on the VM and collects traffic.</span></span>
1. <span data-ttu-id="43643-131">이 패킷 캡처 파일은 검토 및 진단을 위해 저장소 계정에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-131">The packet capture file is uploaded to a storage account for review and diagnosis.</span></span>

<span data-ttu-id="43643-132">이 프로세스를 자동화하려면, 인시던트가 발생할 때 VM에서 트리거할 경고를 만들고 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-132">To automate this process, we create and connect an alert on our VM to trigger when the incident occurs.</span></span> <span data-ttu-id="43643-133">또한 Network Watcher를 호출하기 위한 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-133">We also create a function to call into Network Watcher.</span></span>

<span data-ttu-id="43643-134">이 시나리오는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-134">This scenario does the following:</span></span>

* <span data-ttu-id="43643-135">패킷 캡처를 시작하는 Azure 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="43643-136">가상 컴퓨터에 대한 경고 규칙을 만들고 Azure Function을 호출할 경고 규칙을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-136">Creates an alert rule on a virtual machine and configures the alert rule to call the Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="43643-137">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="43643-137">Create an Azure function</span></span>

<span data-ttu-id="43643-138">첫 번째 단계는 경고를 처리할 Azure Function을 만들고 패킷 캡처를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-138">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

1. <span data-ttu-id="43643-139">[Azure Portal](https://portal.azure.com)에서 **새로 만들기** > **계산** > **함수 앱**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-139">In the [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![함수 앱 만들기][1-1]

2. <span data-ttu-id="43643-141">**함수 앱** 블레이드에서 다음 값을 입력하고 **확인**을 선택하여 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-141">On the **Function App** blade, enter the following values, and then select **OK** to create the app:</span></span>

    |<span data-ttu-id="43643-142">**설정**</span><span class="sxs-lookup"><span data-stu-id="43643-142">**Setting**</span></span> | <span data-ttu-id="43643-143">**값**</span><span class="sxs-lookup"><span data-stu-id="43643-143">**Value**</span></span> | <span data-ttu-id="43643-144">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="43643-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="43643-145">**앱 이름**</span><span class="sxs-lookup"><span data-stu-id="43643-145">**App name**</span></span>|<span data-ttu-id="43643-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="43643-146">PacketCaptureExample</span></span>|<span data-ttu-id="43643-147">함수 앱의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-147">The name of the function app.</span></span>|
    |<span data-ttu-id="43643-148">**구독**</span><span class="sxs-lookup"><span data-stu-id="43643-148">**Subscription**</span></span>|<span data-ttu-id="43643-149">[구독]함수 앱을 만들 구독입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-149">[Your subscription]The subscription for which to create the function app.</span></span>||
    |<span data-ttu-id="43643-150">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="43643-150">**Resource Group**</span></span>|<span data-ttu-id="43643-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="43643-151">PacketCaptureRG</span></span>|<span data-ttu-id="43643-152">함수 앱을 포함할 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-152">The resource group to contain the function app.</span></span>|
    |<span data-ttu-id="43643-153">**호스팅 계획**</span><span class="sxs-lookup"><span data-stu-id="43643-153">**Hosting Plan**</span></span>|<span data-ttu-id="43643-154">소비 계획</span><span class="sxs-lookup"><span data-stu-id="43643-154">Consumption Plan</span></span>| <span data-ttu-id="43643-155">함수 앱이 사용하는 계획 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-155">The type of plan your function app uses.</span></span> <span data-ttu-id="43643-156">옵션은 소비 계획 또는 Azure App Service 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="43643-157">**위치**:</span><span class="sxs-lookup"><span data-stu-id="43643-157">**Location**</span></span>|<span data-ttu-id="43643-158">미국 중부</span><span class="sxs-lookup"><span data-stu-id="43643-158">Central US</span></span>| <span data-ttu-id="43643-159">함수 앱을 만들 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-159">The region in which to create the function app.</span></span>|
    |<span data-ttu-id="43643-160">**저장소 계정**</span><span class="sxs-lookup"><span data-stu-id="43643-160">**Storage Account**</span></span>|<span data-ttu-id="43643-161">{autogenerated}</span><span class="sxs-lookup"><span data-stu-id="43643-161">{autogenerated}</span></span>| <span data-ttu-id="43643-162">범용 저장소용으로 Azure Functions에 필요한 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-162">The storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="43643-163">**PacketCaptureExample** 함수 앱 블레이드에서 **함수** > **사용자 지정 함수** >**+**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-163">On the **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="43643-164">**HttpTrigger-Powershell**을 선택하고 나머지 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-164">Select **HttpTrigger-Powershell**, and then enter the remaining information.</span></span> <span data-ttu-id="43643-165">마지막으로 함수를 만들려면 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-165">Finally, to create the function, select **Create**.</span></span>

    |<span data-ttu-id="43643-166">**설정**</span><span class="sxs-lookup"><span data-stu-id="43643-166">**Setting**</span></span> | <span data-ttu-id="43643-167">**값**</span><span class="sxs-lookup"><span data-stu-id="43643-167">**Value**</span></span> | <span data-ttu-id="43643-168">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="43643-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="43643-169">**시나리오**</span><span class="sxs-lookup"><span data-stu-id="43643-169">**Scenario**</span></span>|<span data-ttu-id="43643-170">실험적</span><span class="sxs-lookup"><span data-stu-id="43643-170">Experimental</span></span>|<span data-ttu-id="43643-171">시나리오 유형</span><span class="sxs-lookup"><span data-stu-id="43643-171">Type of scenario</span></span>|
    |<span data-ttu-id="43643-172">**함수 이름 지정**</span><span class="sxs-lookup"><span data-stu-id="43643-172">**Name your function**</span></span>|<span data-ttu-id="43643-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="43643-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="43643-174">함수의 이름</span><span class="sxs-lookup"><span data-stu-id="43643-174">Name of the function</span></span>|
    |<span data-ttu-id="43643-175">**권한 부여 수준**</span><span class="sxs-lookup"><span data-stu-id="43643-175">**Authorization level**</span></span>|<span data-ttu-id="43643-176">함수</span><span class="sxs-lookup"><span data-stu-id="43643-176">Function</span></span>|<span data-ttu-id="43643-177">함수에 대한 권한 부여 수준</span><span class="sxs-lookup"><span data-stu-id="43643-177">Authorization level for the function</span></span>|

![함수 예제][functions1]

> [!NOTE]
> <span data-ttu-id="43643-179">PowerShell 템플릿은 실험적이며 완전한 지원을 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-179">The PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="43643-180">이 예제에는 사용자 지정이 필요하며 다음 단계에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-180">Customizations are required for this example and are explained in the following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="43643-181">모듈 추가</span><span class="sxs-lookup"><span data-stu-id="43643-181">Add modules</span></span>

<span data-ttu-id="43643-182">Network Watcher PowerShell cmdlet을 사용하려면 최신 PowerShell 모듈을 함수 앱에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-182">To use Network Watcher PowerShell cmdlets, upload the latest PowerShell module to the function app.</span></span>

1. <span data-ttu-id="43643-183">최신 Azure PowerShell 모듈이 설치된 로컬 컴퓨터에서 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-183">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="43643-184">이 예제에서는 Azure PowerShell 모듈의 로컬 경로가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-184">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="43643-185">이러한 폴더는 이후 단계에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-185">These folders are used in a later step.</span></span> <span data-ttu-id="43643-186">이 시나리오에서 사용되는 모듈은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-186">The modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="43643-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="43643-187">AzureRM.Network</span></span>

    * <span data-ttu-id="43643-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="43643-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="43643-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="43643-189">AzureRM.Resources</span></span>

    ![PowerShell 폴더][functions5]

1. <span data-ttu-id="43643-191">**함수 앱 설정** > **App Service 편집기로 이동**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-191">Select **Function app settings** > **Go to App Service Editor**.</span></span>

    ![함수 앱 설정][functions2]

1. <span data-ttu-id="43643-193">**AlertPacketCapturePowershell** 폴더를 마우스 오른쪽 단추로 클릭하고 **azuremodules**라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-193">Right-click the **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="43643-194">필요한 각 모듈에 대한 하위 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-194">Create a subfolder for each module that you need.</span></span>

    ![폴더 및 하위 폴더][functions3]

    * <span data-ttu-id="43643-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="43643-196">AzureRM.Network</span></span>

    * <span data-ttu-id="43643-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="43643-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="43643-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="43643-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="43643-199">**AzureRM.Network** 하위 폴더를 마우스 오른쪽 단추로 클릭하고 **파일 업로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-199">Right-click the **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="43643-200">Azure 모듈로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-200">Go to your Azure modules.</span></span> <span data-ttu-id="43643-201">로컬 **AzureRM.Network** 폴더에서 폴더의 모든 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-201">In the local **AzureRM.Network** folder, select all the files in the folder.</span></span> <span data-ttu-id="43643-202">그런 다음 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="43643-203">**AzureRM.Profile** 및 **AzureRM.Resources**에 대해 이러한 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![파일 업로드][functions6]

1. <span data-ttu-id="43643-205">완료되면 로컬 컴퓨터의 각 폴더에 PowerShell 모듈 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-205">After you've finished, each folder should have the PowerShell module files from your local machine.</span></span>

    ![PowerShell 파일][functions7]

### <a name="authentication"></a><span data-ttu-id="43643-207">인증</span><span class="sxs-lookup"><span data-stu-id="43643-207">Authentication</span></span>

<span data-ttu-id="43643-208">PowerShell cmdlet을 사용하려면 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-208">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="43643-209">함수 앱에서 인증을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-209">You configure authentication in the function app.</span></span> <span data-ttu-id="43643-210">인증을 구성하려면 환경 변수를 구성하고 암호화된 키 파일을 함수 앱에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-210">To configure authentication, you must configure environment variables and upload an encrypted key file to the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="43643-211">이 시나리오에서는 Azure Functions를 사용하여 인증을 구현하는 방법에 대한 하나의 예제를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-211">This scenario provides just one example of how to implement authentication with Azure Functions.</span></span> <span data-ttu-id="43643-212">이 작업은 다른 방법으로도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-212">There are other ways to do this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="43643-213">암호화된 자격 증명</span><span class="sxs-lookup"><span data-stu-id="43643-213">Encrypted credentials</span></span>

<span data-ttu-id="43643-214">다음 PowerShell 스크립트는 **PassEncryptKey.key**라는 키 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-214">The following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="43643-215">또한 제공된 암호의 암호화된 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-215">It also provides an encrypted version of the password that's supplied.</span></span> <span data-ttu-id="43643-216">이 암호는 인증에 사용되는 Azure Active Directory 응용 프로그램에 대해 정의된 것과 동일한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-216">This password is the same password that is defined for the Azure Active Directory application that's used for authentication.</span></span>

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

<span data-ttu-id="43643-217">함수 앱의 App Service 편집기에서 **AlertPacketCapturePowerShell** 아래에 **keys**라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-217">In the App Service Editor of the function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="43643-218">그런 다음 이전 PowerShell 샘플에서 만든 **PassEncryptKey.key** 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-218">Then upload the **PassEncryptKey.key** file that you created in the previous PowerShell sample.</span></span>

![함수 키][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="43643-220">환경 변수의 값 검색</span><span class="sxs-lookup"><span data-stu-id="43643-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="43643-221">최종 요구 사항은 인증에 대한 값에 액세스하는 데 필요한 환경 변수를 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-221">The final requirement is to set up the environment variables that are necessary to access the values for authentication.</span></span> <span data-ttu-id="43643-222">다음은 만들어지는 환경 변수의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-222">The following list shows the environment variables that are created:</span></span>

* <span data-ttu-id="43643-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="43643-223">AzureClientID</span></span>

* <span data-ttu-id="43643-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="43643-224">AzureTenant</span></span>

* <span data-ttu-id="43643-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="43643-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="43643-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="43643-226">AzureClientID</span></span>

<span data-ttu-id="43643-227">클라이언트 ID는 Azure Active Directory에 있는 응용 프로그램의 응용 프로그램 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-227">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="43643-228">사용할 응용 프로그램이 아직 없으면 다음 예제를 실행하여 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-228">If you don't already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="43643-229">응용 프로그램을 만들 때 사용되는 암호는 이전에 키 파일을 저장할 때 만든 암호와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-229">The password that you use when creating the application should be the same password that you created earlier when saving the key file.</span></span>

1. <span data-ttu-id="43643-230">Azure Portal에서 **구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-230">In the Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="43643-231">사용할 구독을 선택하고 **액세스 제어(IAM)**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-231">Select the subscription to use, and then select **Access control (IAM)**.</span></span>

    ![함수 IAM][functions9]

1. <span data-ttu-id="43643-233">사용할 계정을 선택하고 **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-233">Choose the account to use, and then select **Properties**.</span></span> <span data-ttu-id="43643-234">응용 프로그램 ID를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-234">Copy the Application ID.</span></span>

    ![함수 응용 프로그램 ID][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="43643-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="43643-236">AzureTenant</span></span>

<span data-ttu-id="43643-237">다음 PowerShell 샘플을 실행하여 테넌트 ID를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-237">Obtain the tenant ID  by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="43643-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="43643-238">AzureCredPassword</span></span>

<span data-ttu-id="43643-239">AzureCredPassword 환경 변수의 값은 다음 PowerShell 샘플을 실행하여 얻는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-239">The value of the AzureCredPassword environment variable is the value that you get from running the following PowerShell sample.</span></span> <span data-ttu-id="43643-240">이 예제는 이전의 **암호화된 자격 증명** 섹션에 표시된 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-240">This example is the same one that's shown in the preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="43643-241">필요한 값은 `$Encryptedpassword` 변수의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-241">The value that's needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="43643-242">이 암호는 PowerShell 스크립트를 사용하여 암호화한 서비스 주체 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-242">This is the service principal password that you encrypted by using the PowerShell script.</span></span>

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

### <a name="store-the-environment-variables"></a><span data-ttu-id="43643-243">환경 변수 저장</span><span class="sxs-lookup"><span data-stu-id="43643-243">Store the environment variables</span></span>

1. <span data-ttu-id="43643-244">함수 앱으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="43643-244">Go to the function app.</span></span> <span data-ttu-id="43643-245">그런 후 **함수 앱 설정** > **앱 설정 구성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![앱 설정 구성][functions11]

1. <span data-ttu-id="43643-247">환경 변수와 해당 값을 앱 설정에 추가하고 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-247">Add the environment variables and their values to the app settings, and then select **Save**.</span></span>

    ![앱 설정][functions12]

### <a name="add-powershell-to-the-function"></a><span data-ttu-id="43643-249">함수에 PowerShell 추가</span><span class="sxs-lookup"><span data-stu-id="43643-249">Add PowerShell to the function</span></span>

<span data-ttu-id="43643-250">이제 Azure Function 내에서 Network Watcher를 호출할 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-250">It's now time to make calls into Network Watcher from within the Azure function.</span></span> <span data-ttu-id="43643-251">요구 사항에 따라 이 함수의 구현이 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-251">Depending on the requirements, the implementation of this function can vary.</span></span> <span data-ttu-id="43643-252">하지만 코드의 일반적인 흐름은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-252">However, the general flow of the code is as follows:</span></span>

1. <span data-ttu-id="43643-253">입력 매개 변수를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-253">Process input parameters.</span></span>
2. <span data-ttu-id="43643-254">기존 패킷 캡처를 쿼리하여 한도를 확인하고 이름 충돌을 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-254">Query existing packet captures to verify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="43643-255">적절한 매개 변수를 사용하여 패킷 캡처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="43643-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="43643-256">완료될 때까지 패킷 캡처를 주기적으로 폴링합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="43643-257">사용자에게 패킷 캡처 세션이 완료되었음을 알립니다.</span><span class="sxs-lookup"><span data-stu-id="43643-257">Notify the user that the packet capture session is complete.</span></span>

<span data-ttu-id="43643-258">다음 예제는 함수에서 사용할 수 있는 PowerShell 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-258">The following example is PowerShell code that can be used in the function.</span></span> <span data-ttu-id="43643-259">**subscriptionId**, **resourceGroupName** 및 **storageAccountName**에 대해 바꿔야 하는 값이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-259">There are values that need to be replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required to make calls to Network Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID to save captures in
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


            #Get the VM that fired the alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get the Network Watcher in the VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by the function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on the VM that fired the alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-the-function-url"></a><span data-ttu-id="43643-260">함수 URL 검색</span><span class="sxs-lookup"><span data-stu-id="43643-260">Retrieve the function URL</span></span> 
1. <span data-ttu-id="43643-261">함수를 만들었으면 함수와 연결된 URL을 호출하는 경고를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-261">After you've created your function, configure your alert to call the URL that's associated with the function.</span></span> <span data-ttu-id="43643-262">이 값을 가져오려면 함수 앱에서 함수 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-262">To get this value, copy the function URL from your function app.</span></span>

    ![함수 URL 찾기][functions13]

2. <span data-ttu-id="43643-264">함수 앱의 함수 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-264">Copy the function URL for your function app.</span></span>

    ![함수 URL 복사][2]

<span data-ttu-id="43643-266">웹후크 POST 요청의 페이로드에 사용자 지정 속성이 필요한 경우 [Azure 메트릭 경고에 대한 웹후크 구성](../monitoring-and-diagnostics/insights-webhooks-alerts.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43643-266">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="43643-267">VM에서 경고 구성</span><span class="sxs-lookup"><span data-stu-id="43643-267">Configure an alert on a VM</span></span>

<span data-ttu-id="43643-268">특정 메트릭이 여기에 할당된 임계값을 초과할 경우 개인에게 알리도록 경고를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-268">Alerts can be configured to notify individuals when a specific metric crosses a threshold that's assigned to it.</span></span> <span data-ttu-id="43643-269">이 예에서 경고는 전송된 TCP 세그먼트에 대해 이루어지지만 많은 다른 메트릭에 대해 경고를 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-269">In this example, the alert is on the TCP segments that are sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="43643-270">이 예에서는 함수를 호출하는 웹후크를 호출하도록 경고를 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-270">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="43643-271">경고 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="43643-271">Create the alert rule</span></span>

<span data-ttu-id="43643-272">기존 가상 컴퓨터로 이동하고 경고 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-272">Go to an existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="43643-273">경고 구성에 대한 보다 자세한 설명서는 [Azure 서비스에 대한 Azure Monitor에서 경고 만들기 - Azure Portal](../monitoring-and-diagnostics/insights-alerts-portal.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="43643-274">**경고 규칙** 블레이드에 다음 값을 입력하고 **확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-274">Enter the following values in the **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="43643-275">**설정**</span><span class="sxs-lookup"><span data-stu-id="43643-275">**Setting**</span></span> | <span data-ttu-id="43643-276">**값**</span><span class="sxs-lookup"><span data-stu-id="43643-276">**Value**</span></span> | <span data-ttu-id="43643-277">**세부 정보**</span><span class="sxs-lookup"><span data-stu-id="43643-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="43643-278">**Name**</span><span class="sxs-lookup"><span data-stu-id="43643-278">**Name**</span></span>|<span data-ttu-id="43643-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="43643-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="43643-280">경고 규칙의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-280">Name of the alert rule.</span></span>|
  |<span data-ttu-id="43643-281">**설명**</span><span class="sxs-lookup"><span data-stu-id="43643-281">**Description**</span></span>|<span data-ttu-id="43643-282">전송된 TCP 세그먼트가 임계값을 초과함</span><span class="sxs-lookup"><span data-stu-id="43643-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="43643-283">경고 규칙에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-283">The description for the alert rule.</span></span>||
  |<span data-ttu-id="43643-284">**메트릭**</span><span class="sxs-lookup"><span data-stu-id="43643-284">**Metric**</span></span>|<span data-ttu-id="43643-285">전송된 TCP 세그먼트</span><span class="sxs-lookup"><span data-stu-id="43643-285">TCP segments sent</span></span>| <span data-ttu-id="43643-286">경고를 트리거하는 데 사용할 메트릭입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-286">The metric to use to trigger the alert.</span></span> |
  |<span data-ttu-id="43643-287">**Condition**</span><span class="sxs-lookup"><span data-stu-id="43643-287">**Condition**</span></span>|<span data-ttu-id="43643-288">다음보다 큼</span><span class="sxs-lookup"><span data-stu-id="43643-288">Greater than</span></span>| <span data-ttu-id="43643-289">메트릭을 평가할 때 사용할 조건입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-289">The condition to use when evaluating the metric.</span></span>|
  |<span data-ttu-id="43643-290">**임계값**</span><span class="sxs-lookup"><span data-stu-id="43643-290">**Threshold**</span></span>|<span data-ttu-id="43643-291">100</span><span class="sxs-lookup"><span data-stu-id="43643-291">100</span></span>| <span data-ttu-id="43643-292">경고를 트리거하는 메트릭의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-292">The  value of the metric that triggers the alert.</span></span> <span data-ttu-id="43643-293">이 값은 사용자 환경에 적합한 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-293">This value should be set to a valid value for your environment.</span></span>|
  |<span data-ttu-id="43643-294">**기간**</span><span class="sxs-lookup"><span data-stu-id="43643-294">**Period**</span></span>|<span data-ttu-id="43643-295">지난 5분 이상</span><span class="sxs-lookup"><span data-stu-id="43643-295">Over the last five minutes</span></span>| <span data-ttu-id="43643-296">메트릭에서 임계값을 검색할 기간을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-296">Determines the period in which to look for the threshold on the metric.</span></span>|
  |<span data-ttu-id="43643-297">**웹후크**</span><span class="sxs-lookup"><span data-stu-id="43643-297">**Webhook**</span></span>|<span data-ttu-id="43643-298">[함수 앱에서 웹후크 URL]</span><span class="sxs-lookup"><span data-stu-id="43643-298">[webhook URL from function app]</span></span>| <span data-ttu-id="43643-299">이전 단계에서 만든 함수 앱의 웹후크 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-299">The webhook URL from the function app that was created in the previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="43643-300">기본적으로 TCP 세그먼트 메트릭은 사용되지 않도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="43643-300">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="43643-301">[모니터링 및 진단 사용](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md)을 방문하여 추가 메트릭을 설정하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="43643-301">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-the-results"></a><span data-ttu-id="43643-302">결과 검토</span><span class="sxs-lookup"><span data-stu-id="43643-302">Review the results</span></span>

<span data-ttu-id="43643-303">경고 트리거에 대한 기준에 도달하면 패킷 캡처가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="43643-303">After the criteria for the alert triggers, a packet capture is created.</span></span> <span data-ttu-id="43643-304">Network Watcher로 이동한 다음 **패킷 캡처**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-304">Go to Network Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="43643-305">이 페이지에서 패킷 캡처 파일 링크를 선택하여 패킷 캡처를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-305">On this page, you can select the packet capture file link to download the packet capture.</span></span>

![패킷 캡처 보기][functions14]

<span data-ttu-id="43643-307">캡처 파일이 로컬에 저장된 경우 가상 컴퓨터에 로그인하여 캡처 파일을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="43643-307">If the capture file is stored locally, you can retrieve it by signing in to the virtual machine.</span></span>

<span data-ttu-id="43643-308">Azure Storage 계정에서 파일을 다운로드하는 방법에 대한 지침은 [.NET을 사용하여 Azure Blob Storage 시작](../storage/blobs/storage-dotnet-how-to-use-blobs.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="43643-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="43643-309">사용할 수 있는 다른 도구는 [저장소 탐색기](http://storageexplorer.com/)입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="43643-310">캡처를 다운로드했으면 **.cap** 파일을 읽을 수 있는 도구를 사용하여 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="43643-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="43643-311">다음은 이러한 두 도구에 대한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="43643-311">Following are links to two of these tools:</span></span>

- [<span data-ttu-id="43643-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="43643-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="43643-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="43643-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="43643-314">다음 단계</span><span class="sxs-lookup"><span data-stu-id="43643-314">Next steps</span></span>

<span data-ttu-id="43643-315">[Wireshark로 패킷 캡처 분석](network-watcher-deep-packet-inspection.md)에서 패킷 캡처를 보는 방법을 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="43643-315">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


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
