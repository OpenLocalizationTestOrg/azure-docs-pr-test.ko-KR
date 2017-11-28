---
title: "Azure 자동화 통합 모듈 aaaCreate | Microsoft Docs"
description: "자습서는 안내 Azure 자동화에 통합 모듈의 hello 작성, 테스트 및 예제 사용."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 27798efb-08b9-45d9-9b41-5ad91a3df41e
ms.service: automation
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/13/2017
ms.author: magoedte
ms.openlocfilehash: d4064d8b106496f4dab442024131886c4affccab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="6aaf1-103">Azure 자동화 통합 모듈</span><span class="sxs-lookup"><span data-stu-id="6aaf1-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="6aaf1-104">PowerShell은 Azure 자동화 뒤 hello 기본 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-104">PowerShell is hello fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="6aaf1-105">Azure 자동화는 PowerShell을 기반으로, PowerShell 모듈은 Azure 자동화의 핵심 toohello 확장성입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-105">Since Azure Automation is built on PowerShell, PowerShell modules are key toohello extensibility of Azure Automation.</span></span> <span data-ttu-id="6aaf1-106">이 문서에서는 Azure 자동화를 사용 하 여 PowerShell 모듈의 hello 세부 사항 과정을 안내 하, tooas "통합 모듈"을 참조 하 고 사용자 고유의 PowerShell 모듈 toomake 내에서 통합 모듈을 제대로 작동 하는지 확인을 만들기 위한 최상의 방법 Azure 자동화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-106">In this article, we will guide you through hello specifics of Azure Automation’s use of PowerShell modules, referred tooas “Integration Modules”, and best practices for creating your own PowerShell modules toomake sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="6aaf1-107">PowerShell 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="6aaf1-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="6aaf1-108">PowerShell 모듈은 PowerShell cmdlet 등의 그룹 **Get-date** 또는 **Copy-item**, hello PowerShell 콘솔, 스크립트, 워크플로, runbook에서 사용할 수 있는 및 같은 PowerShell DSC 리소스 WindowsFeature 또는 PowerShell DSC 구성에서 사용할 수 있는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from hello PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="6aaf1-109">Cmdlet 및 DSC 리소스를 통해 노출 되는 모든 powershell hello 기능 및 모든 cmdlet/DSC 리소스는 PowerShell 모듈에서 지원 되며 대부분의 PowerShell 자체와 함께 제공입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-109">All of hello functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="6aaf1-110">예를 들어 hello **Get-date** hello Microsoft.PowerShell.Utility PowerShell 모듈의 일부인 cmdlet 및 **Copy-item** hello Microsoft.PowerShell.Management PowerShell 모듈의 일부인 cmdlet 및 hello 패키지 DSC 리소스는 hello PSDesiredStateConfiguration PowerShell 모듈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-110">For example, hello **Get-Date** cmdlet is part of hello Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of hello Microsoft.PowerShell.Management PowerShell module and hello Package DSC resource is part of hello PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="6aaf1-111">이러한 모듈은 모두 PowerShell과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="6aaf1-112">하지만 많은 PowerShell 모듈 PowerShell의 일부로 제공 되지 않은 하 고 대신 System Center 2012 Configuration Manager와 같은 또는 PowerShell 갤러리 같은 위치에 hello vast PowerShell 커뮤니티에서 첫 번째 또는 타사 제품으로 배포 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by hello vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="6aaf1-113">hello 모듈은은 복잡 한 작업 보다 간단 하 게 캡슐화 된 기능을 통해 때문에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-113">hello modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="6aaf1-114">[MSDN의 PowerShell 모듈](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="6aaf1-115">Azure 자동화 통합 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="6aaf1-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="6aaf1-116">통합 모듈은 PowerShell 모듈과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="6aaf1-117">단순히 필요에 따라 추가 파일-runbook에서 hello 모듈의 cmdlet과 함께 사용 되는 Azure 자동화 연결 형식 toobe를 지정 하는 메타 데이터 파일을 포함 하는 PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type toobe used with hello module's cmdlets in runbooks.</span></span> <span data-ttu-id="6aaf1-118">선택 사항 파일 또는 not, 이러한 PowerShell 모듈 DSC 구성에서 사용할 수 있도록 해당 cmdlet에 사용할 수 있는 runbook와 사용할 수 있는 DSC 리소스 내에서 사용 하 여 Azure 자동화 toomake로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-118">Optional file or not, these PowerShell modules can be imported into Azure Automation toomake their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="6aaf1-119">Hello 백그라운드 Azure 자동화 이러한 모듈을 저장 하 고 runbook 작업 및 DSC 컴파일 작업 실행 시간에 있는 runbook이 실행 되 고 DSC 구성이 컴파일됩니다 hello Azure 자동화 샌드박스에 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-119">Behind hello scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into hello Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="6aaf1-120">DSC 리소스 모듈에 tooapply DSC 구성을 시도 하는 컴퓨터에서 가져올 수 있도록에 자동으로 hello 자동화 DSC 끌어오기 서버에 배치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-120">Any DSC resources in modules are also automatically placed on hello Automation DSC pull server, so that they can be pulled by machines attempting tooapply DSC configurations.</span></span>  

<span data-ttu-id="6aaf1-121">즉시, Azure 관리 자동화을 시작할 수 있지만 어떤 시스템, 서비스 또는와 toointegrate 원하는 도구에 대 한 PowerShell 모듈을 가져올 수 있습니다 있습니다 toouse에 대 한 Azure 자동화에서 hello 초기 Azure PowerShell 모듈의 수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-121">We ship a number of Azure  PowerShell modules out of hello box in Azure Automation for you toouse so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want toointegrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="6aaf1-122">특정 모듈에 모듈로"전역" hello 자동화 서비스에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-122">Certain modules are shipped as “global modules” in hello Automation service.</span></span> <span data-ttu-id="6aaf1-123">이러한 전역 모듈은 자동으로 tooyour 자동화 계정에 푸시하는 사용할 수 있는 tooyou 자동화 계정을 만들고 때때로 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-123">These global modules are available tooyou when you create an automation account, and we update them sometimes which automatically pushes them out tooyour automation account.</span></span> <span data-ttu-id="6aaf1-124">할 자동 업데이트, 항상 가져오면 toobe hello 같은 모듈을 직접 및 hello 서비스에서 제공 된 해당 모듈의 hello 전역 모듈 버전이 보다 우선 합니다입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-124">If you don’t want them toobe auto-updated, you can always import hello same module yourself, and that will take precedence over hello global module version of that module that we ship in hello service.</span></span> 

<span data-ttu-id="6aaf1-125">hello 통합 모듈 패키지를 가져오면 형식이 hello 이름과 같은 이름을 hello 모듈 및.zip 확장명을 가진 압축된 파일로.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-125">hello format in which you import an Integration Module package is a compressed file with hello same name as hello module and a .zip extension.</span></span> <span data-ttu-id="6aaf1-126">Hello Windows PowerShell 모듈 및 hello 모듈 하나가 설치 되어 있으면 매니페스트 파일 (.psd1)를 포함 하 여 모든 지원 파일을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-126">It contains hello Windows PowerShell module and any supporting files, including a manifest file (.psd1) if hello module has one.</span></span>

<span data-ttu-id="6aaf1-127">Azure 자동화 연결 형식 hello 모듈을 포함 해야 하는 경우 hello 이름의 파일이 포함 되어야 `<ModuleName>-Automation.json` hello 연결 유형 속성을 지정 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-127">If hello module should contain an Azure Automation connection type, it must also contain a file with hello name `<ModuleName>-Automation.json` that specifies hello connection type properties.</span></span> <span data-ttu-id="6aaf1-128">압축 된.zip 파일의 hello 모듈 폴더 내에 배치 하는 json 파일 이므로 hello 필드를 포함 하는 필수 tooconnect toohello 시스템의 "연결" 또는 서비스 hello 모듈을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-128">This is a json file placed within hello module folder of your compressed .zip file, and contains hello fields of a “connection” that is required tooconnect toohello system or service hello module represents.</span></span> <span data-ttu-id="6aaf1-129">결국 Azure 자동화의 연결 형식을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="6aaf1-130">Hello 필드 이름을 설정할 수 있습니다이 파일을 사용 하 여 형식, 암호화 및/또는 hello 모듈의 hello 연결 유형에 대 한 선택적 hello 필드 여야 하는지 여부 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-130">Using this file you can set hello field names, types, and whether hello fields should be encrypted and / or optional, for hello connection type of hello module.</span></span> <span data-ttu-id="6aaf1-131">hello 다음 hello json 파일 형식으로 서식 파일은입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-131">hello following is a template in hello json file format:</span></span>

```
{ 
   "ConnectionFields": [
   {
      "IsEncrypted":  false,
      "IsOptional":  false,
      "Name":  "ComputerName",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  false,
      "IsOptional":  true,
      "Name":  "Username",
      "TypeName":  "System.String"
   },
   {
      "IsEncrypted":  true,
      "IsOptional":  false,
      "Name":  "Password",
   "TypeName":  "System.String"
   }],
   "ConnectionTypeName":  "DataProtectionManager",
   "IntegrationModuleName":  "DataProtectionManager"
}
```

<span data-ttu-id="6aaf1-132">서비스 관리 자동화를 배포 하면 자동화 runbook에 대 한 통합 모듈 패키지를 만든 경우이 전혀 낯설지 tooyou 찾아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar tooyou.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="6aaf1-133">작성 모범 사례</span><span class="sxs-lookup"><span data-stu-id="6aaf1-133">Authoring Best Practices</span></span>
<span data-ttu-id="6aaf1-134">통합 모듈은 기본적으로 PowerShell 모듈, 이지만 중임을 다양 한 작업 toomake PowerShell 모듈을 제작 하는 동안 고려해 야 하는 것이 좋습니다 Azure 자동화에서 일반적으로 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, toomake it most usable in Azure Automation.</span></span> <span data-ttu-id="6aaf1-135">이 중 일부를 특정, Azure 자동화 되며 그 중 일부는 PowerShell 워크플로에서 잘 작동 하는 모듈 유용한 정당한 toomake 자동화를 사용 하는 여부에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-135">Some of these are Azure Automation specific, and some of them are useful just toomake your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="6aaf1-136">Hello 모듈에 있는 모든 cmdlet에 대 한 URI를 도움말 및 개요, 설명, 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-136">Include a synopsis, description, and help URI for every cmdlet in hello module.</span></span> <span data-ttu-id="6aaf1-137">PowerShell에서 cmdlet tooallow hello 사용자 tooreceive 도움말에 대 한 도움말 정보 특정 hello로 사용 하 여에 정의할 수 있습니다 **Get-help** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-137">In PowerShell, you can define certain help information for cmdlets tooallow hello user tooreceive help on using them with hello **Get-Help** cmdlet.</span></span> <span data-ttu-id="6aaf1-138">예를 들어 .psm1 파일에 기록된 PowerShell 모듈에 대한 개요 및 도움말 URI를 정의할 수 있는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
    ```
    <#
        .SYNOPSIS
         Gets all outgoing phone numbers for this Twilio account 
    #>
    function Get-TwilioPhoneNumbers {
    [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
    HelpUri='http://www.twilio.com/docs/api/rest/outgoing-caller-ids')]
    param(
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AccountSid,
   
       [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [string]
       $AuthToken,
   
       [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
       [ValidateNotNullOrEmpty()]
       [Hashtable]
       $Connection
    )
   
    $cred = CreateTwilioCredential -Connection $Connection -AccountSid $AccountSid -AuthToken $AuthToken
   
    $uri = "$TWILIO_BASE_URL/Accounts/" + $cred.UserName + "/IncomingPhoneNumbers"
   
    $response = Invoke-RestMethod -Method Get -Uri $uri -Credential $cred
   
    $response.TwilioResponse.IncomingPhoneNumbers.IncomingPhoneNumber
    }
    ```
   <br> <span data-ttu-id="6aaf1-139">이 정보를 제공 하는 보여 줄 뿐만 아니라 hello를 사용 하 여이 도움말 **Get-help** cmdlet에 PowerShell 콘솔 hello, 내 Azure 자동화에서이 도움말 기능 노출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-139">Providing this info will not only show this help using hello **Get-Help** cmdlet in hello PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="6aaf1-140">예를 들어, runbook을 작성하는 동안 활동을 삽입하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="6aaf1-141">"자세한 도움말 보기"를 클릭 하는 hello의 다른 탭에 열려 hello 도움말 URI 웹 tooaccess Azure 자동화를 사용 중인 브라우저입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-141">Clicking “View detailed help” will open hello help URI in another tab of hello web browser you’re using tooaccess Azure Automation.</span></span><br><span data-ttu-id="6aaf1-142">![통합 모듈 도움말](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="6aaf1-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="6aaf1-143">Hello 모듈 원격 시스템에 대해 실행 되는 경우</span><span class="sxs-lookup"><span data-stu-id="6aaf1-143">If hello module runs against a remote system,</span></span>

    <span data-ttu-id="6aaf1-144">a.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-144">a.</span></span> <span data-ttu-id="6aaf1-145">Hello 필요한 정보 tooconnect toothat 원격 시스템으로 hello 연결 형식 의미를 정의 하는 통합 모듈 메타 데이터 파일을 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-145">It should contain an Integration Module metadata file that defines hello information needed tooconnect toothat remote system, meaning hello connection type.</span></span>  
    <span data-ttu-id="6aaf1-146">b.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-146">b.</span></span> <span data-ttu-id="6aaf1-147">Hello 모듈에서 각 cmdlet에 매개 변수로 수 tootake 연결 개체 (해당 연결 유형의 인스턴스)에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-147">Each cmdlet in hello module should be able tootake in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="6aaf1-148">Hello 모듈의 Cmdlet 매개 변수 toohello cmdlet으로 hello 연결 유형의 hello 필드와 함께 개체를 전달 하도록 허용 하면 Azure 자동화에 보다 쉽게 toouse 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-148">Cmdlets in hello module become easier toouse in Azure Automation if you allow passing an object with hello fields of hello connection type as a parameter toohello cmdlet.</span></span> <span data-ttu-id="6aaf1-149">이 방식으로 사용자가 없는 cmdlet를 호출할 때마다 hello 연결 자산 toohello cmdlet의 해당 매개 변수에의 toomap 매개 변수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-149">This way users don’t have toomap parameters of hello connection asset toohello cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="6aaf1-150">위의 hello runbook 예제에 따라, CorpTwilio tooaccess Twilio를 호출 하는 Twilio 연결 자산을 사용 하 고 hello 계정에서 모든 hello 전화 번호를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-150">Based on hello runbook example above, it uses a Twilio connection asset called CorpTwilio tooaccess Twilio and return all hello phone numbers in hello account.</span></span>  <span data-ttu-id="6aaf1-151">Hello 연결 hello cmdlet의 매개 변수 toohello의 hello 필드 매핑된다 어떻게 확인할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="6aaf1-151">Notice how it is mapping hello fields of hello connection toohello parameters of hello cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="6aaf1-152">쉽고 더 나은 방법은 tooapproach이 직접 전달 하는 hello 연결 개체 toohello cmdlet-</span><span class="sxs-lookup"><span data-stu-id="6aaf1-152">An easier and better way tooapproach this is directly passing hello connection object toohello cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="6aaf1-153">매개 변수에 대 한 연결 필드를 방금 대신 매개 변수로 직접 tooaccept 연결 개체를 허용 하 여 프로그램 cmdlet에 대 한 다음과 같은 동작을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-153">You can enable behavior like this for your cmdlets by allowing them tooaccept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="6aaf1-154">일반적으로 싶을 각 항목에 대해 설정 된 매개 변수 Azure 자동화를 사용 하지 사용자 hello 연결 개체로 hashtable tooact를 생성 하지 않고 프로그램 cmdlet을 호출할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable tooact as hello connection object.</span></span> <span data-ttu-id="6aaf1-155">매개 변수 집합 **SpecifyConnectionFields** 아래 속성 사용 되는 사용 되는 toopass hello 연결 필드 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-155">Parameter set **SpecifyConnectionFields** below is used toopass hello connection field properties one by one.</span></span> <span data-ttu-id="6aaf1-156">**UseConnectionObject** 전달할 수 있습니다 hello부터 바로 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-156">**UseConnectionObject** lets you pass hello connection straight through.</span></span> <span data-ttu-id="6aaf1-157">볼 수 있듯이 hello 송신 TwilioSMS cmdlet hello에 [Twilio PowerShell 모듈](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) 어느 쪽을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-157">As you can see, hello Send-TwilioSMS cmdlet in hello [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
    ```
    function Send-TwilioSMS {
      [CmdletBinding(DefaultParameterSetName='SpecifyConnectionFields', `
      HelpUri='http://www.twilio.com/docs/api/rest/sending-sms')]
      param(
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AccountSid,
   
         [Parameter(ParameterSetName='SpecifyConnectionFields', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [string]
         $AuthToken,
   
         [Parameter(ParameterSetName='UseConnectionObject', Mandatory=$true)]
         [ValidateNotNullOrEmpty()]
         [Hashtable]
         $Connection
   
       )
    }
    ```
   <br>
3. <span data-ttu-id="6aaf1-158">Hello 모듈에서 모든 cmdlet에 대 한 출력 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-158">Define output type for all cmdlets in hello module.</span></span> <span data-ttu-id="6aaf1-159">출력 속성을 제작 하는 동안 사용 하기 위해 hello cmdlet의를 toohelp hello 결정 cmdlet을 통해 디자인 타임 IntelliSense에 대 한 출력 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-159">Defining an output type for a cmdlet allows design-time IntelliSense toohelp you determine hello output properties of hello cmdlet, for use during authoring.</span></span> <span data-ttu-id="6aaf1-160">특히 유용 자동화 runbook 그래픽 제작 하는 동안 디자인 타임 지식을 키 tooan 쉬운 사용자 경험이 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key tooan easy user experience with your module.</span></span><br><br> <span data-ttu-id="6aaf1-161">![그래픽 Runbook 출력 형식](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="6aaf1-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="6aaf1-162">이것은 유사 toohello "계속 입력" 기능은 cmdlet의 출력 PowerShell ISE에서 toorun 필요 없이 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-162">This is similar toohello "type ahead" functionality of a cmdlet's output in PowerShell ISE without having toorun it.</span></span><br><br> <span data-ttu-id="6aaf1-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="6aaf1-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="6aaf1-164">Hello 모듈의 Cmdlet 매개 변수에 대 한 복잡 한 개체 유형을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-164">Cmdlets in hello module should not take complex object types for parameters.</span></span> <span data-ttu-id="6aaf1-165">PowerShell 워크플로는 복합 형식을 역직렬화된 형태로 저장한다는 점에서 PowerShell과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="6aaf1-166">기본 형식과 기본 형식으로 남아 있지만 복합 유형은 속성 모음 기본적으로 역직렬화 하는 변환 된 tootheir 버전으로.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-166">Primitive types will stay as primitives, but complex types are converted tootheir deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="6aaf1-167">예를 들어, hello를 사용 하는 경우 **Get-process** cmdlet runbook (또는 해당 문제에 대 한 PowerShell 워크플로)에서 [Deserialized.System.Diagnostic.Process] 유형의 개체가 반환, 하지 예상된 [hello는 System.Diagnostic.Process] 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-167">For example, if you used hello **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not hello expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="6aaf1-168">이 형식에 동일한 속성을 역직렬화 할 아닌 형식이 아니라 hello 메서드 hello 대로 hello 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-168">This type has all hello same properties as hello non-deserialized type, but none of hello methods.</span></span> <span data-ttu-id="6aaf1-169">하 고 다음 오류가 hello를 표시 합니다 하면 toopass이이 값으로 hello cmdlet이 매개이 변수에 대 한 [System.Diagnostic.Process] 값에는 매개 변수 tooa cmdlet: *인수 변환 매개 변수 '' 프로세스에서 처리할 수 없습니다. . 오류: "으로 변환할 수 없습니다"Deserialized.System.Diagnostics.Process"tootype"System.Diagnostics.Process"형식의 hello"System.Diagnostics.Process (CcmExec)"값입니다.*</span><span class="sxs-lookup"><span data-stu-id="6aaf1-169">And if you try toopass this value as a parameter tooa cmdlet, where hello cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive hello following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert hello "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" tootype "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="6aaf1-170">Hello 간의 유형이 일치 하지 않습니다 [System.Diagnostic.Process] 유형 및 지정 된 [Deserialized.System.Diagnostic.Process] 유형의으로 hello 필요 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-170">This is because there is a type mismatch between hello expected [System.Diagnostic.Process] type and hello given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="6aaf1-171">이 문제를 해결 hello 방법은 tooensure hello cmdlet 모듈의 매개 변수에 대 한 복합 형식을 사용 하지 않는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-171">hello way around this issue is tooensure hello cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="6aaf1-172">다음은 잘못 된 방법 toodo hello 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-172">Here is hello wrong way toodo it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="6aaf1-173">및 오른쪽으로 hello cmdlet에 의해 내부적으로 사용할 수 있는 기본 형식을 toograb hello 복합 개체를 사용 하 여 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-173">And here is hello right way, taking in a primitive that can be used internally by hello cmdlet toograb hello complex object and use it.</span></span> <span data-ttu-id="6aaf1-174">Cmdlet의 PowerShell hello 컨텍스트에서 실행할, 하지 PowerShell 워크플로, hello cmdlet $process 내를 hello 올바른 [System.Diagnostic.Process] 유형.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-174">Since cmdlets execute in hello context of PowerShell, not PowerShell Workflow, inside hello cmdlet $process becomes hello correct [System.Diagnostic.Process] type.</span></span>  
   
    ```
    function Get-ProcessDescription {
      param (
            [String] $processName
      )
      $process = Get-Process -Name $processName
   
      $process.Description
    }
    ```
   <br>
   <span data-ttu-id="6aaf1-175">Runbook에서 연결 자산은 해시 테이블 요소인 복합 형식 및 이러한 해시 테이블에 대 한 cmdlet에 전달할 toobe 수 toobe 것 처럼 보일 아직 자신의 – 연결 매개 변수 없는 캐스트 예외와 완벽 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem toobe able toobe passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="6aaf1-176">기술적으로 일부 PowerShell 형식은 serialize 된 형식 역직렬화 tootheir 형태로에서 제대로 수 toocast 며 따라서 수 cmdlet에 전달할 수 hello 비 deserialize 할 형식을 수락 하는 매개 변수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-176">Technically, some PowerShell types are able toocast properly from their serialized form tootheir deserialized form, and hence can be passed into cmdlets for parameters accepting hello non-deserialized type.</span></span> <span data-ttu-id="6aaf1-177">Hashtable은 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-177">Hashtable is one of these.</span></span> <span data-ttu-id="6aaf1-178">모듈 작성자의 정의 된 형식의 toobe도 deserialize 올바르게 수 있는 방식으로 구현 되는 않는 일부 장단점 tooconsider.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-178">It’s possible for a module author’s defined types toobe implemented in a way that they can correctly deserialize as well, but there are some trade-offs tooconsider.</span></span> <span data-ttu-id="6aaf1-179">기본 생성자를 형식 요구 toohave hello, 모든 해당 속성 공용 있고는 PSTypeConverter 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-179">hello type needs toohave a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="6aaf1-180">그러나 미리 정의 된 형식에 대 한 해당 hello 모듈 작성자는 그렇지 않습니다 너무 더 "수정", 매개 변수 모두 함께 대 한 권장 사항 tooavoid 복합 유형 이므로 hello를 소유 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-180">However, for already-defined types that hello module author does not own, there is no way too“fix” them, hence hello recommendation tooavoid complex types for parameters all together.</span></span> <span data-ttu-id="6aaf1-181">Runbook을 작성 팁: 프로그램 cmdlet 팜이 필요 tootake 복잡 한 매개 변수를 입력 하거나 다른 사람의 필요한 모듈에 복합 형식 매개 변수, PowerShell 워크플로 runbook의 hello 해결 방법 및 로컬에서 PowerShell 워크플로 사용 하는 경우 PowerShell을 hello 복합 형식을 생성 하는 toowrap hello cmdlet 및 hello에 hello 복합 유형을 사용 하는 hello cmdlet은 동일한 InlineScript 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-181">Runbook Authoring tip: If for some reason your cmdlets need tootake a complex type parameter, or you are using someone else’s module that requires a complex type parameter, hello workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is toowrap hello cmdlet that generates hello complex type and hello cmdlet that consumes hello complex type in hello same InlineScript activity.</span></span> <span data-ttu-id="6aaf1-182">PowerShell 워크플로, hello 복합 형식을 생성 하는 hello cmdlet 해당 올바른 형식을 생성 하지 않고 PowerShell로 해당 콘텐츠를 실행 하는 InlineScript, 이후 하지 hello 복합 형식을 deserialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, hello cmdlet generating hello complex type would produce that correct type, not hello deserialized complex type.</span></span>
5. <span data-ttu-id="6aaf1-183">상태 비저장 hello 모듈에서 모든 cmdlet을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-183">Make all cmdlets in hello module stateless.</span></span> <span data-ttu-id="6aaf1-184">PowerShell 워크플로 다른 세션에서 hello 워크플로 호출 하는 모든 cmdlet을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-184">PowerShell Workflow runs every cmdlet called in hello workflow in a different session.</span></span> <span data-ttu-id="6aaf1-185">즉, 생성 / 동일한 모듈 PowerShell 워크플로 runbook에서 작동 하지 것입니다 hello에 다른 cmdlet에 의해 수정 세션 상태에 종속 된 모든 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-185">This means any cmdlets that depend on session state created / modified by other cmdlets in hello same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="6aaf1-186">상황의 예로 toodo 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-186">Here is an example of what not toodo.</span></span>
   
    ```
    $globalNum = 0
    function Set-GlobalNum {
       param(
           [int] $num
       )
   
       $globalNum = $num
    }
    function Get-GlobalNumTimesTwo {
       $output = $globalNum * 2
   
       $output
    }
    ```
   <br>
6. <span data-ttu-id="6aaf1-187">hello 모듈 Xcopy 가능 패키지에 완전히 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-187">hello module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="6aaf1-188">Azure 자동화 모듈은 runbook 할 tooexecute 분산된 toohello 자동화 샌드박스, toowork hello 호스트에서 실행 중인 독립적으로 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-188">Because Azure Automation modules are distributed toohello Automation sandboxes when runbooks need tooexecute, they need toowork independently of hello host they are running on.</span></span> <span data-ttu-id="6aaf1-189">즉 hello 모듈 패키지를 수 tooZip 수, tooany 이동 해야 다른 호스트와 같은 버전이 나 최신 PowerShell 버전을 hello 있고 해당 호스트의 PowerShell 환경으로 가져올 때 정상적으로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-189">What this means is that you should be able tooZip up hello module package, move it tooany other host with hello same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="6aaf1-190">해당 toohappen hello 모듈 (hello 폴더에 Azure 자동화로 가져올 때를 압축 가져옵니다) hello 모듈 폴더 안에 없는 모든 파일에 의존 하거나 호스트에는 모든 고유 레지스트리 설정, 같은 hello에 설정 된 설치의 제품 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-190">In order for that toohappen, hello module should not depend on any files outside hello module folder (hello folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by hello install of a product.</span></span> <span data-ttu-id="6aaf1-191">이 모범 사례를 따르지 않으면 hello 모듈은 Azure 자동화에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6aaf1-191">If this best practice is not followed, hello module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6aaf1-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6aaf1-192">Next steps</span></span>

* <span data-ttu-id="6aaf1-193">PowerShell 워크플로 runbook 시작 tooget 참조 [내 첫 번째 PowerShell 워크플로 runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="6aaf1-193">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="6aaf1-194">PowerShell 모듈 만들기에 대 한 더 toolearn 참조 [Windows PowerShell 모듈 작성](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="6aaf1-194">toolearn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

