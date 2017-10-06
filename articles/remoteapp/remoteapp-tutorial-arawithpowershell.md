---
title: "aaaUse Azure RemoteApp과 함께 PowerShell cmdlet | Microsoft Docs"
description: "자세한 내용은 방법 toouse Azure RemoteApp에서 Windows PowerShell cmdlet."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Azure RemoteApp에서 Windows PowerShell cmdlet 사용
> [!IMPORTANT]
> Azure RemoteApp은 2017년 8월 31일에 중단되었습니다. 읽기 hello [알림](https://go.microsoft.com/fwlink/?linkid=821148) 대 한 자세한 내용은 합니다.
> 
> 

 Azure RemoteApp PowerShell cmdlet tooadminister hello를 사용 하 여 수 있으며 사용자 컬렉션을 유지 관리할 수 있습니다. 다음 시작 정보 tooget hello를 사용 합니다.

## <a name="get-hello-cmdlets"></a>Hello cmdlet 가져오기
- - -
먼저 hello Azure Powershell cmdlet 다운로드 [여기](http://go.microsoft.com/?linkid=9811175), hello RemoteApp cmdlet에 포함 되어 있습니다. 

체크 아웃 hello [Azure RemoteApp cmdlet 도움말](/powershell/module/azure?view=azuresmps-3.7.0)합니다.

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Azure cmdlet toouse 구독 구성
- - -
에 따라 [이 가이드](/powershell/azure/overview) Azure 구독에 대해 hello cmdlet을 사용할 수 있도록 합니다.

이러한 단계 tooget 신속 하 게 시작을 사용할 수 있습니다.

1. 다운로드 및 설치 hello [Azure PowerShell cmdlet](http://go.microsoft.com/?linkid=9811175)합니다.
2. Microsoft Azure PowerShell을 시작합니다.
3. 실행 **Add-azureaccount** tooauthenticate tooyour Azure 구독. 입력 메시지가 표시 되 면 동일한 사용자 이름 및 암호 toosign tooAzure 포털에서 사용 하는 hello 합니다.  
4. 실행 **Get-azuresubscription** 사용자 계정과 연결 된 toolist hello 구독 합니다. 
5. 실행 **선택-SubscriptionName &lt;구독 이름&gt;**  또는 **Select-azuresubscription SubscriptionId &lt;구독 ID&gt;**  toospecify hello 구독 toouse 합니다.

축, Azure PowerShell 콘솔은 구성 및 준비 toouse. 필요가 있다는 것 toorepeate 2 ~ 5 단계 hello hello Azure PowerShell 콘솔을 시작할 때마다 알아야 합니다.  


## <a name="list-all-collections"></a>모든 컬렉션 나열
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>컬렉션 삭제
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

예제: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>클라우드 컬렉션 만들기
- - -
아주 간단, hello 다음 명령을 실행 합니다.

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

명령 위에 hello (Excel, OneNote, Outlook, PowerPoint, Visio 및 Word)의 Microsoft Office 365 응용 프로그램에서 자동으로 게시 합니다.

컬렉션 만들기가 30 분 또는 toocomplete 더 오래 걸릴 수 있습니다. 따라서 이 명령은 다음과 같이 사용할 수 있는 추적 ID를 반환합니다.

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Hello 컬렉션을 완료 한 후 다음 명령을 hello로 사용자 toohello 컬렉션을 추가할 수 있습니다.

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

완료되었습니다! 해당 사용자 수 tooconnect toohello hello Azure RemoteApp 클라이언트를 찾을 수를 사용 하 여 응용 프로그램 해야 [여기](https://www.remoteapp.windowsazure.com/)합니다.

## <a name="available-cmdlets"></a>사용할 수 있는 cmdlet
다양 한 다른 명령을, hello 설명서에 곧 제공 될 예정:

기본 RemoteApp 컬렉션 cmdlet: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

RemoteApp 가상 네트워크 cmdlet:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

RemoteApp 템플릿 이미지 cmdlet:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

기타 RemoteApp cmdlet:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

