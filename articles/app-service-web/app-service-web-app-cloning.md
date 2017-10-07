---
title: "응용 프로그램 aaaWeb PowerShell을 사용 하 여 복제"
description: "자세한 내용은 방법 tooclone PowerShell을 사용 하 여 웹 앱 toonew 웹 응용 프로그램입니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>PowerShell을 사용하여 Azure 앱 서비스 앱 복제
Microsoft Azure PowerShell의 hello 릴리스에서 새로운 옵션이 되었습니다 버전 1.1.0 추가 tooNew-AzureRMWebApp hello 사용자 hello 기능 tooclone hello 또는 다른 지역에 기존 웹 응용 프로그램 새로 만든 tooa 앱을 제공 하는 동일한 지역입니다. 이렇게 쉽고 신속 하 게 서로 다른 지역의 여러 고객 toodeploy 수의 앱 활성화 됩니다.

앱 복제는 현재 프리미엄 계층의 앱 서비스 계획에만 지원됩니다. 새 기능 사용 hello hello 동일한 웹 앱 백업 기능으로, 제한 사항 참조 [Azure 앱 서비스의 웹 앱 백업](web-sites-backup.md)합니다.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Azure 리소스 관리자를 사용 하는 방법에 대 한 toolearn 기반 Azure PowerShell cmdlet toomanage 웹 응용 프로그램 확인 [Azure 리소스 관리자 기반 Azure 웹 앱에 대 한 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>기존 앱 복제
시나리오: 미국 중남부 지역에서 기존 웹 앱, hello 사용자 것인지 tooclone hello 내용을 tooa 새 웹 앱에서 North Central US 지역은 합니다. 이 hello-SourceWebApp 옵션과 함께 hello PowerShell cmdlet toocreate 새 웹 앱의 hello Azure 리소스 관리자 버전을 사용 하 여 수행할 수 있습니다.

Hello 리소스를 알고 있으면 hello 소스 웹 앱이 포함 된 그룹 이름을 다음 PowerShell 명령 tooget hello 소스 웹 응용 프로그램의 정보 (이 예제의 소스 webapp 명명 된) hello에 사용할 수 있습니다.

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

새 앱 서비스 계획 toocreate, hello 다음 예제와 같이 새로 AzureRmAppServicePlan 명령을 사용할 수 있습니다.

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

새로 만들기-AzureRmWebApp hello 명령을 사용 하 여, म 수 있는데 hello North Central US 지역은에서 hello 새 웹 앱을 만들 tooan 기존 premium 계층 앱 서비스 계획을 연결, 또한 동일한 리소스 hello 소스 웹 응용 프로그램으로 그룹화 하거나 새 리소스 그룹을 정의 하는 hello에 사용할 수 있습니다. hello 다음을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

모든 연결 된 배포 슬롯을 포함 하 여 기존 웹 앱, hello 사용자가 필요로 toouse tooclone hello IncludeSourceWebAppSlots 매개 변수, 다음 PowerShell 명령을 hello 새로 AzureRmWebApp 명령 hello로 해당 매개 변수의 hello 사용을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone hello 내에서 기존 웹 앱 같은 지역의 hello 사용자가 필요로 hello에 대 한 새 리소스 그룹 및 새 앱 서비스 계획 toocreate 동일한 지역 및 사용 하 여 hello 다음 PowerShell 명령 tooclone hello 웹 응용 프로그램

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>기존 앱 tooan 앱 서비스 환경 복제
시나리오: 미국 중남부 지역에서 기존 웹 앱, hello 사용자 것인지 tooclone hello 내용을 tooa 새 웹 앱 tooan 기존 앱 서비스 환경 (ASE) 합니다.

Hello 리소스를 알고 있으면 hello 소스 웹 앱이 포함 된 그룹 이름을 다음 PowerShell 명령 tooget hello 소스 웹 응용 프로그램의 정보 (이 예제의 소스 webapp 명명 된) hello에 사용할 수 있습니다.

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Hello ASE 이름 및 hello 리소스 그룹 이름에 속하는 hello ASE를 알고 있으면 hello 사용자 צ ְ ײ hello 새로 AzureRmWebApp 명령에 따라 hello hello 기존 ASE toocreate hello 새 웹 앱을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

hello 위치 매개 변수 toolegacy 이유 때문에 필요 하지만 hello ASE에 응용 프로그램을 만드는 경우에서에 무시 됩니다 됩니다. 

## <a name="cloning-an-existing-app-slot"></a>기존 앱 슬롯 복제
시나리오: hello 사용자 tooclone 기존 웹 앱 슬롯 tooeither 새 웹 앱 또는 새 웹 앱 슬롯을 원합니다. 새 웹 앱도 hello 가능 hello hello 원본 웹 앱 슬롯으로 또는 다른 지역에 동일한 영역입니다.

Hello 리소스를 알고 있으면 hello 소스 웹 앱이 포함 된 그룹 이름을 다음 PowerShell 명령을 tooget hello 소스 웹 앱 슬롯의 정보 (이 예제의 소스 webappslot 명명 된) 연결 tooWeb 앱 소스 webapp hello에 사용할 수 있습니다.

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

hello 다음 hello 소스 웹 응용 프로그램 tooa 새 웹 앱의 복제본을 만드는 하는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>앱을 복제하는 동한 트래픽 관리자 구성
다중 지역 웹 응용 프로그램을 만들어 Azure 트래픽 관리자 tooroute 트래픽 tooall 이러한 웹 응용 프로그램 구성 되는 고객의 앱이 있는 기존 웹 앱을 복제할 때 항상 사용 가능한 중요 한 시나리오 n tooinsure hello 옵션 tooconnect 모두 웹 앱 tooeither 트래픽 관리자 프로필을 새 또는 기존-참고 해당만 Azure 리소스 관리자 버전의 트래픽 관리자가 지원 합니다.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>앱을 복제하는 동안 새 트래픽 관리자 프로필 만들기
시나리오: hello 사용자가 두 웹 앱이 포함 된 Azure 리소스 관리자 트래픽 관리자 프로필을 구성 하는 동안 웹 앱 tooanother 영역 tooclone를 원하는 합니다. hello 다음 새로운 트래픽 관리자 프로필을 구성 하는 동안 hello 소스 웹 응용 프로그램 tooa 새 웹 앱의 복제본을 만드는 하는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>새 복제 된 웹 응용 프로그램 tooan 기존 트래픽 관리자 프로필을 추가합니다.
시나리오: hello 사용자는 Azure 리소스 관리자 트래픽 관리자 프로필을 이미 있는 tooadd 싶어합니다 둘 다 웹 앱 끝점으로 합니다. toodo 따라서 먼저 먼저 tooassemble 기존 트래픽 관리자 프로필 id hello, hello 구독 id, 리소스 그룹 이름 및 hello 기존 트래픽 관리자 프로필 이름이 필요 합니다.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Hello 트래픽 관리자 id를 가진, 후 hello 다음 tooan 기존 트래픽 관리자 프로필을 추가 하는 동안 hello 소스 웹 응용 프로그램 tooa 새 웹 앱의 복제본을 만드는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>현재 제한 사항
이 기능은 현재 미리 보기, 시간이 지남에 따라 tooadd 새로운 기능을 노력 하 고, hello 목록 다음에 복제 하는 응용 프로그램의 현재 버전 hello에 대 한 알려진된 제한 hello 됩니다.

* 자동 크기 설정은 복제되지 않습니다.
* 백업 일정 설정은 복제되지 않습니다.
* VNET 설정은 복제되지 않습니다.
* App Insights 설정 되지 않는 자동으로 hello 대상 웹 응용 프로그램
* 간편한 인증 설정은 복제되지 않습니다.
* Kudu 확장은 복제되지 않습니다.
* TiP 규칙은 복제되지 않습니다.
* 데이터베이스 내용이 복제되지 않습니다.

### <a name="references"></a>참조
* [Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)
* [Azure 포털을 사용하여 웹앱 복제](app-service-web-app-cloning-portal.md)
* [Azure 앱 서비스에서 웹앱 백업](web-sites-backup.md)
* [Azure Traffic Manager에 대한 Azure Resource Manager 지원 미리 보기](../traffic-manager/traffic-manager-powershell-arm.md)
* [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)
* [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)

