---
title: "Azure 앱 서비스의 웹 앱에 대 한 환경 준비를 aaaSet | Microsoft Docs"
description: "Toouse Azure 앱 서비스에서 웹 앱에 대 한 게시를 준비 하는 방법에 대해 알아봅니다."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a>Azure App Service에서 스테이징 환경 설정
<a name="Overview"></a>

배포 하는 경우 웹 앱, Linux, 백 엔드 모바일 및 API 앱에 웹 앱 너무[앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714), hello에서 실행 하는 경우 기본 프로덕션 슬롯만 hello 대신 tooa 별도 배포 슬롯을 배포할 수 있습니다 **표준**또는 **프리미엄** 앱 서비스 계획 모드입니다. 배포 슬롯은 실제로 고유한 호스트 이름이 있는 라이브 앱입니다. 응용 프로그램 콘텐츠 및 구성 요소는 hello 프로덕션 슬롯을 포함 하 여 두 배포 슬롯 간에 교환할 수 있습니다. 배포 응용 프로그램 tooa 배포 슬롯을 사용 하 여 hello 이점을 뒤에 있습니다.

* Hello 프로덕션 슬롯으로 교환 하기 전에 스테이징 배포 슬롯에서 응용 프로그램은 변경을 확인할 수 있습니다.
* 앱 tooa 슬롯을 먼저 배포 하 고 프로덕션으로 교환 하기 전에 프로덕션으로 교환 하 hello 슬롯의 모든 인스턴스 준비 됩니다 되도록 합니다. 따라서 앱을 배포할 때 가동 중지가 발생하지 않습니다. hello 트래픽 리디렉션이 원활 하 게, 고 교환 작업으로 요청 없음이 삭제 됩니다. 사전 교환 유효성 검사가 필요하지 않은 경우 [자동 교환](#Auto-Swap) 을 구성하여 이 전체 워크플로를 자동화할 수 있습니다.
* Hello 슬롯을 이전에 준비 된 앱과, 교환 후 프로덕션 응용 프로그램을 이전 하는 hello에 있습니다. Hello 프로덕션 슬롯으로 교환 된 hello 변경 하면 예상과 다른 경우 hello tooget "마지막 알려진된 좋은 사이트" 백업 하는 즉시 동일한 교체를 수행할 수 있습니다.

각 앱 서비스 계획 모드는 다양한 수의 배포 슬롯을 지원합니다. 슬롯 개수 hello 아웃 toofind 앱의 모드를 지원, 참조 [앱 서비스 가격 책정](https://azure.microsoft.com/pricing/details/app-service/)합니다.

* 응용 프로그램에 여러 슬롯, hello 모드를 변경할 수 없습니다.
* 프로덕션이 아닌 슬롯에 대해 크기 조정을 사용할 수 없습니다.
* 연결된 리소스 관리는 프로덕션이 아닌 슬롯에 대해 지원되지 않습니다. Hello에 [Azure 포털](http://go.microsoft.com/fwlink/?LinkId=529715) 만 hello 비-프로덕션 슬롯 tooa 다른 앱 서비스 계획 모드를 일시적으로 이동 하 여 프로덕션 슬롯에 영향을 줄이 방지할 수 있습니다. 해당 hello 비-프로덕션 슬롯 hello를 다시 공유 해야 하는 참고 hello 두 슬롯을 전환할 수 전에 hello 프로덕션 슬롯으로 동일한 모드입니다.

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a>배포 슬롯 추가
hello에서 hello 응용 프로그램을 실행 해야 **표준** 또는 **프리미엄** 다중 배포 슬롯이 있습니다 tooenable에 대 한 모드에서 순서입니다.

1. Hello에 [Azure 포털](https://portal.azure.com/), 응용 프로그램을 열고 [리소스 블레이드](../azure-resource-manager/resource-group-portal.md#manage-resources)합니다.
2. Hello 선택 **배포 슬롯** 클릭 한 다음 옵션을 **슬롯 추가**합니다.
   
    ![새 배포 슬롯 추가][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > Hello 앱에에서 없는 경우 이미 hello **표준** 또는 **프리미엄** 모드에서는 준비 된 게시를 사용 하기 위해 지원 되는 hello 모드를 나타내는 메시지가 표시 됩니다. 이 시점에서 hello 옵션 tooselect를 있는 **업그레이드** toohello 이동 **배율** 계속 하기 전에 응용 프로그램의 탭 합니다.
   > 
   > 
3. Hello에 **슬롯 추가** 블레이드에서 hello 슬롯에 이름을 지정 하 고 선택 여부 tooclone 앱 다른 기존 배포 슬롯에서에서 구성 합니다. Hello 확인 표시가 toocontinue를 클릭 합니다.
   
    ![구성 원본][ConfigurationSource1]
   
    hello 슬롯을 추가 하는 처음으로 두 가지 선택 사항: 프로덕션 환경에서 되지 않거나 전혀 hello 기본 슬롯에서 복제 구성 합니다.
    여러 슬롯을 만든 후에 프로덕션 환경에서 하나 hello 이외의 슬롯에서 수 tooclone 구성 됩니다.
   
    ![구성 원본][MultipleConfigurationSources]
4. 응용 프로그램의 리소스 블레이드 클릭 **배포 슬롯**, 배포 슬롯 tooopen 메트릭 및 다른 모든 앱에서와 마찬가지로 구성 집합과 해당 슬롯 리소스 블레이드를 차례로 클릭 합니다. hello 이름 hello 슬롯의 표시 되어 hello 블레이드 tooremind hello 위쪽에 배포 슬롯 hello 보려는 있습니다.
   
    ![배포 슬롯 제목][StagingTitle]
5. Hello 슬롯의 블레이드에서 hello 앱 URL을 클릭 합니다. 공지 hello 배포 슬롯에서 자체 호스트 이름을 있으며 라이브 앱 이기도 합니다. toolimit 공용 액세스 toohello 배포 슬롯 참조 [앱 서비스 웹 앱 블록 웹 액세스 toonon 프로덕션 배포 슬롯](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)합니다.

배포 슬롯을 만든 후 콘텐츠가 없습니다. 전혀 다른 저장소 또는 다른 리포지토리의 분기에서 슬롯 toohello 배포할 수 있습니다. 또한 hello 슬롯의 구성을 변경할 수 있습니다. 사용 하 여 hello 프로필 배포 자격 증명 또는 연결 된 콘텐츠 업데이트에 대 한 hello 배포 슬롯을 게시 합니다.  예를 들어, [git가 포함 된 슬롯 toothis 게시](app-service-deploy-local-git.md)합니다.

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a>배포 슬롯의 구성
다른 배포 슬롯에서에서 구성 복제 하면 복제 된 hello 구성을 편집할 수 있습니다. 또한 일부 구성 요소가 다른 구성 요소를 동일한 슬롯 교환 (특정 슬롯) 후 hello에 유지 하는 동안 스왑 (하지 특정 슬롯)에서 hello 콘텐츠를 수행 합니다. hello 다음 목록에서는 보여 hello 구성 슬롯을 전환할 때 변경 됩니다.

**교환된 설정**:

* 프레임워크 버전, 32/64비트, 웹 소켓과 같은 일반 설정
* 앱 설정 (구성 된 toostick tooa 슬롯 수 있음)
* 연결 문자열 (구성 된 toostick tooa 슬롯 수 있음)
* 처리기 매핑
* 모니터링 및 진단 설정
* WebJob 콘텐츠

**교환되지 않은 설정**:

* 게시 끝점
* 사용자 지정 도메인 이름
* SSL 인증서 및 바인딩
* 크기 조정 설정
* WebJob 스케줄러

응용 프로그램 설정 또는 연결 문자열 toostick tooa 슬롯 (교환 되지 않습니다) 액세스 hello tooconfigure **응용 프로그램 설정** 특정 슬롯 다음 선택 hello에 대 한 블레이드 **슬롯 설정을** hello에 대 한 상자 hello 슬롯 집중 해야 하는 구성 요소입니다. Note 해당 구성 요소를 것으로 표시 슬롯 특정 효과가 hello hello 앱과 연결 된 모든 hello 배포 슬롯 간에 하지 스왑 가능으로 해당 요소를 설정 합니다.

![슬롯 설정][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a>배포 슬롯 교환 
Hello에 배포 슬롯을 전환할 수 **개요** 또는 **배포 슬롯** 응용 프로그램의 리소스 블레이드의 보기입니다.

> [!IMPORTANT]
> 프로덕션 환경에 배포 슬롯에서 응용 프로그램을 교체 전에 toohave를 원하는 대로 모든 비 슬롯 특정 설정이 구성 되어 있는지 확인 hello 교환 대상은 합니다.
> 
> 

1. tooswap 배포 슬롯 클릭 hello **교체** hello 앱의 hello 명령 모음 또는 배포 슬롯의 hello 명령 모음에서 단추입니다.
   
    ![교환 단추][SwapButtonBar]

2. Hello 스왑 원본과 스왑 대상 제대로 설정 되어 있는지 확인 합니다. 일반적으로 hello 교환 대상은 프로덕션 슬롯 hello입니다. 클릭 **확인** toocomplete hello 작업 합니다. Hello 작업이 완료 되 면 hello 배포 슬롯 기능이 바뀌었는지 합니다.

    ![전체 교환](./media/web-sites-staged-publishing/SwapImmediately.png)

    Hello에 대 한 **미리 보기** 유형 swap, 참조 [미리 보기 (다중 단계 교체)](#Multi-Phase)합니다.  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a>미리 보기가 있는 교환(다단계 교환)

미리 보기가 있는 교환 또는 다단계 교환은 연결 문자열과 같은 슬롯 관련 구성 요소의 유효성 검사를 간소화합니다.
중요 한 작업을 위해 앱 hello toovalidate hello 프로덕션 슬롯의 구성을 적용 될 때 예상 대로 작동 하 고 이러한 유효성 검사를 수행 해야 *하기 전에* hello 앱이 프로덕션 환경으로 대체 합니다. 미리 보기가 있는 교환이 필요합니다.

> [!NOTE]
> 미리 보기가 있는 교환은 Linux의 웹앱에서 지원되지 않습니다.

Hello를 사용 하는 경우 **미리 보기가 교환이** 옵션 (참조 [배포 슬롯 교환](#Swap)), 다음 응용 프로그램 서비스는 hello:

- 유지 hello 대상 슬롯 변경 되지 않은 기존 작업 (예: 프로덕션) 해당 슬롯에 영향을 받지 않습니다.
- Hello 대상 슬롯 toohello 원본 슬롯 hello 슬롯의 연결 문자열, 앱 설정 등의 hello 구성 요소에 적용 됩니다.
- 이러한 앞에서 언급 한 구성 요소를 사용 하 여 hello 원본 슬롯에서 hello 작업자 프로세스를 다시 시작 합니다.
- Hello 교환을 완료 하는 경우: hello 대상 슬롯으로 이동 합니다. hello 사전 warmed 업 원본 슬롯입니다. hello 대상 슬롯 수동 스왑에서와 같이 hello 원본 슬롯으로 이동 합니다.
- Hello 스왑을 취소 하면: hello 원본 슬롯 toohello 원본 슬롯의 hello 구성 요소를 다시 적용 합니다.

정확 하 게 hello 앱 동작 방식을 hello 대상 슬롯의 구성을 사용 하 여 미리 볼 수 있습니다. 유효성 검사를 완료 한 후 hello 스왑 별도 단계에서를 완료 합니다. 이 단계는 hello 원본 슬롯이 hello 필요한 구성 준비 이미 되 고 클라이언트 가동 중지 시간이 발생 하지 것입니다는 또 다른 이점은 hello 했습니다.  

Hello 다단계 전환을 사용할 수 있는 Azure PowerShell cmdlet에 대 한 예제는 hello 배포 슬롯 섹션에 대 한 Azure PowerShell cmdlet에에서 포함 됩니다.

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a>자동 교환 구성
자동 스왑 간소화 DevOps 있는 시나리오는 toocontinuously hello 응용 프로그램의 최종 고객에 대 한 0 콜드 시작 및 중단 시간이 0을 사용 하 여 앱을 배포 합니다. 배포 슬롯에 대해 구성 된 자동 전환을 프로덕션 환경으로 내 코드 업데이트 toothat 슬롯을 누를 때마다 하는 경우 앱 서비스 됩니다 자동으로 교체 hello 앱 프로덕션 환경으로 해당 준비 된 후 이미 hello 슬롯에 합니다.

> [!IMPORTANT]
> 슬롯에 대 한 자동 교환를 설정한 경우 hello 슬롯 구성을 hello 대상 슬롯 (일반적으로 hello 프로덕션 슬롯)에 대 한으로 의도 된 hello 구성 정확 하 게 인지 확인 합니다.
> 
> 

> [!NOTE]
> 자동 교환은 Linux의 웹앱에서 지원되지 않습니다.

슬롯에 대한 자동 교환 구성은 쉽습니다. 아래의 hello 단계를 수행 합니다.

1. **배포 슬롯**에서 비프로덕션 슬롯을 선택하고 해당 슬롯의 리소스 블레이드에서 **응용 프로그램 설정**을 선택합니다.  
   
    ![][Autoswap1]
2. 선택 **에** 에 대 한 **자동 교환**선택, hello 원하는 대상 슬롯에 **자동 교환할 슬롯**를 클릭 하 고 **저장** hello 명령 모음에서 합니다. Hello 슬롯에 대 한 구성은 hello 대상 슬롯으로 의도 된 hello 구성 정확 하 게 있는지 확인 합니다.
   
    hello **알림** 탭 녹색 깜박입니다 **성공** hello 작업이 완료 되 면입니다.
   
    ![][Autoswap2]
   
   > [!NOTE]
   > tootest 자동 교환에 대 한 응용 프로그램을 먼저 선택의 비-프로덕션 대상 슬롯 **자동 교환 슬롯** toobecome hello 기능에 익숙한 합니다.  
   > 
   > 
3. 코드 푸시 toothat 배포 슬롯을 실행 합니다. 잠시 후 자동 전환할은 발생 하지 않으며 hello 업데이트 대상 슬롯의 URL에 반영 됩니다.

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a>교환 후 프로덕션 앱 toorollback
슬롯 교환 후 프로덕션에 오류가 있는지를 확인 하는 경우 hello 슬롯 백 tootheir 사전 스왑 상태 여 롤포워드할 즉시 hello 동일한 두 슬롯을 교환 합니다.

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a>교환하기 전에 사용자 지정 준비
일부 앱에는 사용자 지정 준비 작업이 필요할 수 있습니다. hello `applicationInitialization` web.config에 구성 요소 있습니다 toospecify 사용자 지정 초기화 작업 toobe 수행 전에 요청을 받을 수 있습니다. 이 사용자 지정 준비 toocomplete hello 스왑 작업이 대기 합니다. 샘플 web.config 조각은 다음과 같습니다.

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a>배포 슬롯을 toodelete
Hello 블레이드 열기 hello 배포 슬롯 블레이드 배포 슬롯에 대 한 클릭 **개요** (hello 기본 페이지)를 클릭 하 고 **삭제** hello 명령 모음에서 합니다.  

![배포 슬롯 삭제][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a>배포 슬롯용 Azure PowerShell cmdlet
Azure PowerShell은 cmdlet toomanage Azure 앱 서비스의 배포 슬롯을 관리 하기 위한 지원을 비롯 하 여 Windows PowerShell을 통해 Azure를 제공 하는 모듈입니다.

* 설치 하 고 Azure PowerShell을 구성 및 Azure 구독으로 Azure PowerShell 인증 정보를 참조 하십시오. [어떻게 tooinstall Microsoft Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.  

- - -
### <a name="create-a-web-app"></a>웹앱 만들기
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a>배포 슬롯 만들기
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a>검토 (다중 단계 교체) 교체를 시작 하 고 대상 슬롯 구성 toosource 슬롯 적용
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a>보류 중인 교환(검토가 있는 교환) 취소 및 원본 슬롯 구성 복원
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a>배포 슬롯 교환
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a>배포 슬롯 삭제
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a>배포 슬롯에 대한 Azure CLI(Azure 명령줄 인터페이스) 명령
앱 서비스 배포 슬롯을 관리 하기 위한 지원을 비롯 하 여 Azure를 사용 하기 위한 플랫폼 간 명령을 제공 하는 hello Azure CLI 합니다.

* 설치 및 구성에 대 한 지침 Azure CLI hello에 대 한 방법에 대 한 정보를 포함 한 tooconnect Azure CLI tooyour Azure 구독을 참조 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md)합니다.
* hello Azure CLI Azure 앱 서비스에 사용할 수 있는 toolist hello 명령 호출 `azure site -h`합니다.

> [!NOTE] 
> 배포 슬롯에 대한 [Azure CLI 2.0](https://github.com/Azure/azure-cli) 명령의 경우 [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot)을 참조하세요.

- - -
### <a name="azure-site-list"></a>azure site list
호출에 hello 앱 hello 현재 구독에 대 한 내용은 **azure 사이트 목록**와 같이, 다음 예제는 hello 합니다.

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a>azure site create
배포 슬롯을 toocreate 호출 **azure 사이트 만들기** 기존 앱의 hello 이름과 hello 다음 예제와 같이 hello 슬롯 toocreate의 hello 이름을 지정 합니다.

`azure site create webappslotstest --slot staging`

hello 새 슬롯을 사용 하 여 hello에 대 한 소스 제어 tooenable **-git** hello 다음 예제와 같이 옵션입니다.

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a>azure site swap
toomake hello 업데이트 된 배포 슬롯 hello 프로덕션 응용 프로그램, hello를 사용 하 여 **azure 사이트 스왑** 명령 tooperform hello 다음 예제와 같이 스왑 작업 합니다. hello 프로덕션 앱 모든 중단 시간을 발생 하지 않습니다 나 콜드 시작 될 예정입니다.

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a>azure site delete
배포 슬롯을 더 이상 toodelete 필요 hello를 사용 하 여 **azure 사이트 삭제** hello 다음 예제와 같이 명령입니다.

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> 작업에서 웹앱을 확인합니다. [앱 서비스 체험](https://azure.microsoft.com/try/app-service/) 에서는 신용 카드와 약정 없이 수명이 짧은 스타터 앱을 즉시 만들 수 있습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
[Azure 앱 서비스 웹 앱-웹 액세스 toonon 프로덕션 배포 슬롯을 차단](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[소개 tooApp linux 서비스](./app-service-linux-intro.md)
[Microsoft Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

