---
title: "PowerShell을 사용하여 알림 허브 배포 및 관리"
description: "자동화를 위한 PowerShell을 사용하여 알림 허브를 만들고 관리하는 방법"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="9a82a-103">PowerShell을 사용하여 알림 허브 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="9a82a-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="9a82a-104">개요</span><span class="sxs-lookup"><span data-stu-id="9a82a-104">Overview</span></span>
<span data-ttu-id="9a82a-105">이 문서는 PowerShell을 사용하여 Azure 알림 허브를 만들기 및 관리 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-105">This article shows you how to use Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="9a82a-106">다음과 같은 일반적인 자동화 작업은이 항목에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-106">The following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="9a82a-107">알림 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="9a82a-107">Create a Notification Hub</span></span>
* <span data-ttu-id="9a82a-108">자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="9a82a-108">Set Credentials</span></span>

<span data-ttu-id="9a82a-109">알림 허브용 새 서비스 버스 네임스페이스를 만드는 경우 [PowerShell로 Service Bus 관리](../service-bus-messaging/service-bus-powershell-how-to-provision.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a82a-109">If you also need to create a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="9a82a-110">알림 허브 관리는 Azure PowerShell에 포함된 cmdlet에서 직접 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-110">Managing Notifications Hubs is not supported directly by the cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="9a82a-111">PowerShell에서 Microsoft.Azure.NotificationHubs.dll 어셈블리를 참조하는 것이 최선의 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-111">The best approach from PowerShell is to reference the Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="9a82a-112">어셈블리는 [Microsoft Azure 알림 허브 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)와 함께 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-112">The assembly is distributed with the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a82a-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9a82a-113">Prerequisites</span></span>
<span data-ttu-id="9a82a-114">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-114">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="9a82a-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="9a82a-115">An Azure subscription.</span></span> <span data-ttu-id="9a82a-116">Azure는 구독 기반 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="9a82a-117">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션], [구성원 제공 항목] 또는 [무료 평가판]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a82a-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="9a82a-118">Azure PowerShell이 설치된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9a82a-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="9a82a-119">자세한 내용은 [Azure PowerShell 설치 및 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a82a-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="9a82a-120">PowerShell 스크립트, NuGet 패키지 및 .NET Framework 전반에 대한 지식</span><span class="sxs-lookup"><span data-stu-id="9a82a-120">A general understanding of PowerShell scripts, NuGet packages, and the .NET Framework.</span></span>

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a><span data-ttu-id="9a82a-121">.NET 어셈블리에 서비스 버스에 대한 참조 포함</span><span class="sxs-lookup"><span data-stu-id="9a82a-121">Including a reference to the .NET assembly for Service Bus</span></span>
<span data-ttu-id="9a82a-122">Azure 알림 허브 관리는 아직 Azure PowerShell에서 PowerShell cmdlet에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-122">Managing Azure Notification Hubs is not yet included with the PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="9a82a-123">알림 허브를 프로비전하려면 [Microsoft Azure 알림 허브 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)에서 제공된 .NET 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-123">To provision notification hubs, you can use the .NET client provided in the [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="9a82a-124">먼저 스크립트가 Visual Studio 프로젝트에서 NuGet 패키지로 설치되는 **Microsoft.Azure.NotificationHubs.dll** 어셈블리를 찾을 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-124">First, make sure your script can locate the **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="9a82a-125">유연한 작업을 위해 스크립트는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-125">In order to be flexible, the script performs these steps:</span></span>

1. <span data-ttu-id="9a82a-126">호출된 경로를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-126">Determines the path at which it was invoked.</span></span>
2. <span data-ttu-id="9a82a-127">이름이 `packages`인 폴더를 찾을 때까지 경로를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-127">Traverses the path until it finds a folder named `packages`.</span></span> <span data-ttu-id="9a82a-128">이 폴더는 Visual Studio 프로젝트용 NuGet 패키지를 설치할 때 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="9a82a-129">**Microsoft.Azure.NotificationHubs.dll** 어셈블리에 대한 `packages` 폴더를 재귀적으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-129">Recursively searches the `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="9a82a-130">해당 형식을 나중에 사용할 수 있도록 어셈블리를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-130">References the assembly so that the types are available for later use.</span></span>

<span data-ttu-id="9a82a-131">PowerShell 스크립트에서 이러한 단계는 다음과 같이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a><span data-ttu-id="9a82a-132">NamespaceManager 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="9a82a-132">Create the NamespaceManager class</span></span>
<span data-ttu-id="9a82a-133">알림 허브를 프로비전하려면 SDK에서 [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-133">To provision Notification Hubs, create an instance of the [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from the SDK.</span></span> 

<span data-ttu-id="9a82a-134">Azure PowerShell을 포함하는 [Get-AzureSBAuthorizationRule] cmdlet을 사용하면 연결 문자열을 제공하는 데 사용되는 권한 부여 규칙을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-134">You can use the [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell to retrieve an authorization rule that's used to provide a connection string.</span></span> <span data-ttu-id="9a82a-135">여기서는 `NamespaceManager` 인스턴스에 대한 참조를 `$NamespaceManager` 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-135">We'll store a reference to the `NamespaceManager` instance in the `$NamespaceManager` variable.</span></span> <span data-ttu-id="9a82a-136">`$NamespaceManager` 를 사용하여 알림 허브를 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-136">We will use `$NamespaceManager` to provision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="9a82a-137">새 알림 허브 프로비전</span><span class="sxs-lookup"><span data-stu-id="9a82a-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="9a82a-138">새 알림 허브를 프로비전하려면 [알림 허브용 .NET API]를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-138">To provision a new notification hub, use the [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="9a82a-139">이 스크립트 부분에서는 4개의 로컬 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-139">In this part of the script you set up four local variables.</span></span> 

1. <span data-ttu-id="9a82a-140">`$Namespace` : 알림 허브를 만들려는 네임스페이스 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-140">`$Namespace` : Set this to the name of the namespace where you want to create a notification hub.</span></span>
2. <span data-ttu-id="9a82a-141">`$Path` : 새 알림 허브의 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-141">`$Path` : Set this path to the name of the new notification hub.</span></span>  <span data-ttu-id="9a82a-142">예를 들면 "MyHub"와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="9a82a-143">`$WnsPackageSid` : [Windows 개발자 센터](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)의 Windows 앱용 패키지 SID로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-143">`$WnsPackageSid` : Set this to the package SID for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="9a82a-144">`$WnsSecretkey`: [Windows 개발자 센터](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)의 Windows 앱 비밀 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-144">`$WnsSecretkey`: Set this to the secret key for you Windows App from the [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="9a82a-145">이러한 변수를 네임스페이스에 연결하고 새 알림 허브를 만들어서 Windows 앱용 WNS 자격 증명으로 WNS(Windows Notification Services) 알림을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-145">These variables are used to connect to your namespace and create a new Notification Hub configured to handle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="9a82a-146">패키지SID 및 보안 키를 얻는 방법에 대한 정보는 [알림 허브 시작](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a82a-146">For information on obtaining the package SID and secret key see, the [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="9a82a-147">스크립트 코드 조각은 `NamespaceManager` 개체를 사용하여 `$Path`로 식별되는 알림 허브가 존재하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-147">The script snippet uses the `NamespaceManager` object to check to see if the Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="9a82a-148">존재하지 않는 경우 스크립트가 WNS 자격 증명으로 `NotificationHubDescription`을 만들고 `NamespaceManager` 클래스 `CreateNotificationHub` 메서드로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-148">If it does not exist, the script will create an `NotificationHubDescription` with WNS credentials and pass that to the `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="9a82a-149">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9a82a-149">Additional Resources</span></span>
* [<span data-ttu-id="9a82a-150">PowerShell을 사용하여 Service Bus 관리</span><span class="sxs-lookup"><span data-stu-id="9a82a-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="9a82a-151">PowerShell 스크립트를 사용하여 서비스 버스 큐, 토픽 및 구독을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="9a82a-151">How to create Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="9a82a-152">PowerShell 스크립트를 사용하여 서비스 버스 네임스페이스 및 이벤트 허브를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="9a82a-152">How to create a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="9a82a-153">즉시 사용 가능한 스크립트도 다운로드 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="9a82a-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="9a82a-154">Service Bus PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="9a82a-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

<span data-ttu-id="9a82a-155">[구매 옵션]: http://azure.microsoft.com/pricing/purchase-options/</span><span class="sxs-lookup"><span data-stu-id="9a82a-155">[Purchase Options]: http://azure.microsoft.com/pricing/purchase-options/</span></span>
<span data-ttu-id="9a82a-156">[구성원 제공 항목]: http://azure.microsoft.com/pricing/member-offers/</span><span class="sxs-lookup"><span data-stu-id="9a82a-156">[Member Offers]: http://azure.microsoft.com/pricing/member-offers/</span></span>
<span data-ttu-id="9a82a-157">[무료 평가판]: http://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="9a82a-157">[Free Trial]: http://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="9a82a-158">[Azure PowerShell 설치 및 구성]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="9a82a-158">[Install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="9a82a-159">[알림 허브용 .NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span><span class="sxs-lookup"><span data-stu-id="9a82a-159">[.NET API for Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx</span></span>
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
<span data-ttu-id="9a82a-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span><span class="sxs-lookup"><span data-stu-id="9a82a-160">[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx</span></span>

