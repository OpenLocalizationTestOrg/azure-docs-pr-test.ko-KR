---
title: "PowerShell을 사용하여 웹앱 복제"
description: "PowerShell을 사용하여 웹앱을 새 웹앱에 복제하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: d47d5a2f7d2462525bf37718a234e222b4f64e6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>PowerShell을 사용하여 Azure 앱 서비스 앱 복제
새 옵션이 New-AzureRMWebApp에 추가된 Microsoft Azure PowerShell 버전 1.1.0이 출시되어 사용자는 기존 웹앱을 다른 지역이나 동일한 지역에서 새로 만든 앱에 복제할 수 있습니다. 이를 통해 고객은 수많은 앱을 다른 지역에 배포할 수 있습니다.

앱 복제는 현재 프리미엄 계층의 앱 서비스 계획에만 지원됩니다. 새로운 기능은 웹앱 백업 기능과 동일한 제한 사항을 사용합니다. [Azure App Service에서 웹앱 백업](web-sites-backup.md)을 참조하세요.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Azure Resource Manager 기반 Azure PowerShell cmdlet을 사용하여 [Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>기존 앱 복제
시나리오: 사용자가 미국 중남부 지역의 기존 웹앱의 콘텐츠를 미국 중북부 지역의 새 웹앱으로 복제하려고 합니다. 이 작업은 SourceWebApp 옵션으로 새 웹앱을 만들기 위해 PowerShell cmdlet의 Azure Resource Manager 버전을 사용하여 수행할 수 있습니다.

원본 웹앱을 포함하는 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 원본 웹앱의 정보를 가져올 수 있습니다(이 경우 이름은 source-webapp임).

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

새 앱 서비스 계획을 만들려면 다음 예제처럼 New-AzureRmAppServicePlan 명령을 사용할 수 있습니다.

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

New-AzureRmWebApp 명령을 사용하여 미국 중북부 지역에서 새 웹앱을 만들어 기존 프리미엄 계층 앱 서비스 계획에 연결할 수 있으며 또한 원본 웹앱과 동일한 리소스 그룹을 사용하거나 다음과 같이 새 리소스 그룹을 정의할 수 있습니다. 

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

연결된 모든 배포 슬롯을 포함하여 기존 웹앱을 복제하려면 사용자는 IncludeSourceWebAppSlots 매개 변수를 사용해야 합니다. 다음 PowerShell 명령은 New-AzureRmWebApp 명령으로 해당 매개 변수를 사용하는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

동일한 지역 내에서 기존 웹앱을 복제하려면 사용자는 새 리소스 그룹 및 동일한 지역의 새 앱 서비스 계획을 만들고 다음 PowerShell 명령을 사용하여 웹앱을 복제해야 합니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a>기존 앱을 앱 서비스 환경으로 복제
시나리오: 사용자가 기존 미국 중남부 지역의 웹앱의 콘텐츠를 기존 ASE(앱 서비스 환경)에 있는 새 웹앱으로 복제하려고 합니다.

원본 웹앱을 포함하는 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 원본 웹앱의 정보를 가져올 수 있습니다(이 경우 이름은 source-webapp임).

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

ASE의 이름 및 ASE가 속한 리소스 그룹 이름을 알고 있으면 사용자는 New-AzureRmWebApp 명령을 사용하여 다음과 같이 기존 ASE에서 새 웹앱을 만들 수 있습니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

위치 매개 변수는 레거시 때문에 필요하지만 앱을 ASE에서 만드는 경우에는 무시됩니다. 

## <a name="cloning-an-existing-app-slot"></a>기존 앱 슬롯 복제
시나리오: 사용자가 기존 웹앱 슬롯을 새 웹앱이나 새 웹앱 슬롯에 복제하려고 합니다. 새 웹앱은 원래 웹앱 슬롯과 동일한 지역이나 다른 지역에 있을 수 있습니다.

원본 웹앱을 포함한 리소스 그룹 이름을 알고 있으면 다음 PowerShell 명령을 사용하여 웹앱 source-webapp과 연결된 원본 웹앱 슬롯의 정보를 가져올 수 있습니다(이 경우 이름은 source-webappslot임).

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

다음에서는 새 웹앱에 원본 웹앱의 클론을 만드는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>앱을 복제하는 동한 트래픽 관리자 구성
다중 지역 웹앱을 만들고 이러한 웹앱에 트래픽을 라우팅하도록 Azure 트래픽 관리자를 구성하는 것은 고객에게 높은 앱 가용성을 보장하기 위해 매우 중요한 시나리오입니다. 기존 웹앱을 복제할 때 두 웹앱을 새 트래픽 관리자 프로필에 연결할 수도 있고 기존 트래픽 관리자 프로필에 연결할 수도 있습니다. 단, 트래픽 관리자의 Azure Resource Manager 버전만 지원됩니다.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>앱을 복제하는 동안 새 트래픽 관리자 프로필 만들기
시나리오: 사용자가 두 웹앱을 모두 포함하는 Azure Resource Manager 트래픽 관리자 프로필을 구성하는 동안 다른 지역에 웹앱을 복제하려고 합니다. 다음에서는 새 트래픽 관리자 프로필을 구성하는 동안 새 웹앱으로 원본 웹앱의 클론을 만드는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-to-an-existing-traffic-manager-profile"></a>기존 트래픽 관리자 프로필에 복제된 새 웹앱 추가
시나리오: 사용자가 두 웹앱을 끝점으로 추가하려고 하는 Azure Resource Manager 트래픽 관리자 프로필을 이미 가지고 있습니다. 이를 수행하려면 먼저 기존 트래픽 관리자 프로필 ID를 어셈블해야 하며 구독 ID, 리소스 그룹 이름 및 기존 트래픽 관리자 프로필 이름이 필요합니다.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

트래픽 관리자 ID를 알게 된 후 다음에서는 원본 웹앱과 새 웹앱을 기존 트래픽 관리자 프로필에 추가하는 동안 원본 웹앱의 클론을 새 웹앱으로 만드는 방법을 보여 줍니다.

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>현재 제한 사항
이 기능은 현재 미리 보기 상태이며 점차 새 기능을 추가하기 위해 작업 중입니다. 다음 목록은 앱 복제의 현재 버전에 대해 알려진 제한 사항입니다.

* 자동 크기 설정은 복제되지 않습니다.
* 백업 일정 설정은 복제되지 않습니다.
* VNET 설정은 복제되지 않습니다.
* App Insights는 대상 웹앱에서 자동으로 설치되지 않습니다.
* 간편한 인증 설정은 복제되지 않습니다.
* Kudu 확장은 복제되지 않습니다.
* TiP 규칙은 복제되지 않습니다.
* 데이터베이스 내용이 복제되지 않습니다.

### <a name="references"></a>참조
* [Azure 웹앱용 Azure Resource Manager 기반 PowerShell 명령](app-service-web-app-azure-resource-manager-powershell.md)
* [Azure 포털을 사용하여 웹앱 복제](app-service-web-app-cloning-portal.md)
* [Azure 앱 서비스에서 웹앱 백업](web-sites-backup.md)
* [Azure Traffic Manager에 대한 Azure Resource Manager 지원 미리 보기](../traffic-manager/traffic-manager-powershell-arm.md)
* [앱 서비스 환경 소개](app-service-app-service-environment-intro.md)
* [Azure 리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)

