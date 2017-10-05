---
title: "Event Hubs를 사용하여 Azure Key Vault의 로그 통합 | Microsoft Docs"
description: "Azure 로그 통합을 사용하여 Key Vault 로그를 SIEM에 제공하는 데 필요한 단계를 안내하는 자습서"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="3a2ca-103">Azure 로그 통합 자습서: Event Hubs를 사용하여 Azure Key Vault 이벤트 처리</span><span class="sxs-lookup"><span data-stu-id="3a2ca-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="3a2ca-104">Azure 로그 통합을 사용하여 기록된 이벤트를 검색하고 SIEM(보안 정보 및 이벤트 관리) 시스템에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="3a2ca-105">이 자습서는 Azure 로그 통합을 사용하여 Azure Event Hubs를 통해 획득한 로그를 처리하는 방법의 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="3a2ca-106">이 자습서를 사용하여 예제 단계를 따르고 각 단계가 솔루션을 어떻게 지원하는지 이해하면 Azure 로그 통합 및 Event Hubs가 연동하는 방식에 익숙해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="3a2ca-107">그런 다음 여기서 학습한 내용을 바탕으로 회사 고유의 요구 사항을 지원하기 위한 자신만의 단계를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="3a2ca-108">이 자습서의 단계와 명령은 복사하여 붙여넣을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="3a2ca-109">예제일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-109">They're examples only.</span></span> <span data-ttu-id="3a2ca-110">PowerShell 명령을 라이브 환경에 “있는 그대로” 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="3a2ca-111">이러한 명령은 고유 환경에 맞게 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="3a2ca-112">이 자습서에서는 Azure Key Vault 활동이 이벤트 허브에 기록되도록 하고 JSON 파일로 SIEM 시스템에 제공하는 프로세스를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="3a2ca-113">그런 다음 JSON 파일을 처리하도록 SIEM 시스템을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="3a2ca-114">이 자습서의 단계는 대부분 Key Vault, 저장소 계정 및 이벤트 허브 구성과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="3a2ca-115">특정 Azure 로그 통합 단계는 이 자습서의 끝에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="3a2ca-116">프로덕션 환경에서 다음 단계를 수행하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="3a2ca-117">랩 환경 전용으로 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="3a2ca-118">프러덕션 환경에서 사용하기 전에 단계를 사용자 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="3a2ca-119">함께 제공되는 정보는 각 단계를 수행하는 이유를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="3a2ca-120">다른 아티클에 대한 링크는 특정 토픽에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="3a2ca-121">이 자습서에 언급된 서비스에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="3a2ca-122">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3a2ca-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="3a2ca-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3a2ca-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="3a2ca-124">Azure 로그 통합</span><span class="sxs-lookup"><span data-stu-id="3a2ca-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="3a2ca-125">초기 설치</span><span class="sxs-lookup"><span data-stu-id="3a2ca-125">Initial setup</span></span>

<span data-ttu-id="3a2ca-126">이 아티클의 단계를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="3a2ca-127">Azure 구독 및 관리자 권한이 있는 해당 구독의 계정.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="3a2ca-128">구독이 없는 경우 [무료 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="3a2ca-129">Azure 로그 통합을 설치하기 위한 요구 사항을 충족하는, 인터넷에 액세스할 수 있는 시스템.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="3a2ca-130">시스템은 클라우드 서비스에 있거나 온-프레미스에 호스트될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="3a2ca-131">[Azure 로그 통합](https://www.microsoft.com/download/details.aspx?id=53324) 설치됨.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="3a2ca-132">설치하려면:</span><span class="sxs-lookup"><span data-stu-id="3a2ca-132">To install it:</span></span>

   <span data-ttu-id="3a2ca-133">a.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-133">a.</span></span> <span data-ttu-id="3a2ca-134">원격 데스크톱을 사용하여 2단계에서 언급한 시스템에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="3a2ca-135">b.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-135">b.</span></span> <span data-ttu-id="3a2ca-136">Azure 로그 통합 설치 관리자를 시스템에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="3a2ca-137">[설치 파일을 다운로드](https://www.microsoft.com/download/details.aspx?id=53324)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="3a2ca-138">c.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-138">c.</span></span> <span data-ttu-id="3a2ca-139">설치 관리자를 시작하고 Microsoft 소프트웨어 사용 조건에 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="3a2ca-140">d.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-140">d.</span></span> <span data-ttu-id="3a2ca-141">원격 분석 정보를 입력하는 경우 확인란을 선택한 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="3a2ca-142">사용 정보를 Microsoft로 보내지 않으려면 확인란의 선택을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="3a2ca-143">Azure 로그 통합 및 설치 방법에 대한 자세한 내용은 [Azure 로그 통합, Azure 진단 로깅 및 Windows 이벤트 전달](security-azure-log-integration-get-started.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="3a2ca-144">최신 PowerShell 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="3a2ca-145">Windows Server 2016이 설치되어 있는 경우 PowerShell 5.0 이상이 설치되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="3a2ca-146">다른 버전의 Windows Server를 사용 중인 경우 이전 버전의 PowerShell이 설치되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="3a2ca-147">PowerShell 창에서 ```get-host```를 입력하면 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="3a2ca-148">PowerShell 5.0이 설치되어 있지 않으면 [다운로드](https://www.microsoft.com/download/details.aspx?id=50395)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="3a2ca-149">PowerShell 5.0 이상이 있는 경우 최신 버전 설치를 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="3a2ca-150">a.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-150">a.</span></span> <span data-ttu-id="3a2ca-151">PowerShell 창에서 ```Install-Module Azure``` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="3a2ca-152">설치 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="3a2ca-153">b.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-153">b.</span></span> <span data-ttu-id="3a2ca-154">```Install-Module AzureRM``` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="3a2ca-155">설치 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-155">Complete the installation steps.</span></span>

   <span data-ttu-id="3a2ca-156">자세한 내용은 [Azure PowerShell 설치](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="3a2ca-157">지원 인프라 요소 만들기</span><span class="sxs-lookup"><span data-stu-id="3a2ca-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="3a2ca-158">관리자 권한 PowerShell 창을 열고 **C\Program Files\Microsoft Azure Log Integration**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="3a2ca-159">LoadAzLogModule.ps1 스크립트를 실행하여 AzLog cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="3a2ca-160">`.\LoadAzLogModule.ps1` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="3a2ca-161">(해당 명령에서 “.\” 확인) 다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![로드된 모듈 목록](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="3a2ca-163">`Login-AzureRmAccount` 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="3a2ca-164">로그인 창에서 이 자습서에 사용할 구독에 대한 자격 증명 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3a2ca-165">이 컴퓨터에서 Azure에 처음 로그인하는 경우 Microsoft에서 PowerShell 사용 데이터를 수집하도록 허용하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="3a2ca-166">이 기능은 Azure PowerShell을 개선하는 데 사용되므로, 이 데이터 수집을 사용하도록 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="3a2ca-167">인증에 성공하면 로그인되고 다음 스크린샷의 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="3a2ca-168">구독 ID 및 구독 이름을 메모해 두세요. 이후 단계를 완료하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![PowerShell 창](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="3a2ca-170">나중에 사용할 값을 저장하는 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="3a2ca-171">다음 각 PowerShell 줄을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="3a2ca-172">환경에 맞게 값을 조정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="3a2ca-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(구독 이름은 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="3a2ca-174">이는 이전 명령의 출력에서 볼 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3a2ca-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="3a2ca-175">```$location = 'West US'```(이 변수는 리소스를 만들 위치를 전달하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="3a2ca-176">이 변수를 선택한 위치로 변경할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3a2ca-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="3a2ca-177">``` $name = 'azlogtest' + $random```(이름은 임의로 지정할 수 있지만 소문자와 숫자만 포함해야 합니다.)</span><span class="sxs-lookup"><span data-stu-id="3a2ca-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="3a2ca-178">``` $storageName = $name```(이 변수는 저장소 계정 이름에 사용됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3a2ca-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="3a2ca-179">```$rgname = $name ```(이 변수는 리소스 그룹 이름에 사용됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3a2ca-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="3a2ca-180">``` $eventHubNameSpaceName = $name```(이벤트 허브 네임스페이스의 이름입니다.)</span><span class="sxs-lookup"><span data-stu-id="3a2ca-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="3a2ca-181">작업할 구독을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="3a2ca-182">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="3a2ca-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="3a2ca-183">이때 `$rg`를 입력하면 이 스크린샷과 유사한 출력이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![리소스 그룹 생성 후 출력](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="3a2ca-185">상태 정보를 추적하는 데 사용할 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="3a2ca-186">이벤트 허브 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-186">Create the event hub namespace.</span></span> <span data-ttu-id="3a2ca-187">이 네임스페이스는 이벤트 허브를 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="3a2ca-188">정보 공급자와 함께 사용할 규칙 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="3a2ca-189">가능한 모든 Azure 위치를 가져오고 이후 단계에서 사용할 수 있는 변수에 이름을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="3a2ca-190">a.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="3a2ca-191">b.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="3a2ca-192">이때 `$locations`를 입력하고 Get-AzureRmLocation에서 반환되는 추가 정보 없이 위치 이름이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="3a2ca-193">Azure Resource Manager 로그 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="3a2ca-194">Azure 로그 프로필에 대한 자세한 내용은 [Azure 활동 로그 개요](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3a2ca-195">로그 프로필을 만들려고 할 때 오류 메시지가 표시될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="3a2ca-196">그러면 Get-AzureRmLogProfile 및 Remove-AzureRmLogProfile에 대한 설명서를 검토하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="3a2ca-197">Get-AzureRmLogProfile을 실행하는 경우 로그 프로필에 대한 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="3a2ca-198">```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` 명령을 입력하면 기존 로그 프로필을 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Resource Manager 프로필 오류](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="3a2ca-200">키 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="3a2ca-200">Create a key vault</span></span>

1. <span data-ttu-id="3a2ca-201">키 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="3a2ca-202">키 자격 증명 모음에 대한 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="3a2ca-203">로그 작업 생성</span><span class="sxs-lookup"><span data-stu-id="3a2ca-203">Generate log activity</span></span>

<span data-ttu-id="3a2ca-204">로그 작업을 생성하려면 Key Vault에 요청을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="3a2ca-205">키 생성, 암호 저장 또는 Key Vault에서 암호 읽기 등의 작업은 로그 항목을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="3a2ca-206">현재 저장소 키를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="3a2ca-207">새로운 **key2**를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="3a2ca-208">키를 다시 표시하고 **key2**에 다른 값이 포함된 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="3a2ca-209">암호를 설정하고 읽어서 추가 로그 항목을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="3a2ca-210">a.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-210">a.</span></span> <span data-ttu-id="3a2ca-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![반환된 암호](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="3a2ca-213">Azure 로그 통합 구성</span><span class="sxs-lookup"><span data-stu-id="3a2ca-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="3a2ca-214">Key Vault에서 이벤트 허브에 기록하는 데 필요한 요소를 모두 구성했으므로 이제 Azure 로그 통합을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="3a2ca-215">각 이벤트 허브에 대해 AzLog 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="3a2ca-216">마지막 두 개의 명령을 1분 정도 실행하면 JSON 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="3a2ca-217">**C:\users\AzLog\EventHubJson** 디렉터리를 모니터링하여 이를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ca-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a2ca-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3a2ca-218">Next steps</span></span>

- [<span data-ttu-id="3a2ca-219">Azure 로그 통합 FAQ</span><span class="sxs-lookup"><span data-stu-id="3a2ca-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="3a2ca-220">Azure 로그 통합 시작</span><span class="sxs-lookup"><span data-stu-id="3a2ca-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="3a2ca-221">Azure 리소스의 로그를 SIEM 시스템에 통합</span><span class="sxs-lookup"><span data-stu-id="3a2ca-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
