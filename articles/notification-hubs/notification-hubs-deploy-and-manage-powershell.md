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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>PowerShell을 사용하여 알림 허브 배포 및 관리
## <a name="overview"></a>개요
이 문서에서는 toouse 만들기 및 PowerShell을 사용 하 여 관리할 Azure 알림 허브입니다. 일반적인 자동화 작업을 수행 하는 hello이이 항목에 표시 됩니다.

* 알림 허브 만들기
* 자격 증명 설정

알림 허브에 대 한 새 서비스 버스 네임 스페이스 toocreate도 해야 할 경우 참조 [PowerShell 사용 하 여 서비스 버스 관리](../service-bus-messaging/service-bus-powershell-how-to-provision.md)합니다.

알림 허브 관리 Azure PowerShell에 포함 된 hello cmdlet에서 직접 지원 되지 않습니다. PowerShell에서 가장 좋은 방법이 hello는 tooreference hello Microsoft.Azure.NotificationHubs.dll 어셈블리. hello로 hello 어셈블리는 배포 [Microsoft Azure 알림 허브 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* Azure 구독. Azure는 구독 기반 플랫폼입니다. 구독을 얻는 방법에 대한 자세한 내용은 [구매 옵션], [구성원 제공 항목] 또는 [무료 평가판]을 참조하세요.
* Azure PowerShell이 설치된 컴퓨터 자세한 내용은 [Azure PowerShell 설치 및 구성]을 참조하세요.
* PowerShell 스크립트, NuGet 패키지 및.NET Framework hello 일반 이해 해야 합니다.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>서비스 버스에 대 한 참조 toohello.NET 어셈블리를 포함 하 여
Azure 알림 허브 관리 아직에 포함 되지 않은 hello Azure PowerShell에서 PowerShell cmdlet입니다. tooprovision 알림 허브 hello에 제공 된 hello.NET 클라이언트를 사용할 수 있습니다 [Microsoft Azure 알림 허브 NuGet 패키지](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)합니다.

먼저 스크립트 hello를 찾을 수 있는지 확인 합니다 **Microsoft.Azure.NotificationHubs.dll** 어셈블리는 Visual Studio 프로젝트에서 NuGet 패키지도 설치 됩니다. 순서 toobe 유연한, hello 스크립트는 다음이 단계를 수행합니다.

1. 호출 된 hello 경로 결정 합니다.
2. 라는 폴더를 찾을 때까지 트래버스하여 hello 경로 `packages`합니다. 이 폴더는 Visual Studio 프로젝트용 NuGet 패키지를 설치할 때 생성됩니다.
3. 재귀적으로 검색 hello `packages` 이라는 어셈블리에 대 한 폴더 **Microsoft.Azure.NotificationHubs.dll**합니다.
4. Hello 유형은 나중에 사용할 수 있도록 참조 어셈블리를 hello 합니다.

PowerShell 스크립트에서 이러한 단계는 다음과 같이 구현됩니다.

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

## <a name="create-hello-namespacemanager-class"></a>Hello NamespaceManager 클래스 만들기
알림 허브 tooprovision hello의 인스턴스를 만들고 [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) hello SDK에서에서 클래스입니다. 

Hello를 사용할 수 있습니다 [Get AzureSBAuthorizationRule] cmdlet에 포함 된 Azure PowerShell tooretrieve 권한 부여 규칙 tooprovide 연결 문자열을 사용 합니다. 참조 toohello 저장할 것 `NamespaceManager` hello에 대 한 인스턴스 `$NamespaceManager` 변수입니다. 사용 하 여 `$NamespaceManager` tooprovision 알림 허브입니다.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>새 알림 허브 프로비전
tooprovision 새 알림 허브를 사용 하 여 hello [알림 허브에 대 한.NET API]합니다.

Hello 스크립트의이 부분에서는 4 개의 지역 변수를 설정 합니다. 

1. `$Namespace`:이 toohello 이름을 설정 hello 네임 스페이스의 toocreate 원하는 알림 허브입니다.
2. `$Path`: Hello 새 알림 허브의이 경로 toohello 이름을 설정 합니다.  예를 들면 "MyHub"와 같습니다.    
3. `$WnsPackageSid`:이 toohello 패키지 SID에 대해 설정 하면 Windows 응용 프로그램 hello에서 [Windows 개발자 센터](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)합니다.
4. `$WnsSecretkey`:이 키를 설정 toohello 비밀 있습니다 Windows 앱에 대 한 hello에서 [Windows 개발자 센터](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409)합니다.

이러한 변수는 사용 되는 tooconnect tooyour 네임 스페이스 및 새 알림 허브 구성 toohandle Notification Services WNS (Windows) 알림 만들기 WNS 자격 증명으로 Windows 앱에 대 한 합니다. Hello를 얻는 방법에 대 한 정보에 대 한 패키지 SID 및 비밀 키 참조 hello [알림 허브 시작](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) 자습서입니다. 

* hello 스크립트 조각 hello를 사용 하 여 `NamespaceManager` hello 알림 허브로 식별 되는 경우 toocheck toosee 개체 `$Path` 존재 합니다.
* 존재 하지 않는 경우 hello 만들어집니다는 `NotificationHubDescription` WNS와 함께 자격 증명 그리고 해당 toohello 전달 `NamespaceManager` 클래스 `CreateNotificationHub` 메서드.

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




## <a name="additional-resources"></a>추가 리소스
* [PowerShell을 사용하여 서비스 버스 관리](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [어떻게 toocreate 서비스 버스 큐, 항목 및 PowerShell 스크립트를 사용 하 여 구독](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [어떻게 toocreate 서비스 버스 Namespace 및 PowerShell 스크립트를 사용 하 여 이벤트 허브](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

즉시 사용 가능한 스크립트도 다운로드 가능합니다.

* [Service Bus PowerShell 스크립트](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[구매 옵션]: http://azure.microsoft.com/pricing/purchase-options/
[구성원 제공 항목]: http://azure.microsoft.com/pricing/member-offers/
[무료 평가판]: http://azure.microsoft.com/pricing/free-trial/
[Azure PowerShell 설치 및 구성]: /powershell/azureps-cmdlets-docs
[알림 허브에 대 한.NET API]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

