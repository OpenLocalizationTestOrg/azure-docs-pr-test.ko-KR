---
title: "Amazon Web Services에서 VM 배포 자동화 | Microsoft Docs"
description: "이 문서에서는 Azure 자동화를 사용하여 Amazon Web Service VM 만들기를 자동화하는 방법을 보여 줍니다."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 1d85c01a-d795-4523-8194-84fc15b53838
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/14/2017
ms.author: tiandert; bwren
ms.openlocfilehash: e0b784006b4933fe986890c09afa965934511784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a><span data-ttu-id="c5061-103">Azure 자동화 시나리오 - AWS 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="c5061-103">Azure Automation scenario - provision an AWS virtual machine</span></span>
<span data-ttu-id="c5061-104">이 문서에서는 Azure 자동화를 사용하여 AWS(Amazon Web Service) 구독에서 가상 컴퓨터를 프로비전하고 해당 VM에 특정 이름을 지정하는 방법을 설명합니다. 이는 AWS에서 VM "태그 지정"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-104">In this article, we demonstrate how you can leverage Azure Automation to provision a virtual machine in your Amazon Web Service (AWS) subscription and give that VM a specific name – which AWS refers to as “tagging” the VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5061-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c5061-105">Prerequisites</span></span>
<span data-ttu-id="c5061-106">이 문서에서는 Azure 자동화 계정 및 AWS 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-106">For the purposes of this article, you need to have an Azure Automation account and an AWS subscription.</span></span> <span data-ttu-id="c5061-107">Azure 자동화 계정을 설정하고 AWS 구독 자격 증명으로 구성하는 데 대한 자세한 내용은 [Configure Authentication with Amazon Web Services(Amazon Web Services로 인증 구성)](automation-configure-aws-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5061-107">For more information on setting up an Azure Automation account and configuring it with your AWS subscription credentials, review [Configure Authentication with Amazon Web Services](automation-configure-aws-account.md).</span></span>  <span data-ttu-id="c5061-108">이 계정은 아래 단계에서 참조되므로 먼저 AWS 구독 자격 증명으로 생성하거나 업데이트한 다음 진행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-108">This account should be created or updated with your AWS subscription credentials before proceeding, as we will reference this account in the steps below.</span></span>

## <a name="deploy-amazon-web-services-powershell-module"></a><span data-ttu-id="c5061-109">Amazon Web Services PowerShell 모듈 배포</span><span class="sxs-lookup"><span data-stu-id="c5061-109">Deploy Amazon Web Services PowerShell Module</span></span>
<span data-ttu-id="c5061-110">Microsoft의 VM 프로비전 Runbook은 AWS PowerShell 모듈을 활용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-110">Our VM provisioning runbook will leverage the AWS PowerShell module to do its work.</span></span> <span data-ttu-id="c5061-111">다음 단계를 수행하여 AWS 구독 자격 증명으로 구성된 자동화 계정에 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-111">Perform the following steps to add the module to your Automation account that is configured with your AWS subscription credentials.</span></span>  

1. <span data-ttu-id="c5061-112">웹 브라우저를 열고 [PowerShell 갤러리](http://www.powershellgallery.com/packages/AWSPowerShell/)로 이동하여 **Azure 자동화에 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-112">Open your web browser and navigate to the [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) and click on the **Deploy to Azure Automation button**.</span></span><br><br> <span data-ttu-id="c5061-113">![AWS PS 모듈 가져오기](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span><span class="sxs-lookup"><span data-stu-id="c5061-113">![AWS PS Module Import](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span></span>
2. <span data-ttu-id="c5061-114">Azure 로그인 페이지가 열리고 인증되면 Azure 포털로 이동하여 다음 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-114">You are taken to the Azure login page and after authenticating, you will be routed to the Azure Portal and presented with the following blade.</span></span><br><br> ![모듈 가져오기 블레이드](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. <span data-ttu-id="c5061-116">**리소스 그룹** 드롭다운 목록 및 매개 변수 블레이드에서 리소스 그룹을 선택하고 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-116">Select the Resource Group from the **Resource Group** drop-down list and on the Parameters blade, provide the following information:</span></span>
   
   * <span data-ttu-id="c5061-117">**새 또는 기존 자동화 계정(문자열)** 드롭다운 목록에서 **기존**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-117">From the **New or Existing Automation Account (string)** drop-down list select **Existing**.</span></span>  
   * <span data-ttu-id="c5061-118">**자동화 계정 이름(문자열)** 상자에 AWS 구독에 대한 자격 증명을 포함하는 자동화 계정의 정확한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-118">In the **Automation Account Name (string)** box, type in the exact name of the Automation account that includes the credentials for your AWS subscription.</span></span>  <span data-ttu-id="c5061-119">예를 들어 **AWSAutomation**이라는 전용 계정을 만들었으면 해당 이름을 상자에 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-119">For example, if you created a dedicated account named **AWSAutomation**, then that is what you type in the box.</span></span>
   * <span data-ttu-id="c5061-120">**자동화 계정 위치** 드롭다운 목록에서 해당 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-120">Select the appropriate region from the **Automation Account Location** drop-down list.</span></span>
4. <span data-ttu-id="c5061-121">필요한 정보를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-121">When you have completed entering the required information, click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c5061-122">PowerShell 모듈을 Azure 자동화로 가져올 때 cmdlet도 추출되며 모듈에서 cmdlet 가져오기 및 추출이 완료될 때까지 이러한 활동이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-122">While importing a PowerShell module into Azure Automation, it is also extracting the cmdlets and these activities will not appear until the module has completely finished importing and extracting the cmdlets.</span></span> <span data-ttu-id="c5061-123">이 프로세스는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-123">This  process can take a few minutes.</span></span>  
   > <br>
   > 
   > 
5. <span data-ttu-id="c5061-124">Azure 포털에서 3단계에서 참조된 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-124">In the Azure Portal, open your Automation account referenced in step 3.</span></span>
6. <span data-ttu-id="c5061-125">**자산** 타일을 클릭하고 **자산** 블레이드에서 **모듈** 타일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-125">Click on the **Assets** tile and on the **Assets** blade, select the **Modules** tile.</span></span>
7. <span data-ttu-id="c5061-126">**모듈** 블레이드의 목록에 **AWSPowerShell** 모듈이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-126">On the **Modules** blade you will see the **AWSPowerShell** module in the list.</span></span>

## <a name="create-aws-deploy-vm-runbook"></a><span data-ttu-id="c5061-127">AWS 배포 VM Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="c5061-127">Create AWS deploy VM runbook</span></span>
<span data-ttu-id="c5061-128">AWS PowerShell 모듈을 배포한 후에는 Runbook을 작성하여 PowerShell 스크립트를 통해 AWS에서 가상 컴퓨터를 프로비전하는 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-128">Once the AWS PowerShell Module has been deployed, we can now author a runbook to automate provisioning a virtual machine in AWS using a PowerShell script.</span></span> <span data-ttu-id="c5061-129">다음 단계에서는 Azure 자동화에서 네이티브 PowerShell 스크립트를 활용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-129">The steps below will demonstrate how to leverage native PowerShell script in Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="c5061-130">이 스크립트와 관련된 추가 옵션 및 정보를 보려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="c5061-130">For further options and information regarding this script, please visit the [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).</span></span>
> 

1. <span data-ttu-id="c5061-131">PowerShell 세션을 열고 다음을 입력하여 PowerShell 갤러리에서 PowerShell 스크립트 New-AwsVM을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-131">Download the PowerShell script New-AwsVM from the PowerShell Gallery by opening a PowerShell session and typing the following:</span></span><br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. <span data-ttu-id="c5061-132">Azure Portal에서 자동화 계정을 열고 **Runbook** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-132">From the Azure Portal, open your Automation account and click the  **Runbooks** tile.</span></span>  
3. <span data-ttu-id="c5061-133">**Runbook** 블레이드에서 **Runbook 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-133">From the **Runbooks** blade, select **Add a runbook**.</span></span>
4. <span data-ttu-id="c5061-134">**Runbook 추가** 블레이드에서 **빨리 만들기**(새 Runbook 만들기)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-134">On the **Add a runbook** blade, select **Quick Create** (Create a new runbook).</span></span>
5. <span data-ttu-id="c5061-135">**Runbook** 속성 블레이드에서 Runbook의 이름 상자에 이름을 입력하고 **Runbook 유형** 드롭다운 목록에서 **PowerShell**을 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-135">On the **Runbook** properties blade, type a name in the Name box for your runbook and from the **Runbook type** drop-down list select **PowerShell**, and then click **Create**.</span></span><br><br> <span data-ttu-id="c5061-136">![모듈 가져오기 블레이드](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span><span class="sxs-lookup"><span data-stu-id="c5061-136">![Import Module Blade](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span></span>
6. <span data-ttu-id="c5061-137">PowerShell Runbook 편집 블레이드가 나타나면 PowerShell 스크립트를 복사하여 Runbook 작성 캔버스에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-137">When the Edit PowerShell Runbook blade appears, copy and paste the PowerShell script into the runbook authoring canvas.</span></span><br><br> ![Runbook PowerShell 스크립트](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > <span data-ttu-id="c5061-139">예제 PowerShell 스크립트 작업을 할 때는 다음 사항에 주의하세요.</span><span class="sxs-lookup"><span data-stu-id="c5061-139">Please note the following when working with the example PowerShell script:</span></span>
    > 
    > * <span data-ttu-id="c5061-140">Runbook에는 많은 기본 매개 변수 값이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-140">The runbook contains a number of default parameter values.</span></span> <span data-ttu-id="c5061-141">모든 기본 값을 평가하고 필요한 경우 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="c5061-141">Please evaluate all default values and update where necessary.</span></span>
    > * <span data-ttu-id="c5061-142">AWS 자격 증명을 **AWScred**와 다른 이름의 자격 증명 자산으로 저장한 경우 이에 맞게 스크립트의 57번째 줄을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-142">If you have stored your AWS credentials as a credential asset named differently than **AWScred**, you will need to update the script on line 57 to match accordingly.</span></span>  
    > * <span data-ttu-id="c5061-143">PowerShell에서 AWS CLI 명령을 사용하여 작업할 때 특히 이 예제 Runbook에서는 AWS 영역을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-143">When working with the AWS CLI commands in PowerShell, especially with this example runbook, you must specify the AWS region.</span></span> <span data-ttu-id="c5061-144">그러지 않으면 cmdlet이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-144">Otherwise, the cmdlets will fail.</span></span>  <span data-ttu-id="c5061-145">자세한 내용은 PowerShell용 AWS 도구 설명서의 AWS 항목 [AWS 영역 지정](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5061-145">View AWS topic [Specify AWS Region](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) in the AWS Tools for PowerShell document for further details.</span></span>  
    >

7. <span data-ttu-id="c5061-146">AWS 구독에서 이미지 이름 목록을 검색하려면 PowerShell ISE를 시작하고 AWS PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-146">To retrieve a list of image names from your AWS subscription, launch PowerShell ISE and import the AWS PowerShell Module.</span></span>  <span data-ttu-id="c5061-147">ISE 환경의 **Get-AutomationPSCredential**을 **AWScred = Get-Credential**로 바꿔서 AWS에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-147">Authenticate against AWS by replacing **Get-AutomationPSCredential** in your ISE environment with **AWScred = Get-Credential**.</span></span>  <span data-ttu-id="c5061-148">자격 증명을 요청하는 메시지가 표시되면 암호로 **액세스 키 ID** 및 **보안 액세스 키**를 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-148">This will prompt you for your credentials and you can provide your **Access Key ID** for the username and **Secret Access Key** for the password.</span></span>  <span data-ttu-id="c5061-149">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c5061-149">See the example below:</span></span>  

        #Sample to get the AWS VM available images
        #Please provide the path where you have downloaded the AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up the environment to access AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    <span data-ttu-id="c5061-150">다음과 같은 출력이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-150">The following output is returned:</span></span><br><br><span data-ttu-id="c5061-151">
   ![AWS 이미지 가져오기](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span><span class="sxs-lookup"><span data-stu-id="c5061-151">
![Get AWS images](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span></span><br>  
8. <span data-ttu-id="c5061-152">이미지 이름 중 하나를 복사하여 Runbook에서 **$InstanceType**으로 참조되는 자동화 변수에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-152">Copy and paste the one of the image names in an Automation variable as referenced in the runbook as **$InstanceType**.</span></span> <span data-ttu-id="c5061-153">이 예제에서는 무료 AWS 계층화된 구독을 사용하므로 Runbook 예제에 대해 **t2.micro** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-153">Since in this example we are using the free AWS tiered subscription, we'll use **t2.micro** for our runbook example.</span></span>  
9. <span data-ttu-id="c5061-154">Runbook을 저장하고 **게시**를 클릭하여 Runbook을 게시한 다음 확인 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-154">Save the runbook, then click **Publish** to publish the runbook and then **Yes** when prompted.</span></span>

### <a name="testing-the-aws-vm-runbook"></a><span data-ttu-id="c5061-155">AWS VM Runbook 테스트</span><span class="sxs-lookup"><span data-stu-id="c5061-155">Testing the AWS VM runbook</span></span>
<span data-ttu-id="c5061-156">Runbook 테스트를 진행하기 전에 몇 가지 사항을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-156">Before we proceed with testing the runbook, we need to verify a few things.</span></span> <span data-ttu-id="c5061-157">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-157">Specifically:</span></span>  

* <span data-ttu-id="c5061-158">AWS에 대해 인증하기 위한 **AWScred** 라는 이름의 자산을 만들거나 스크립트가 자격 증명 자산의 이름을 참조하도록 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-158">An asset for authenticating against AWS has been created called **AWScred** or the script has been updated to reference the name of your credential asset.</span></span>    
* <span data-ttu-id="c5061-159">Azure 자동화에서 AWS PowerShell 모듈을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-159">The AWS PowerShell module has been imported in Azure Automation</span></span>  
* <span data-ttu-id="c5061-160">새 Runbook을 만든 후 매개 변수 값을 확인하고 필요한 경우 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-160">A new runbook has been created and parameter values have been verified and updated where necessary</span></span>  
* <span data-ttu-id="c5061-161">Runbook **로깅 및 추적** 설정 아래에서 **상세 레코드 기록** 및 **진행률 레코드 기록**(옵션)을 **사용**으로 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-161">**Log verbose records** and optionally **Log progress records** under the runbook setting **Logging and tracing** have been set to **On**.</span></span><br><br> <span data-ttu-id="c5061-162">![Runbook 로깅 및 추적](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span><span class="sxs-lookup"><span data-stu-id="c5061-162">![Runbook Logging and Tracing](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span></span>  

1. <span data-ttu-id="c5061-163">Runbook을 시작하려면 Runbook 시작 블레이드를 열 때 **시작**을 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-163">We want to start the runbook, so click **Start** and then click **OK** when the Start Runbook blade opens.</span></span>
2. <span data-ttu-id="c5061-164">Runbook 시작 블레이드에서 **VMname**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-164">On the Start Runbook blade, provide a **VMname**.</span></span>  <span data-ttu-id="c5061-165">앞서 스크립트에서 미리 구성한 다른 매개 변수의 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-165">Accept the default values for the other parameters that you preconfigured in the script earlier.</span></span>  <span data-ttu-id="c5061-166">**확인**을 클릭하여 Runbook 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-166">Click **OK** to start the runbook job.</span></span><br><br> <span data-ttu-id="c5061-167">![New-AwsVM Runbook 시작](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span><span class="sxs-lookup"><span data-stu-id="c5061-167">![Start New-AwsVM runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span></span>
3. <span data-ttu-id="c5061-168">우리가 방금 만들었던 runbook작업에 대한 작업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-168">A job pane is opened for the runbook job that we just created.</span></span> <span data-ttu-id="c5061-169">이 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-169">Close this pane.</span></span>
4. <span data-ttu-id="c5061-170">Runbook 작업 블레이드에서 **모든 로그**를 선택하여 작업 진행 상태 및 출력 **스트림**을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5061-170">We can view progress of the job and view output **Streams** by selecting the **All Logs** tile from the runbook job blade.</span></span><br><br> <span data-ttu-id="c5061-171">![스트림 출력](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span><span class="sxs-lookup"><span data-stu-id="c5061-171">![Stream output](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span></span>
5. <span data-ttu-id="c5061-172">VM이 프로비전 중인지 확인하려면 AWS 관리 콘솔에 로그인합니다(현재 로그인되지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="c5061-172">To confirm the VM is being provisioned, log into the AWS Management Console if you are not currently logged in.</span></span><br><br> ![AWS 콘솔에서 VM 배포](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a><span data-ttu-id="c5061-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c5061-174">Next steps</span></span>
* <span data-ttu-id="c5061-175">그래픽 Runbook을 시작하려면 [내 첫 번째 그래픽 Runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="c5061-175">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="c5061-176">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="c5061-176">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="c5061-177">Runbook 형식, 해당 장점 및 제한 사항에 대해 자세히 확인하려면 [Azure 자동화 Runbook 형식](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="c5061-177">To know more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
* <span data-ttu-id="c5061-178">PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span><span class="sxs-lookup"><span data-stu-id="c5061-178">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span></span>

