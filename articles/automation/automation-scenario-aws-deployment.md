---
title: "Amazon 웹 서비스에서 vm aaaAutomating 배포 | Microsoft Docs"
description: "이 문서에서는 방법을 toouse Amazon 웹 서비스 VM의 Azure 자동화 tooautomate 만들기"
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
ms.openlocfilehash: dd1f3af47d8700ced85a3ee5a406dde1c1311990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---provision-an-aws-virtual-machine"></a><span data-ttu-id="d17a7-103">Azure 자동화 시나리오 - AWS 가상 컴퓨터 프로비전</span><span class="sxs-lookup"><span data-stu-id="d17a7-103">Azure Automation scenario - provision an AWS virtual machine</span></span>
<span data-ttu-id="d17a7-104">이 문서에 대해서도 설명 Azure 자동화 tooprovision를 가상 컴퓨터를 활용 하 여 웹 서비스 AWS (Amazon) 구독에 해당 VM에 특정 이름을 –를 지정 하는 방법을 어떤 AWS tooas hello VM "태그 지정"을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-104">In this article, we demonstrate how you can leverage Azure Automation tooprovision a virtual machine in your Amazon Web Service (AWS) subscription and give that VM a specific name – which AWS refers tooas “tagging” hello VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d17a7-105">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d17a7-105">Prerequisites</span></span>
<span data-ttu-id="d17a7-106">Hello이이 문서에서는 Azure 자동화 계정 및 AWS 구독 toohave 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-106">For hello purposes of this article, you need toohave an Azure Automation account and an AWS subscription.</span></span> <span data-ttu-id="d17a7-107">Azure 자동화 계정을 설정하고 AWS 구독 자격 증명으로 구성하는 데 대한 자세한 내용은 [Configure Authentication with Amazon Web Services(Amazon Web Services로 인증 구성)](automation-configure-aws-account.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d17a7-107">For more information on setting up an Azure Automation account and configuring it with your AWS subscription credentials, review [Configure Authentication with Amazon Web Services](automation-configure-aws-account.md).</span></span>  <span data-ttu-id="d17a7-108">이 계정은 만들지 또는 아래 hello 단계에서이 계정을 참조할 म 처럼 계속 하기 전에 AWS 구독 자격 증명으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-108">This account should be created or updated with your AWS subscription credentials before proceeding, as we will reference this account in hello steps below.</span></span>

## <a name="deploy-amazon-web-services-powershell-module"></a><span data-ttu-id="d17a7-109">Amazon Web Services PowerShell 모듈 배포</span><span class="sxs-lookup"><span data-stu-id="d17a7-109">Deploy Amazon Web Services PowerShell Module</span></span>
<span data-ttu-id="d17a7-110">우리의 VM runbook 프로 비전 작업 hello AWS PowerShell 모듈 toodo를 활용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-110">Our VM provisioning runbook will leverage hello AWS PowerShell module toodo its work.</span></span> <span data-ttu-id="d17a7-111">Hello 단계 tooadd hello 모듈 tooyour 자동화 계정을 AWS 구독 자격 증명을 사용 하 여 구성한 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-111">Perform hello following steps tooadd hello module tooyour Automation account that is configured with your AWS subscription credentials.</span></span>  

1. <span data-ttu-id="d17a7-112">웹 브라우저를 열고 탐색 toohello [PowerShell 갤러리](http://www.powershellgallery.com/packages/AWSPowerShell/) hello에서을 클릭 하 고 **배포 tooAzure 자동화 단추**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-112">Open your web browser and navigate toohello [PowerShell Gallery](http://www.powershellgallery.com/packages/AWSPowerShell/) and click on hello **Deploy tooAzure Automation button**.</span></span><br><br> <span data-ttu-id="d17a7-113">![AWS PS 모듈 가져오기](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span><span class="sxs-lookup"><span data-stu-id="d17a7-113">![AWS PS Module Import](./media/automation-scenario-aws-deployment/powershell-gallery-download-awsmodule.png)</span></span>
2. <span data-ttu-id="d17a7-114">Toohello Azure 로그인 페이지를 이동 하 고를 인증 한 후 있습니다 라우트된 toohello Azure 포털 됩니다 블레이드 다음 hello로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-114">You are taken toohello Azure login page and after authenticating, you will be routed toohello Azure Portal and presented with hello following blade.</span></span><br><br> ![모듈 가져오기 블레이드](./media/automation-scenario-aws-deployment/deploy-aws-powershell-module-parameters.png)
3. <span data-ttu-id="d17a7-116">Hello에서 리소스 그룹 선택 hello **리소스 그룹** 드롭 다운 목록 및 hello 매개 변수 블레이드에서 hello 다음 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-116">Select hello Resource Group from hello **Resource Group** drop-down list and on hello Parameters blade, provide hello following information:</span></span>
   
   * <span data-ttu-id="d17a7-117">Hello에서 **신규 또는 기존 자동화 계정을 (string)** 드롭다운 목록에서 선택 **기존**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-117">From hello **New or Existing Automation Account (string)** drop-down list select **Existing**.</span></span>  
   * <span data-ttu-id="d17a7-118">Hello에 **자동화 계정 이름 (string)** 상자 hello hello 자격 AWS 구독에 대 한 포함 된 자동화 계정이의 hello 정확한 이름 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-118">In hello **Automation Account Name (string)** box, type in hello exact name of hello Automation account that includes hello credentials for your AWS subscription.</span></span>  <span data-ttu-id="d17a7-119">예를 들어, 명명 된 전용된 계정을 만든 경우 **AWSAutomation**, 하는 hello 상자에 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-119">For example, if you created a dedicated account named **AWSAutomation**, then that is what you type in hello box.</span></span>
   * <span data-ttu-id="d17a7-120">선택 hello hello에서 적절 한 지역 **자동화 계정 위치** 드롭 다운 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-120">Select hello appropriate region from hello **Automation Account Location** drop-down list.</span></span>
4. <span data-ttu-id="d17a7-121">Hello 필요한 정보를 모두 입력을 완료 했으면 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-121">When you have completed entering hello required information, click **Create**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d17a7-122">Azure 자동화로 PowerShell 모듈을 가져오는 것도 추출 hello cmdlet 이지만 이러한 활동에는 가져오기 및 hello cmdlet 추출 hello 모듈 완전히 완료 될 때까지 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-122">While importing a PowerShell module into Azure Automation, it is also extracting hello cmdlets and these activities will not appear until hello module has completely finished importing and extracting hello cmdlets.</span></span> <span data-ttu-id="d17a7-123">이 프로세스는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-123">This  process can take a few minutes.</span></span>  
   > <br>
   > 
   > 
5. <span data-ttu-id="d17a7-124">Hello Azure 포털에서에서 3 단계에서 참조 하 고 자동화 계정을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-124">In hello Azure Portal, open your Automation account referenced in step 3.</span></span>
6. <span data-ttu-id="d17a7-125">Hello 클릭 **자산** 타일 및 hello에 **자산** 블레이드, 선택 hello **모듈** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-125">Click on hello **Assets** tile and on hello **Assets** blade, select hello **Modules** tile.</span></span>
7. <span data-ttu-id="d17a7-126">Hello에 **모듈** hello 나타납니다 블레이드 **AWSPowerShell** hello 목록에는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-126">On hello **Modules** blade you will see hello **AWSPowerShell** module in hello list.</span></span>

## <a name="create-aws-deploy-vm-runbook"></a><span data-ttu-id="d17a7-127">AWS 배포 VM Runbook 만들기</span><span class="sxs-lookup"><span data-stu-id="d17a7-127">Create AWS deploy VM runbook</span></span>
<span data-ttu-id="d17a7-128">한 번 AWS PowerShell 모듈 배포 된 hello, 우리 이제 작성할 수는 runbook tooautomate AWS PowerShell 스크립트를 사용 하는 가상 컴퓨터를 프로 비전.</span><span class="sxs-lookup"><span data-stu-id="d17a7-128">Once hello AWS PowerShell Module has been deployed, we can now author a runbook tooautomate provisioning a virtual machine in AWS using a PowerShell script.</span></span> <span data-ttu-id="d17a7-129">다음 hello 단계에서는 어떻게 tooleverage 네이티브 PowerShell 스크립트를 Azure 자동화에서 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-129">hello steps below will demonstrate how tooleverage native PowerShell script in Azure Automation.</span></span>  

> [!NOTE]
> <span data-ttu-id="d17a7-130">추가 옵션 및이 스크립트에 대 한 정보에 대 한 hello를 방문 하십시오 [PowerShell 갤러리](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript)합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-130">For further options and information regarding this script, please visit hello [PowerShell Gallery](https://www.powershellgallery.com/packages/New-AwsVM/DisplayScript).</span></span>
> 

1. <span data-ttu-id="d17a7-131">PowerShell 세션을 열고 hello 다음을 입력 하 여 hello PowerShell 갤러리에서에서 New AwsVM hello PowerShell 스크립트를 다운로드:</span><span class="sxs-lookup"><span data-stu-id="d17a7-131">Download hello PowerShell script New-AwsVM from hello PowerShell Gallery by opening a PowerShell session and typing hello following:</span></span><br>
   ```
   Save-Script -Name New-AwsVM -Path <path>
   ```
   <br>
2. <span data-ttu-id="d17a7-132">Hello Azure 포털에서에서 자동화 계정을 열고 hello 클릭 **Runbook** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-132">From hello Azure Portal, open your Automation account and click hello  **Runbooks** tile.</span></span>  
3. <span data-ttu-id="d17a7-133">Hello에서 **Runbook** 블레이드를 **runbook을 추가할**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-133">From hello **Runbooks** blade, select **Add a runbook**.</span></span>
4. <span data-ttu-id="d17a7-134">Hello에 **runbook을 추가할** 블레이드를 **빠른 생성** (새 runbook 만들기).</span><span class="sxs-lookup"><span data-stu-id="d17a7-134">On hello **Add a runbook** blade, select **Quick Create** (Create a new runbook).</span></span>
5. <span data-ttu-id="d17a7-135">Hello에 **Runbook** 속성 블레이드에서 hello와 runbook에 대 한 hello 이름 상자에 이름 입력 **Runbook 형식** 드롭다운 목록에서 선택 **PowerShell**, 를클릭한다음 **만들**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-135">On hello **Runbook** properties blade, type a name in hello Name box for your runbook and from hello **Runbook type** drop-down list select **PowerShell**, and then click **Create**.</span></span><br><br> <span data-ttu-id="d17a7-136">![모듈 가져오기 블레이드](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span><span class="sxs-lookup"><span data-stu-id="d17a7-136">![Import Module Blade](./media/automation-scenario-aws-deployment/runbook-quickcreate-properties.png)</span></span>
6. <span data-ttu-id="d17a7-137">Hello PowerShell Runbook 편집 블레이드 나타나면 복사한 hello runbook 제작 캔버스에 hello PowerShell 스크립트를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-137">When hello Edit PowerShell Runbook blade appears, copy and paste hello PowerShell script into hello runbook authoring canvas.</span></span><br><br> ![Runbook PowerShell 스크립트](./media/automation-scenario-aws-deployment/runbook-powershell-script.png)<br>
   
    > [!NOTE]
    > <span data-ttu-id="d17a7-139">Hello 예제 PowerShell 스크립트를 작업할 때 다음 hello를 note 하십시오.</span><span class="sxs-lookup"><span data-stu-id="d17a7-139">Please note hello following when working with hello example PowerShell script:</span></span>
    > 
    > * <span data-ttu-id="d17a7-140">hello runbook 다양 한 기본 매개 변수 값을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-140">hello runbook contains a number of default parameter values.</span></span> <span data-ttu-id="d17a7-141">모든 기본 값을 평가하고 필요한 경우 업데이트하세요.</span><span class="sxs-lookup"><span data-stu-id="d17a7-141">Please evaluate all default values and update where necessary.</span></span>
    > * <span data-ttu-id="d17a7-142">자격 증명 자산 보다 다르게 명명 AWS 자격 증명을 저장 한 경우 **AWScred**, 그에 따라 tooupdate hello 스크립트 줄 57 toomatch에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-142">If you have stored your AWS credentials as a credential asset named differently than **AWScred**, you will need tooupdate hello script on line 57 toomatch accordingly.</span></span>  
    > * <span data-ttu-id="d17a7-143">특히이 예제에서는 runbook 사용 하 여 PowerShell에서 AWS CLI 명령을 hello로 작업 하는 경우 hello AWS 영역을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-143">When working with hello AWS CLI commands in PowerShell, especially with this example runbook, you must specify hello AWS region.</span></span> <span data-ttu-id="d17a7-144">그렇지 않으면 hello cmdlet이 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-144">Otherwise, hello cmdlets will fail.</span></span>  <span data-ttu-id="d17a7-145">AWS 항목 보기 [AWS 영역 지정](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) hello AWS 도구에 대 한 자세한 내용은 PowerShell 문서에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-145">View AWS topic [Specify AWS Region](http://docs.aws.amazon.com/powershell/latest/userguide/pstools-installing-specifying-region.html) in hello AWS Tools for PowerShell document for further details.</span></span>  
    >

7. <span data-ttu-id="d17a7-146">AWS 구독에서 이미지 이름의 목록 tooretrieve PowerShell ISE를 시작 하 고 hello AWS PowerShell 모듈을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-146">tooretrieve a list of image names from your AWS subscription, launch PowerShell ISE and import hello AWS PowerShell Module.</span></span>  <span data-ttu-id="d17a7-147">ISE 환경의 **Get-AutomationPSCredential**을 **AWScred = Get-Credential**로 바꿔서 AWS에 대해 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-147">Authenticate against AWS by replacing **Get-AutomationPSCredential** in your ISE environment with **AWScred = Get-Credential**.</span></span>  <span data-ttu-id="d17a7-148">묻는 메시지가 나타납니다에 대 한 자격 증명을 제공할 수 있습니다 프로그램 **액세스 키 ID** hello 사용자 이름에 대 한 및 **암호 선택 키** hello 암호에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-148">This will prompt you for your credentials and you can provide your **Access Key ID** for hello username and **Secret Access Key** for hello password.</span></span>  <span data-ttu-id="d17a7-149">아래 hello 예제를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-149">See hello example below:</span></span>  

        #Sample tooget hello AWS VM available images
        #Please provide hello path where you have downloaded hello AWS PowerShell module
        Import-Module AWSPowerShell
        $AwsRegion = "us-west-2"
        $AwsCred = Get-Credential
        $AwsAccessKeyId = $AwsCred.UserName
        $AwsSecretKey = $AwsCred.GetNetworkCredential().Password
   
        # Set up hello environment tooaccess AWS
        Set-AwsCredentials -AccessKey $AwsAccessKeyId -SecretKey $AwsSecretKey -StoreAs AWSProfile
        Set-DefaultAWSRegion -Region $AwsRegion
   
        Get-EC2ImageByName -ProfileName AWSProfile

    <span data-ttu-id="d17a7-150">hello 다음과 같은 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-150">hello following output is returned:</span></span><br><br><span data-ttu-id="d17a7-151">
   ![AWS 이미지 가져오기](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span><span class="sxs-lookup"><span data-stu-id="d17a7-151">
![Get AWS images](./media/automation-scenario-aws-deployment/powershell-ise-output.png)</span></span><br>  
8. <span data-ttu-id="d17a7-152">에서 복사 및 붙여넣기 hello 이미지 이름 중 하나는 hello로 hello runbook에서 참조 되는 자동화 변수 **$InstanceType**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-152">Copy and paste hello one of hello image names in an Automation variable as referenced in hello runbook as **$InstanceType**.</span></span> <span data-ttu-id="d17a7-153">이후 hello를 사용 하는 것이 예에서 무료 AWS 구독 계층에서는 **t2.micro** runbook 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-153">Since in this example we are using hello free AWS tiered subscription, we'll use **t2.micro** for our runbook example.</span></span>  
9. <span data-ttu-id="d17a7-154">Hello runbook을 저장 한 다음 클릭 **게시** toopublish hello runbook 차례로 **예** 대화 상자가 나타나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-154">Save hello runbook, then click **Publish** toopublish hello runbook and then **Yes** when prompted.</span></span>

### <a name="testing-hello-aws-vm-runbook"></a><span data-ttu-id="d17a7-155">Hello AWS VM runbook 테스트</span><span class="sxs-lookup"><span data-stu-id="d17a7-155">Testing hello AWS VM runbook</span></span>
<span data-ttu-id="d17a7-156">테스트 hello runbook을 계속 진행 하기 전에 tooverify 몇 가지 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-156">Before we proceed with testing hello runbook, we need tooverify a few things.</span></span> <span data-ttu-id="d17a7-157">구체적으로 살펴보면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-157">Specifically:</span></span>  

* <span data-ttu-id="d17a7-158">AWS에 대 한 인증을 위해 자산 만든 호출 **AWScred** 하거나 hello 스크립트 되어 업데이트 된 tooreference hello 이름 자격 증명 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-158">An asset for authenticating against AWS has been created called **AWScred** or hello script has been updated tooreference hello name of your credential asset.</span></span>    
* <span data-ttu-id="d17a7-159">Azure 자동화에서 hello AWS PowerShell 모듈을 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-159">hello AWS PowerShell module has been imported in Azure Automation</span></span>  
* <span data-ttu-id="d17a7-160">새 Runbook을 만든 후 매개 변수 값을 확인하고 필요한 경우 업데이트했습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-160">A new runbook has been created and parameter values have been verified and updated where necessary</span></span>  
* <span data-ttu-id="d17a7-161">**상세 레코드를 기록** 및 필요에 따라 **진행률 레코드를 기록** hello runbook 설정을 **로깅 및 추적** 너무 설정 된**에**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-161">**Log verbose records** and optionally **Log progress records** under hello runbook setting **Logging and tracing** have been set too**On**.</span></span><br><br> <span data-ttu-id="d17a7-162">![Runbook 로깅 및 추적](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span><span class="sxs-lookup"><span data-stu-id="d17a7-162">![Runbook Logging and Tracing](./media/automation-scenario-aws-deployment/runbook-settings-logging-and-tracing.png)</span></span>  

1. <span data-ttu-id="d17a7-163">원하는 toostart hello runbook을 클릭 했습니다 **시작** 클릭 하 고 **확인** hello Runbook 시작 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-163">We want toostart hello runbook, so click **Start** and then click **OK** when hello Start Runbook blade opens.</span></span>
2. <span data-ttu-id="d17a7-164">Hello Runbook 시작 블레이드에서 제공는 **VMname**합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-164">On hello Start Runbook blade, provide a **VMname**.</span></span>  <span data-ttu-id="d17a7-165">Hello에 대 한 hello 기본값 hello 스크립트에서 이전 사전 다른 매개 변수를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-165">Accept hello default values for hello other parameters that you preconfigured in hello script earlier.</span></span>  <span data-ttu-id="d17a7-166">클릭 **확인** toostart hello runbook 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-166">Click **OK** toostart hello runbook job.</span></span><br><br> <span data-ttu-id="d17a7-167">![New-AwsVM Runbook 시작](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span><span class="sxs-lookup"><span data-stu-id="d17a7-167">![Start New-AwsVM runbook](./media/automation-scenario-aws-deployment/runbook-start-job-parameters.png)</span></span>
3. <span data-ttu-id="d17a7-168">방금 만든 hello runbook 작업에 대 한 작업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-168">A job pane is opened for hello runbook job that we just created.</span></span> <span data-ttu-id="d17a7-169">이 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-169">Close this pane.</span></span>
4. <span data-ttu-id="d17a7-170">Hello 작업 및 보기 출력의 진행률을 볼 수 있습니다 **스트림을** hello를 선택 하 여 **모든 로그** hello runbook 작업 블레이드에서 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-170">We can view progress of hello job and view output **Streams** by selecting hello **All Logs** tile from hello runbook job blade.</span></span><br><br> <span data-ttu-id="d17a7-171">![스트림 출력](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span><span class="sxs-lookup"><span data-stu-id="d17a7-171">![Stream output](./media/automation-scenario-aws-deployment/runbook-job-streams-output.png)</span></span>
5. <span data-ttu-id="d17a7-172">현재 로그인 하지 않은 경우 AWS 관리 콘솔 hello 하는 VM을 프로 비전 되 고 tooconfirm hello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="d17a7-172">tooconfirm hello VM is being provisioned, log into hello AWS Management Console if you are not currently logged in.</span></span><br><br> ![AWS 콘솔에서 VM 배포](./media/automation-scenario-aws-deployment/aws-instances-status.png)

## <a name="next-steps"></a><span data-ttu-id="d17a7-174">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d17a7-174">Next steps</span></span>
* <span data-ttu-id="d17a7-175">그래픽 runbook 시작 tooget 참조 [내 첫 번째 그래픽 runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="d17a7-175">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="d17a7-176">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="d17a7-176">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="d17a7-177">runbook 형식이, 장점 및 제한 사항에 대해 자세히 tooknow 참조 [Azure 자동화 runbook 형식](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="d17a7-177">tooknow more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>
* <span data-ttu-id="d17a7-178">PowerShell 스크립트 지원 기능에 대한 자세한 내용은 [Azure 자동화에서 네이티브 PowerShell 스크립트 지원](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span><span class="sxs-lookup"><span data-stu-id="d17a7-178">For more information on PowerShell script support feature, see [Native PowerShell script support in Azure Automation](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)</span></span>

