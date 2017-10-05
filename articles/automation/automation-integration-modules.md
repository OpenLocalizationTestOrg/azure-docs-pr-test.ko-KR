---
title: "<span data-ttu-id=\"06d57-101\">Azure Automation 통합 모듈 만들기 | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"06d57-101\">Create an Azure Automation Integration Module | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"06d57-102\">Azure Automation의 통합 모듈을 만들고 테스트하며 예제를 사용하는 과정을 안내하는 자습서입니다.</span><span class=\"sxs-lookup\"><span data-stu-id=\"06d57-102\">Tutorial that walks you through the creation, testing, and example use of  integration modules in Azure Automation.</span></span>"
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
ms.openlocfilehash: aeb06276a52e5472667ae0a741fb3007a91910fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-integration-modules"></a><span data-ttu-id="06d57-103">Azure 자동화 통합 모듈</span><span class="sxs-lookup"><span data-stu-id="06d57-103">Azure Automation Integration Modules</span></span>
<span data-ttu-id="06d57-104">PowerShell은 Azure 자동화의 기본 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-104">PowerShell is the fundamental technology behind Azure Automation.</span></span> <span data-ttu-id="06d57-105">Azure 자동화는 PowerShell을 기반으로 하기 때문에 PowerShell 모듈은 Azure 자동화의 확장성에 대한 키입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-105">Since Azure Automation is built on PowerShell, PowerShell modules are key to the extensibility of Azure Automation.</span></span> <span data-ttu-id="06d57-106">이 문서에서는 "통합 모듈"이라고 하는 PowerShell 모듈에서 Azure 자동화를 만드는 세부 정보 및 Azure 자동화 내에서 통합 모듈로 작동하도록 고유한 PowerShell 모듈을 만드는 모범 사례를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-106">In this article, we will guide you through the specifics of Azure Automation’s use of PowerShell modules, referred to as “Integration Modules”, and best practices for creating your own PowerShell modules to make sure they work as Integration Modules within Azure Automation.</span></span> 

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="06d57-107">PowerShell 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="06d57-107">What is a PowerShell Module?</span></span>
<span data-ttu-id="06d57-108">PowerShell 모듈은 WindowsFeature 또는 파일과 같은 PowerShell 콘솔, 스크립트, 워크플로, Runbook 및 PowerShell DSC 리소스에서 사용할 수 있고 PowerShell DSC 구성에서 사용할 수 있는 **Get-Date** 또는 **Copy-Item**와 같은 PowerShell cmdlet의 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-108">A PowerShell module is a group of PowerShell cmdlets like **Get-Date** or **Copy-Item**, that can be used from the PowerShell console, scripts, workflows, runbooks, and PowerShell DSC resources like WindowsFeature or File, that can be used from PowerShell DSC configurations.</span></span> <span data-ttu-id="06d57-109">모든 PowerShell의 기능은 cmdlet 및 DSC 리소스를 통해 노출되고 모든 cmdlet/DSC 리소스는 PowerShell 모듈에서 지원됩니다. 이 대부분은 PowerShell 자체와 함께 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-109">All of the functionality of PowerShell is exposed through cmdlets and DSC resources, and every cmdlet/DSC resource is backed by a PowerShell module, many of which ship with PowerShell itself.</span></span> <span data-ttu-id="06d57-110">예를 들어 **Get-Date** cmdlet은 Microsoft.PowerShell.Utility PowerShell 모듈의 일부이며 **Copy-Item** cmdlet은 Microsoft.PowerShell.Management PowerShell 모듈의 일부이고 패키지 DSC 리소스는 PSDesiredStateConfiguration PowerShell 모듈의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-110">For example, the **Get-Date** cmdlet is part of the Microsoft.PowerShell.Utility PowerShell module, and **Copy-Item** cmdlet is part of the Microsoft.PowerShell.Management PowerShell module and the Package DSC resource is part of the PSDesiredStateConfiguration PowerShell module.</span></span> <span data-ttu-id="06d57-111">이러한 모듈은 모두 PowerShell과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-111">Both of these modules ship with PowerShell.</span></span> <span data-ttu-id="06d57-112">하지만 많은 PowerShell 모듈은 PowerShell의 일부로 제공되지 않으며 대신 System Center 2012 Configuration Manager에서 자사 또는 타사 제품으로 배포되거나 PowerShell 갤러리와 같은 곳의 방대한 PowerShell 커뮤니티에서 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-112">But many PowerShell modules do not ship as part of PowerShell, and are instead distributed with first or third-party products like System Center 2012 Configuration Manager or by the vast PowerShell community on places like PowerShell Gallery.</span></span>  <span data-ttu-id="06d57-113">모듈은 캡슐화된 기능을 통해 복잡한 작업을 간단하게 만들 수 있기 때문에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-113">The modules are useful because they make complex tasks simpler through encapsulated functionality.</span></span>  <span data-ttu-id="06d57-114">[MSDN의 PowerShell 모듈](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx)에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-114">You can learn more about [PowerShell modules on MSDN](https://msdn.microsoft.com/library/dd878324%28v=vs.85%29.aspx).</span></span> 

## <a name="what-is-an-azure-automation-integration-module"></a><span data-ttu-id="06d57-115">Azure 자동화 통합 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="06d57-115">What is an Azure Automation Integration Module?</span></span>
<span data-ttu-id="06d57-116">통합 모듈은 PowerShell 모듈과 다르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-116">An Integration Module isn't very different from a PowerShell module.</span></span> <span data-ttu-id="06d57-117">단순히 필요에 따라 추가 파일(Runbook에서 모듈의 cmdlet과 함께 사용되는 Azure 자동화 연결 형식을 지정하는 메타데이터 파일)을 포함하는 PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-117">Its simply a PowerShell module that optionally contains one additional file - a metadata file specifying an Azure Automation connection type to be used with the module's cmdlets in runbooks.</span></span> <span data-ttu-id="06d57-118">선택 사항 파일인지 여부와 상관 없이 이러한 PowerShell 모듈은 Azure 자동화로 가져와서 DSC 구성 내에서 사용할 수 있는 runbook 및 DSC 리소스 내에서 해당 cmdlet을 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-118">Optional file or not, these PowerShell modules can be imported into Azure Automation to make their cmdlets available for use within runbooks and their DSC resources available for use within DSC configurations.</span></span> <span data-ttu-id="06d57-119">배후에서 Azure Automation는 이러한 모듈을 저장하고 runbook 작업 및 DSC 컴파일 작업 실행 시 runbook을 실행하고 DSC 구성을 컴파일하는 Azure Automation 샌드박스에 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-119">Behind the scenes, Azure Automation stores these modules, and at runbook job and DSC compilation job execution time, loads them into the Azure Automation sandboxes where runbooks are executed and DSC configurations are compiled.</span></span>  <span data-ttu-id="06d57-120">또는 모듈의 DSC 리소스는 DSC 구성을 적용하려는 컴퓨터에서 가져올 수 있도록 자동으로 자동화 DSC 끌어오기 서버에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-120">Any DSC resources in modules are also automatically placed on the Automation DSC pull server, so that they can be pulled by machines attempting to apply DSC configurations.</span></span>  

<span data-ttu-id="06d57-121">Azure 관리를 즉시 자동화하기 시작할 수 있도록 Azure Automation에서 다양한 Azure PowerShell 모듈을 기본적으로 제공하지만 통합하려는 시스템, 서비스 또는 도구가 무엇이든 PowerShell 모듈을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-121">We ship a number of Azure  PowerShell modules out of the box in Azure Automation for you to use so you can get started automating Azure management right away, but you can import PowerShell modules for whatever system, service, or tool you want to integrate with.</span></span> 

> [!NOTE]
> <span data-ttu-id="06d57-122">특정 모듈은 자동화 서비스에서 "전역 모듈"로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-122">Certain modules are shipped as “global modules” in the Automation service.</span></span> <span data-ttu-id="06d57-123">이러한 전역 모듈은 자동화 계정을 만들 경우에 제공되고 때로 업데이트되어 자동화 계정에 자동으로 푸시됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-123">These global modules are available to you when you create an automation account, and we update them sometimes which automatically pushes them out to your automation account.</span></span> <span data-ttu-id="06d57-124">자동 업데이트하지 않으려면 언제든지 같은 모듈을 직접 가져올 수 있습니다. 그렇게 하면 서비스에 제공된 해당 모듈의 전역 모듈 버전보다 우선적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-124">If you don’t want them to be auto-updated, you can always import the same module yourself, and that will take precedence over the global module version of that module that we ship in the service.</span></span> 

<span data-ttu-id="06d57-125">통합 모듈 패키지를 가져온 형식은 모듈 및.zip 확장명과 동일한 이름을 가진 압축된 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-125">The format in which you import an Integration Module package is a compressed file with the same name as the module and a .zip extension.</span></span> <span data-ttu-id="06d57-126">Windows PowerShell 모듈 및 모듈에 있는 매니페스트 파일(.psd1)를 포함한 모든 지원 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-126">It contains the Windows PowerShell module and any supporting files, including a manifest file (.psd1) if the module has one.</span></span>

<span data-ttu-id="06d57-127">모듈이 Azure Automation 연결 형식을 포함해야 하는 경우 연결 유형 속성을 지정하는 `<ModuleName>-Automation.json`이라는 이름의 파일도 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-127">If the module should contain an Azure Automation connection type, it must also contain a file with the name `<ModuleName>-Automation.json` that specifies the connection type properties.</span></span> <span data-ttu-id="06d57-128">압축된.zip 파일의 모듈 폴더 내에 배치된 json 파일이며 모듈이 나타내는 시스템 또는 서비스에 연결하는 데 필요한 "연결"의 필드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-128">This is a json file placed within the module folder of your compressed .zip file, and contains the fields of a “connection” that is required to connect to the system or service the module represents.</span></span> <span data-ttu-id="06d57-129">결국 Azure 자동화의 연결 형식을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-129">This will end up creating a connection type in Azure Automation.</span></span> <span data-ttu-id="06d57-130">이 파일을 사용하여 필드 이름을 설정할 수 있고 필드에 관계 없이 모듈의 연결 형식에 대한 암호화 및/또는 선택적이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-130">Using this file you can set the field names, types, and whether the fields should be encrypted and / or optional, for the connection type of the module.</span></span> <span data-ttu-id="06d57-131">다음은 json 파일 형식인 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-131">The following is a template in the json file format:</span></span>

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

<span data-ttu-id="06d57-132">서비스 관리 자동화를 배포하고 자동화 runbook에 통합 모듈 패키지를 만든 경우 분명히 매우 익숙하게 느껴질 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-132">If you have deployed Service Management Automation and created Integration Modules packages for your automation runbooks, this should look very familiar to you.</span></span> 

## <a name="authoring-best-practices"></a><span data-ttu-id="06d57-133">작성 모범 사례</span><span class="sxs-lookup"><span data-stu-id="06d57-133">Authoring Best Practices</span></span>
<span data-ttu-id="06d57-134">통합 모듈이 기본적으로 PowerShell 모듈임에도 불구하고 Azure Automation에서도 유용하게 만들려면 PowerShell 모듈을 작성하는 동안 고려해야 할 점이 많습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-134">Even though Integration Modules are essentially PowerShell modules, there’s still a number of things we recommend you consider while authoring a PowerShell module, to make it most usable in Azure Automation.</span></span> <span data-ttu-id="06d57-135">그 중 일부는 Azure 자동화에 특정되고 일부는 자동화를 사용하는지 여부에 관계 없이 PowerShell 워크플로에서 모듈이 잘 작동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-135">Some of these are Azure Automation specific, and some of them are useful just to make your modules work well in PowerShell Workflow, regardless of whether or not you’re using Automation.</span></span> 

1. <span data-ttu-id="06d57-136">모듈에서 모든 cmdlet에 대한 개요, 설명 및 도움말 URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-136">Include a synopsis, description, and help URI for every cmdlet in the module.</span></span> <span data-ttu-id="06d57-137">PowerShell에서는 cmdlet에 대한 도움말 정보를 정의하여 사용자가 **Get-Help** cmdlet과 해당 정보를 통해 도움을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-137">In PowerShell, you can define certain help information for cmdlets to allow the user to receive help on using them with the **Get-Help** cmdlet.</span></span> <span data-ttu-id="06d57-138">예를 들어 .psm1 파일에 기록된 PowerShell 모듈에 대한 개요 및 도움말 URI를 정의할 수 있는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-138">For example, here’s how you can define a synopsis and help URI for a PowerShell module written in a .psm1 file.</span></span><br>  
   
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
   <br> <span data-ttu-id="06d57-139">이 정보를 제공하면 PowerShell 콘솔에서 **Get-Help** cmdlet을 사용하는 도움말을 보여 줄 뿐만 아니라 Azure Automation 내에서 이 도움말 기능을 노출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-139">Providing this info will not only show this help using the **Get-Help** cmdlet in the PowerShell console, it will also expose this help functionality within Azure Automation.</span></span>  <span data-ttu-id="06d57-140">예를 들어, runbook을 작성하는 동안 활동을 삽입하는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-140">For example, when inserting activities during runbook authoring.</span></span> <span data-ttu-id="06d57-141">"자세한 도움말 보기"를 클릭하면 Azure 자동화에 액세스하는 데 사용하는 웹 브라우저의 다른 탭에서 도움말 URI가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-141">Clicking “View detailed help” will open the help URI in another tab of the web browser you’re using to access Azure Automation.</span></span><br><span data-ttu-id="06d57-142">![통합 모듈 도움말](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span><span class="sxs-lookup"><span data-stu-id="06d57-142">![Integration Module Help](media/automation-integration-modules/automation-integration-module-activitydesc.png)</span></span>
2. <span data-ttu-id="06d57-143">원격 시스템에 대해 모듈을 실행하는 경우</span><span class="sxs-lookup"><span data-stu-id="06d57-143">If the module runs against a remote system,</span></span>

    <span data-ttu-id="06d57-144">a.</span><span class="sxs-lookup"><span data-stu-id="06d57-144">a.</span></span> <span data-ttu-id="06d57-145">해당 원격 시스템 즉, 파일 연결 형식에 연결하는 데 필요한 정보를 정의하는 통합 모듈 메타데이터 파일을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-145">It should contain an Integration Module metadata file that defines the information needed to connect to that remote system, meaning the connection type.</span></span>  
    <span data-ttu-id="06d57-146">b.</span><span class="sxs-lookup"><span data-stu-id="06d57-146">b.</span></span> <span data-ttu-id="06d57-147">모듈의 각 cmdlet은 매개 변수로 연결 개체(해당 연결 형식의 인스턴스)를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-147">Each cmdlet in the module should be able to take in a connection object (an instance of that connection type) as a parameter.</span></span>  

    <span data-ttu-id="06d57-148">연결 형식의 필드가 포함된 개체를 cmdlet에 대한 매개 변수로 전달하도록 허용하는 경우 모듈의 cmdlet은 Azure 자동화에서 쉽게 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-148">Cmdlets in the module become easier to use in Azure Automation if you allow passing an object with the fields of the connection type as a parameter to the cmdlet.</span></span> <span data-ttu-id="06d57-149">이 방식으로 사용자는 cmdlet를 호출할 때마다 cmdlet의 해당 매개 변수에 연결 자산의 매개 변수를 매핑할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-149">This way users don’t have to map parameters of the connection asset to the cmdlet's corresponding parameters each time they call a cmdlet.</span></span> <span data-ttu-id="06d57-150">위의 runbook 예제에 따라 CorpTwilio라는 Twilio 연결 자산을 사용하여 Twilio에 액세스하고 계정에서 모든 전화 번호를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-150">Based on the runbook example above, it uses a Twilio connection asset called CorpTwilio to access Twilio and return all the phone numbers in the account.</span></span>  <span data-ttu-id="06d57-151">cmdlet의 매개 변수에 연결의 필드를 매핑하는 방법을 알고 있나요?</span><span class="sxs-lookup"><span data-stu-id="06d57-151">Notice how it is mapping the fields of the connection to the parameters of the cmdlet?</span></span><br>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers 
        -AccountSid $CorpTwilio.AccountSid  
        -AuthToken $CorptTwilio.AuthToken
    }
    ```
  
    <span data-ttu-id="06d57-152">이에 접근하는 더 쉽고 나은 방법은 cmdlet에 직접 연결 개체를 전달하는 것입니다 -</span><span class="sxs-lookup"><span data-stu-id="06d57-152">An easier and better way to approach this is directly passing the connection object to the cmdlet -</span></span>
   
    ```
    workflow Get-CorpTwilioPhones
    {
      $CorpTwilio = Get-AutomationConnection -Name 'CorpTwilio'
   
      Get-TwilioPhoneNumbers -Connection $CorpTwilio
    }
    ```
   
    <span data-ttu-id="06d57-153">매개 변수에 대한 연결 필드 대신에 매개 변수인 연결 개체를 직접 수용할 수 있도록 하여 cmdlet에 다음과 같은 동작을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-153">You can enable behavior like this for your cmdlets by allowing them to accept a connection object directly as a parameter, instead of just connection fields for parameters.</span></span> <span data-ttu-id="06d57-154">일반적으로 각각에 대해 매개 변수를 설정하여 Azure 자동화를 사용하는 사용자가 hashtable을 생성하지 않고 cmdlet를 호출하여 연결 개체의 역할을 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-154">Usually you’ll want a parameter set for each, so that a user not using Azure Automation can call your cmdlets without constructing a hashtable to act as the connection object.</span></span> <span data-ttu-id="06d57-155">연결 필드 속성을 하나씩 전달하는 데 다음 매개 변수 집합 **SpecifyConnectionFields** 를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-155">Parameter set **SpecifyConnectionFields** below is used to pass the connection field properties one by one.</span></span> <span data-ttu-id="06d57-156">**UseConnectionObject** 를 사용하면 연결을 직접 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-156">**UseConnectionObject** lets you pass the connection straight through.</span></span> <span data-ttu-id="06d57-157">보시다시피 [Twilio PowerShell 모듈](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) 의 Send-TwilioSMS cmdlet을 사용하면 한 쪽을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-157">As you can see, the Send-TwilioSMS cmdlet in the [Twilio PowerShell module](https://gallery.technet.microsoft.com/scriptcenter/Twilio-PowerShell-Module-8a8bfef8) allows passing either way:</span></span> 
   
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
3. <span data-ttu-id="06d57-158">모듈에서 모든 cmdlet에 대한 출력 형식을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-158">Define output type for all cmdlets in the module.</span></span> <span data-ttu-id="06d57-159">cmdlet에 대한 출력 형식을 정의하면 디자인 타임 IntelliSense에서 작성 중에 사용하기 위한 cmdlet의 출력 속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-159">Defining an output type for a cmdlet allows design-time IntelliSense to help you determine the output properties of the cmdlet, for use during authoring.</span></span> <span data-ttu-id="06d57-160">자동화 runbook 그래픽을 작성하는 동안 특히 유용하며 이 경우 디자인 타임 지식은 모듈을 사용하는 쉬운 사용자 환경의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-160">It is especially helpful during Automation runbook graphical authoring, where design time knowledge is key to an easy user experience with your module.</span></span><br><br> <span data-ttu-id="06d57-161">![그래픽 Runbook 출력 형식](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span><span class="sxs-lookup"><span data-stu-id="06d57-161">![Graphical Runbook Output Type](media/automation-integration-modules/runbook-graphical-module-output-type.png)</span></span><br> <span data-ttu-id="06d57-162">PowerShell ISE에서 cmdlet의 출력을 실행하지 않는 "사전 입력" 기능과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-162">This is similar to the "type ahead" functionality of a cmdlet's output in PowerShell ISE without having to run it.</span></span><br><br> <span data-ttu-id="06d57-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span><span class="sxs-lookup"><span data-stu-id="06d57-163">![POSH IntelliSense](media/automation-integration-modules/automation-posh-ise-intellisense.png)</span></span><br>
4. <span data-ttu-id="06d57-164">모듈의 Cmdlet은 매개 변수에 복잡한 개체 유형을 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-164">Cmdlets in the module should not take complex object types for parameters.</span></span> <span data-ttu-id="06d57-165">PowerShell 워크플로는 복합 형식을 역직렬화된 형태로 저장한다는 점에서 PowerShell과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-165">PowerShell Workflow is different from PowerShell in that it stores complex types in deserialized form.</span></span> <span data-ttu-id="06d57-166">기본 형식은 기본 요소로 유지되지만 복합 형식은 역직렬화된 버전으로 변환되며 이는 기본적으로 속성 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-166">Primitive types will stay as primitives, but complex types are converted to their deserialized versions, which are essentially property bags.</span></span> <span data-ttu-id="06d57-167">예를 들어 runbook(또는 문제에 대한 PowerShell 워크플로)에서 **Get-Process** cmdlet을 사용하는 경우 예상된 [System.Diagnostic.Process] 형식이 아닌 [Deserialized.System.Diagnostic.Process] 형식의 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-167">For example, if you used the **Get-Process** cmdlet in a runbook (or a PowerShell Workflow for that matter), it would return an object of type [Deserialized.System.Diagnostic.Process], not the expected [System.Diagnostic.Process] type.</span></span> <span data-ttu-id="06d57-168">이 형식에는 역직렬화된 형식으로 동일한 속성이 포함되지만 메서드는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-168">This type has all the same properties as the non-deserialized type, but none of the methods.</span></span> <span data-ttu-id="06d57-169">이 값을 cmdlet에 대한 매개 변수로 전달하려는 경우 cmdlet에서 이 매개 변수에 대한 [System.Diagnostic.Process] 값이 필요하면 다음 오류가 표시됩니다. *'프로세스' 매개 변수에서 인수 변환을 처리할 수 없습니다. 오류: "Deserialized.System.Diagnostics.Process" 형식의 "System.Diagnostics.Process(CcmExec)" 값을 "System.Diagnostics.Process" 형식으로 변환할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="06d57-169">And if you try to pass this value as a parameter to a cmdlet, where the cmdlet expects a [System.Diagnostic.Process] value for this parameter, you’ll receive the following error: *Cannot process argument transformation on parameter 'process'. Error: "Cannot convert the "System.Diagnostics.Process (CcmExec)" value of type  "Deserialized.System.Diagnostics.Process" to type "System.Diagnostics.Process".*</span></span>   <span data-ttu-id="06d57-170">예상된 [System.Diagnostic.Process] 형식 및 지정된 [Deserialized.System.Diagnostic.Process] 형식 간의 형식이 일치하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-170">This is because there is a type mismatch between the expected [System.Diagnostic.Process] type and the given [Deserialized.System.Diagnostic.Process] type.</span></span> <span data-ttu-id="06d57-171">이 문제를 해결하는 방법은 모듈의 cmdlet이 매개 변수에 복합 형식을 사용하지 않도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-171">The way around this issue is to ensure the cmdlets of your module do not take complex types for parameters.</span></span> <span data-ttu-id="06d57-172">작업을 수행하는 잘못된 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-172">Here is the wrong way to do it.</span></span>
   
    ```
    function Get-ProcessDescription {
      param (
            [System.Diagnostic.Process] $process
      )
      $process.Description
    }
    ``` 
    <br>
    <span data-ttu-id="06d57-173">또한 복잡한 개체를 선택하고 사용하는 cmdlet이 내부적으로 사용할 수 있는 기본 요소를 가져오는 올바른 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-173">And here is the right way, taking in a primitive that can be used internally by the cmdlet to grab the complex object and use it.</span></span> <span data-ttu-id="06d57-174">cmdlet이 PowerShell 워크플로가 아닌 PowerShell의 컨텍스트에서 실행되기 때문에 cmdlet 내에서 $process는 잘못된 [System.Diagnostic.Process] 형식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-174">Since cmdlets execute in the context of PowerShell, not PowerShell Workflow, inside the cmdlet $process becomes the correct [System.Diagnostic.Process] type.</span></span>  
   
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
   <span data-ttu-id="06d57-175">Runbook의 연결 자산은 복합 형식인 hashtable이며 이러한 hashtable은 캐스트 예외 없이 해당 –Connection 매개 변수에 대한 cmdlet에 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-175">Connection assets in runbooks are hashtables, which are a complex type, and yet these hashtables seem to be able to be passed into cmdlets for their –Connection parameter perfectly, with no cast exception.</span></span> <span data-ttu-id="06d57-176">기술적으로 일부 PowerShell 형식은 직렬화된 형식에서 역직렬화된 형식으로 제대로 캐스팅할 수 있으며 따라서 역직렬화되지 않은 형식을 허용하는 매개 변수에 대한 cmdlet에 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-176">Technically, some PowerShell types are able to cast properly from their serialized form to their deserialized form, and hence can be passed into cmdlets for parameters accepting the non-deserialized type.</span></span> <span data-ttu-id="06d57-177">Hashtable은 다음 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-177">Hashtable is one of these.</span></span> <span data-ttu-id="06d57-178">모듈 작성자가 정의한 형식이 올바르게 역직렬화되는 방식으로 구현될 수 있지만 고려해야 할 장단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-178">It’s possible for a module author’s defined types to be implemented in a way that they can correctly deserialize as well, but there are some trade-offs to consider.</span></span> <span data-ttu-id="06d57-179">형식에는 기본 생성자, 모든 공용 속성 및 는 PSTypeConverter가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-179">The type needs to have a default constructor, have all of its properties public, and have a PSTypeConverter.</span></span> <span data-ttu-id="06d57-180">그러나 모듈 작성자가 소유하지 않은 미리 정의된 형식의 경우 "수정"할 방법이 없습니다. 따라서 매개 변수 모두에 대한 복합 형식을 방지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-180">However, for already-defined types that the module author does not own, there is no way to “fix” them, hence the recommendation to avoid complex types for parameters all together.</span></span> <span data-ttu-id="06d57-181">Runbook 작성 팁: 어떤 이유로든 cmdlet이 복합 형식 매개 변수를 사용해야 하거나 사용자가 복합 형식 매개 변수가 필요한 다른 사람의 모듈을 사용하는 경우 로컬 PowerShell의 PowerShell 워크플로 runbook 및 PowerShell 워크플로 해결 방법은 복합 형식을 생성하는 cmdlet 및 동일한 InlineScript 작업에서 복합 형식을 사용하는 cmdlet을 래핑하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-181">Runbook Authoring tip: If for some reason your cmdlets need to take a complex type parameter, or you are using someone else’s module that requires a complex type parameter, the workaround in PowerShell Workflow runbooks and PowerShell Workflows in local PowerShell, is to wrap the cmdlet that generates the complex type and the cmdlet that consumes the complex type in the same InlineScript activity.</span></span> <span data-ttu-id="06d57-182">InlineScript가 해당 콘텐츠를 PowerShell 워크플로 대신 PowerShell으로 실행하기 때문에 복합 형식을 생성하는 cmdlet에서는 역직렬화된 복합 형식이 아닌 올바른 형식을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-182">Since InlineScript executes its contents as PowerShell rather than PowerShell Workflow, the cmdlet generating the complex type would produce that correct type, not the deserialized complex type.</span></span>
5. <span data-ttu-id="06d57-183">모듈의 모든 cmdlet을 상태 비저장으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-183">Make all cmdlets in the module stateless.</span></span> <span data-ttu-id="06d57-184">PowerShell 워크플로는 다른 세션에서 워크플로 호출하는 모든 cmdlet을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-184">PowerShell Workflow runs every cmdlet called in the workflow in a different session.</span></span> <span data-ttu-id="06d57-185">즉, 동일한 모듈의 다른 cmdlet에서 생성/수정된 세션 상태에 의존하는 cmdlet은 PowerShell 워크플로 runbook에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-185">This means any cmdlets that depend on session state created / modified by other cmdlets in the same module will not work in PowerShell Workflow runbooks.</span></span>  <span data-ttu-id="06d57-186">다음은 수행해서는 안되는 작업의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-186">Here is an example of what not to do.</span></span>
   
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
6. <span data-ttu-id="06d57-187">모듈은 Xcopy 가능 패키지에 완전히 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-187">The module should be fully contained in an Xcopy-able package.</span></span> <span data-ttu-id="06d57-188">runbook을 실행해야 하는 경우 Azure 자동화 모듈이 자동화 샌드박스에 분산되어 있기 때문에 실행 중인 호스트와 독립적으로 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-188">Because Azure Automation modules are distributed to the Automation sandboxes when runbooks need to execute, they need to work independently of the host they are running on.</span></span> <span data-ttu-id="06d57-189">즉, 모듈 패키지를 압축하고 동일하거나 최신 PowerShell 버전인 다른 호스트에 이동하며 해당 호스트의 PowerShell 환경으로 가져오는 경우 정상적으로 작동할 수 있도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-189">What this means is that you should be able to Zip up the module package, move it to any other host with the same or newer PowerShell version, and have it function as normal when imported into that host’s PowerShell environment.</span></span> <span data-ttu-id="06d57-190">이를 위해서 모듈은 모듈 폴더(Azure 자동화로 가져올 때 압축된 폴더) 외부의 파일 또는 호스트의 고유한 레지스트리 설정(제품의 설정으로 설정됨)에 의존해서 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-190">In order for that to happen, the module should not depend on any files outside the module folder (the folder that gets zipped up when importing into Azure Automation), or on any unique registry settings on a host, such as those set by the install of a product.</span></span> <span data-ttu-id="06d57-191">이 모범 사례를 따르지 않으면 모듈은 Azure Automation에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="06d57-191">If this best practice is not followed, the module will not be usable in Azure Automation.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="06d57-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="06d57-192">Next steps</span></span>

* <span data-ttu-id="06d57-193">PowerShell 워크플로 Runbook을 시작하려면 [내 첫 번째 PowerShell 워크플로 Runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="06d57-193">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="06d57-194">PowerShell 모듈을 만드는 자세한 내용은 [Windows PowerShell 모듈 작성](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="06d57-194">To learn more about creating PowerShell Modules, see [Writing a Windows PowerShell Module](https://msdn.microsoft.com/library/dd878310%28v=vs.85%29.aspx)</span></span>

