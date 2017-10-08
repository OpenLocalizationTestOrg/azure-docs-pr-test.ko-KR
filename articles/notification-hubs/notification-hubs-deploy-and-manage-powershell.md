---
title: "aaaDeploy 및 PowerShell을 사용 하 여 알림 허브 관리"
description: "어떻게 tooCreate 및 관리 알림 허브를 사용 하 여 PowerShell 자동화"
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
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="913a8-103">PowerShell을 사용하여 알림 허브 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="913a8-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="913a8-104">개요</span><span class="sxs-lookup"><span data-stu-id="913a8-104">Overview</span></span>
<span data-ttu-id="913a8-105">이 문서에서는 toouse 만들기 및 PowerShell을 사용 하 여 관리할 Azure 알림 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="913a8-106">일반적인 자동화 작업을 수행 하는 hello이이 항목에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="913a8-107">알림 허브 만들기</span><span class="sxs-lookup"><span data-stu-id="913a8-107">Create a Notification Hub</span></span>
* <span data-ttu-id="913a8-108">자격 증명 설정</span><span class="sxs-lookup"><span data-stu-id="913a8-108">Set Credentials</span></span>

<span data-ttu-id="913a8-109">알림 허브에 대 한 새 서비스 버스 네임 스페이스 toocreate도 해야 할 경우 참조 [PowerShell 사용 하 여 서비스 버스 관리](../service-bus-messaging/service-bus-powershell-how-to-provision.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="913a8-110">알림 허브 관리 Azure PowerShell에 포함 된 hello cmdlet에서 직접 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="913a8-111">PowerShell에서 가장 좋은 방법이 hello는 tooreference hello Microsoft.Azure.NotificationHubs.dll 어셈블리.</span><span class="sxs-lookup"><span data-stu-id="913a8-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="913a8-112">hello로 hello 어셈블리는 배포 [Microsoft Azure 알림 허브 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="913a8-113">필수 조건</span><span class="sxs-lookup"><span data-stu-id="913a8-113">Prerequisites</span></span>
<span data-ttu-id="913a8-114">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="913a8-115">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="913a8-115">An Azure subscription.</span></span> <span data-ttu-id="913a8-116">Azure는 구독 기반 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="913a8-117">구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션], [구성원 제공 항목] 또는 [무료 평가판]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="913a8-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="913a8-118">Azure PowerShell이 설치된 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="913a8-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="913a8-119">자세한 내용은 [Azure PowerShell 설치 및 구성]을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="913a8-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="913a8-120">PowerShell 스크립트, NuGet 패키지 및.NET Framework hello 일반 이해 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="913a8-121">서비스 버스에 대 한 참조 toohello.NET 어셈블리를 포함 하 여</span><span class="sxs-lookup"><span data-stu-id="913a8-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="913a8-122">Azure 알림 허브 관리 아직에 포함 되지 않은 hello Azure PowerShell에서 PowerShell cmdlet입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="913a8-123">tooprovision 알림 허브 hello에 제공 된 hello.NET 클라이언트를 사용할 수 있습니다 [Microsoft Azure 알림 허브 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="913a8-124">먼저 스크립트 hello를 찾을 수 있는지 확인 합니다 **Microsoft.Azure.NotificationHubs.dll** 어셈블리는 Visual Studio 프로젝트에서 NuGet 패키지도 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="913a8-125">순서 toobe 유연한, hello 스크립트는 다음이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="913a8-126">호출 된 hello 경로 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="913a8-127">라는 폴더를 찾을 때까지 트래버스하여 hello 경로 `packages`합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="913a8-128">이 폴더는 Visual Studio 프로젝트용 NuGet 패키지를 설치할 때 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="913a8-129">재귀적으로 검색 hello `packages` 이라는 어셈블리에 대 한 폴더 **Microsoft.Azure.NotificationHubs.dll**합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="913a8-130">Hello 유형은 나중에 사용할 수 있도록 참조 어셈블리를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="913a8-131">PowerShell 스크립트에서 이러한 단계는 다음과 같이 구현됩니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="913a8-132">Hello NamespaceManager 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="913a8-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="913a8-133">알림 허브 tooprovision hello의 인스턴스를 만들고 [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) hello SDK에서에서 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="913a8-134">Hello를 사용할 수 있습니다 [Get AzureSBAuthorizationRule] cmdlet에 포함 된 Azure PowerShell tooretrieve 권한 부여 규칙 tooprovide 연결 문자열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="913a8-135">참조 toohello 저장할 것 `NamespaceManager` hello에 대 한 인스턴스 `$NamespaceManager` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="913a8-136">사용 하 여 `$NamespaceManager` tooprovision 알림 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="913a8-137">새 알림 허브 프로비전</span><span class="sxs-lookup"><span data-stu-id="913a8-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="913a8-138">tooprovision 새 알림 허브를 사용 하 여 hello [알림 허브에 대 한.NET API]합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="913a8-139">Hello 스크립트의이 부분에서는 4 개의 지역 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="913a8-140">`$Namespace`:이 toohello 이름을 설정 hello 네임 스페이스의 toocreate 원하는 알림 허브입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="913a8-141">`$Path`: Hello 새 알림 허브의이 경로 toohello 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="913a8-142">예를 들면 "MyHub"와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="913a8-143">`$WnsPackageSid`:이 toohello 패키지 SID에 대해 설정 하면 Windows 응용 프로그램 hello에서 [Windows 개발자 센터](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="913a8-144">`$WnsSecretkey`:이 키를 설정 toohello 비밀 있습니다 Windows 앱에 대 한 hello에서 [Windows 개발자 센터](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="913a8-145">이러한 변수는 사용 되는 tooconnect tooyour 네임 스페이스 및 새 알림 허브 구성 toohandle Notification Services WNS (Windows) 알림 만들기 WNS 자격 증명으로 Windows 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="913a8-146">Hello를 얻는 방법에 대 한 정보에 대 한 패키지 SID 및 비밀 키 참조 hello [알림 허브 시작](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="913a8-147">hello 스크립트 조각 hello를 사용 하 여 `NamespaceManager` hello 알림 허브로 식별 되는 경우 toocheck toosee 개체 `$Path` 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="913a8-148">존재 하지 않는 경우 hello 만들어집니다는 `NotificationHubDescription` WNS와 함께 자격 증명 그리고 해당 toohello 전달 `NamespaceManager` 클래스 `CreateNotificationHub` 메서드.</span><span class="sxs-lookup"><span data-stu-id="913a8-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="913a8-149">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="913a8-149">Additional Resources</span></span>
* [<span data-ttu-id="913a8-150">PowerShell을 사용하여 서비스 버스 관리</span><span class="sxs-lookup"><span data-stu-id="913a8-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="913a8-151">어떻게 toocreate 서비스 버스 큐, 항목 및 PowerShell 스크립트를 사용 하 여 구독</span><span class="sxs-lookup"><span data-stu-id="913a8-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="913a8-152">어떻게 toocreate 서비스 버스 Namespace 및 PowerShell 스크립트를 사용 하 여 이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="913a8-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="913a8-153">즉시 사용 가능한 스크립트도 다운로드 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="913a8-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="913a8-154">Service Bus PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="913a8-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[구매 옵션]: http://azure.microsoft.com/pricing/purchase-options/
[구성원 제공 항목]: http://azure.microsoft.com/pricing/member-offers/
[무료 평가판]: http://azure.microsoft.com/pricing/free-trial/
[Azure PowerShell 설치 및 구성]: /powershell/azureps-cmdlets-docs
[알림 허브에 대 한.NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

