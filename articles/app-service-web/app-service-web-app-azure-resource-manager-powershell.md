---
title: "Azure 웹 앱에 대 한 리소스 관리자 기반 PowerShell aaaAzure 명령을 | Microsoft Docs"
description: "어떻게 toouse hello 새 Azure 리소스 관리자 기반 PowerShell 명령을 toomanage Azure 웹 앱에 알아봅니다."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Azure Resource Manager-Based PowerShell tooManage Azure 웹 앱을 사용 하 여
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Microsoft Azure powershell 버전 1.0.0 새로운 명령이 추가 된 hello 사용자 hello 기능 toouse Azure 리소스 관리자 기반 PowerShell 명령을 toomanage 웹 응용 프로그램을 제공 하는 합니다.

리소스 그룹을 관리 하는 방법에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../powershell-azure-resource-manager.md)합니다. 

매개 변수 및 hello PowerShell cmdlet에 대 한 옵션의 전체 목록 hello에 대 한 toolearn hello 참조 [전체 웹 앱 Azure 리소스 관리자 기반 PowerShell Cmdlet의 Cmdlet 참조](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>앱 서비스 계획 관리
### <a name="create-an-app-service-plan"></a>앱 서비스 계획 만들기
앱 서비스 계획을 toocreate hello를 사용 하 여 **새로 AzureRmAppServicePlan** cmdlet.

다음은 hello 다른 매개 변수:

* **이름**: hello 앱 서비스 계획의 이름입니다.
* **Location**: 서비스 계획 위치.
* **ResourceGroupName**: 새로 만든 hello 앱 서비스 계획을 포함 하는 리소스 그룹입니다.
* **계층**: hello 가격 책정 계층을 원하는 (기본값은 무료, 공유, Basic, Standard 및 Premium 다른 옵션은)
* **WorkerSize**: hello (기본값은 작은 경우 Basic, Standard 또는 Premium으로 hello 계층 매개 변수가 지정 되었습니다 작업자의 크기. 다른 옵션은 Medium 및 Large입니다.)
* **작업자**: (기본값은 1) hello 앱 서비스 계획의 작업자 수가 hello 합니다. 

예제 toouse이이 cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>앱 서비스 환경에서 앱 서비스 계획 만들기
앱 서비스 환경에 toocreate 앱 서비스 계획, 사용 하 여 hello 동일 명령 **새로 AzureRmAppServicePlan** toospecify hello ASE의 추가 매개 변수 이름과 ASE의 리소스 그룹 이름을 가진 명령을 합니다.

예제 toouse이이 cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

앱 서비스 환경을 검사 하는 방법에 대 한 자세한 toolearn [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>기존 앱 서비스 계획 나열
toolist hello 기존 앱 서비스 계획을 사용 하 여 **Get AzureRmAppServicePlan** cmdlet.

toolist 모든 앱 서비스 계획에서 구독을 사용 합니다. 

    Get-AzureRmAppServicePlan

toolist 특정 리소스 그룹 아래의 모든 앱 서비스 계획을 사용 합니다.

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget 특정 앱 서비스 계획을 사용 합니다.

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>기존 앱 서비스 계획 구성
기존 앱 서비스 계획에 대 한 toochange hello 설정을 사용 하 여 hello **집합 AzureRmAppServicePlan** cmdlet. Hello 계층, 작업자 크기 및 hello 작업자 수를 변경할 수 있습니다. 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>앱 서비스 계획 크기 조정
tooscale는 기존 앱 서비스 계획을 사용 합니다.

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>앱 서비스 계획의 hello 작업자 크기를 변경
기존 앱 서비스 계획을 사용 하 여 작업자의 toochange hello 크기:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>앱 서비스 계획의 계층 hello 변경
기존 앱 서비스 계획을 사용 하 여의 toochange hello 계층:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>기존 앱 서비스 계획 삭제
기존 앱 서비스 계획 toodelete 모두 할당 됨 웹 앱 필요 toobe 이동 하거나 먼저 삭제 합니다. 그런 다음 hello를 사용 하 여 **제거 AzureRmAppServicePlan** cmdlet hello 앱 서비스 계획을 삭제할 수 있습니다.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>앱 서비스 웹앱 관리
### <a name="create-a-web-app"></a>웹앱 만들기
toocreate 웹 응용 프로그램에서 사용 하 여 hello **새로 AzureRmWebApp** cmdlet.

다음은 hello 다른 매개 변수:

* **이름**: hello 웹 앱에 대 한 이름입니다.
* **AppServicePlan**: toohost hello 웹 응용 프로그램을 사용 하는 hello 서비스 계획에 대 한 이름을 지정 합니다.
* **ResourceGroupName**: hello 앱 서비스 계획을 호스팅하는 리소스 그룹입니다.
* **위치**: 웹 앱 위치의 hello 합니다.

예제 toouse이이 cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>App Service Environment에서 웹앱 만들기
앱 서비스 환경 (ASE)에서 웹 앱 toocreate 합니다. 사용 하 여 hello 동일 **새로 AzureRmWebApp** 명령에 추가 매개 변수 toospecify hello ASE 이름 및 hello ASE에 속하는 hello 리소스 그룹 이름입니다.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

앱 서비스 환경을 검사 하는 방법에 대 한 자세한 toolearn [소개 tooApp 서비스 환경](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>기존 웹앱 삭제
toodelete hello를 사용할 수는 기존 웹 응용 프로그램 **제거 AzureRmWebApp** cmdlet toospecify hello hello 웹 응용 프로그램의 이름과 hello 리소스 그룹 이름이 필요 합니다.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>기존 웹앱 나열
toolist hello 기존 웹 응용 프로그램을 사용 하 여 hello **Get AzureRmWebApp** cmdlet.

toolist 구독 아래의 모든 웹 앱을 사용 합니다.

    Get-AzureRmWebApp

toolist 특정 리소스 그룹 아래의 모든 웹 앱을 사용 합니다.

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget 특정 웹 앱을 사용 합니다.

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>기존 웹앱 구성
toochange hello 설정 및 기존 웹 응용 프로그램에 대 한 구성을 사용 하 여 hello **집합 AzureRmWebApp** cmdlet. 매개 변수 전체 목록을 확인 hello [Cmdlet 참조 링크](https://msdn.microsoft.com/library/mt652487.aspx)

이 cmdlet toochange 연결 문자열을 사용 하는 예 (1):

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

예 (2): 앱 설정 추가 또는 변경

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


예 (3): 64 비트 모드에서 웹 앱 toorun hello 설정

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>기존 웹 앱의 hello 상태 변경
#### <a name="restart-a-web-app"></a>웹앱 다시 시작
웹 앱 toorestart hello 웹 앱의 hello 이름과 리소스 그룹을 지정 해야 합니다.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>웹앱 중지
웹 앱 toostop hello 웹 앱의 hello 이름과 리소스 그룹을 지정 해야 합니다.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>웹앱 시작
웹 앱 toostart hello 웹 앱의 hello 이름과 리소스 그룹을 지정 해야 합니다.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>웹앱 게시 프로필 관리
각 웹 응용 프로그램에 사용 되는 toopublish 일 수 있는 게시 프로필 앱, 게시 프로필에 몇 가지 작업을 실행할 수 있습니다.

#### <a name="get-publishing-profile"></a>게시 프로필 가져오기
tooget hello를 사용 하 여 웹 응용 프로그램에 대 한 프로필 게시:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

이 명령은 hello 프로필 toohello 명령줄도 게시 프로필 tooa 텍스트 파일을 게시 하는 hello 출력에 표시 합니다.

#### <a name="reset-publishing-profile"></a>게시 프로필 다시 설정
tooreset 둘 다 hello를 사용 하 여 웹 응용 프로그램에 대 한 FTP 및 웹 배포 게시 암호:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>웹앱 인증서 관리
toolearn toomanage 응용 프로그램 인증서를 웹 하는 방법에 대 한 참조 [PowerShell을 사용 하 여 SSL 인증서 바인딩](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>다음 단계
* Azure 리소스 관리자 PowerShell 지원에 대 한 toolearn 참조 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와 함께 합니다.](../powershell-azure-resource-manager.md)
* 앱 서비스 환경에 대 한 toolearn 참조 [소개 tooApp 서비스 환경입니다.](app-service-app-service-environment-intro.md)
* PowerShell을 사용 하는 응용 프로그램 서비스 SSL 인증서를 관리 하는 방법에 대 한 toolearn 참조 [PowerShell을 사용 하 여 SSL 인증서 바인딩.](app-service-web-app-powershell-ssl-binding.md)
* Azure 웹 앱에 대 한 Azure 리소스 관리자 기반 PowerShell cmdlet의 전체 목록 hello에 대 한 toolearn 참조 [웹 앱 Azure 리소스 관리자 PowerShell Cmdlet의 Azure Cmdlet 참조 합니다.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn CLI를 사용 하 여 응용 프로그램 서비스를 관리 하는 방법에 대 한 참조 [Using Azure Resource Manager-Based XPlat CLI Azure 웹 앱에 대 한 합니다.](app-service-web-app-azure-resource-manager-xplat-cli.md)

