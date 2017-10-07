---
title: "aaaHow tooupdate 클라우드 서비스 | Microsoft Docs"
description: "Azure에서 tooupdate 클라우드 서비스 하는 방법에 대해 알아봅니다. 클라우드 서비스에 대 한 업데이트 tooensure 가용성을 진행 하는 방법에 대해 알아봅니다."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>어떻게 tooupdate 클라우드 서비스

해당 역할 및 게스트 OS를 포함한 클라우드 서비스 업데이트는 3단계 프로세스입니다. 첫째, hello 이진 파일 및 새 hello에 대 한 구성 파일에 대 한 클라우드 서비스 또는 OS 버전을 업로드 해야 합니다. 그런 다음 Azure hello 새 클라우드 서비스 버전의 hello 요구 사항에 따라 hello 클라우드 서비스에 대 한 계산 및 네트워크 리소스를 예약 합니다. 마지막으로, Azure 하 여 가용성을 유지 하면서 롤링 업그레이드 tooincrementally 업데이트 hello 테 넌 트 toohello 새 버전 또는 게스트 OS 수행 합니다. 이 마지막 단계 – hello 롤링 업그레이드의 hello 세부 정보에 설명 합니다.

## <a name="update-an-azure-service"></a>Azure 서비스 업데이트
Azure는 업그레이드 도메인(UD)이라는 논리적 그룹으로 역할 인스턴스를 구성합니다. 업그레이드 도메인(UD)은 그룹으로 업데이트되는 역할 인스턴스의 논리적 집합입니다.  다른 Ud toocontinue 트래픽 처리에 인스턴스를 허용 하 여 한 번에 하나의 UD를 서비스 하는 클라우드는 azure 업데이트 합니다.

hello 기본 업그레이드 도메인 수는 5입니다. Hello 서비스 정의 파일 (.csdef)에 hello upgradeDomainCount 특성을 포함 하 여 서로 다른 업그레이드 도메인 수를 지정할 수 있습니다. Hello upgradeDomainCount 특성에 대 한 자세한 내용은 참조 [WebRole 스키마](https://msdn.microsoft.com/library/azure/gg557553.aspx) 또는 [WorkerRole 스키마](https://msdn.microsoft.com/library/azure/gg557552.aspx)합니다.

서비스에 하나 이상의 역할의 내부 업데이트를 수행 하는 경우 Azure toohello 업그레이드 도메인 toowhich 속하는지에 따라 역할 인스턴스의 조합을 업데이트 합니다. Azure 업데이트 중지 상태로, 업데이트, 지정 된 업그레이드 도메인-hello 인스턴스를 모두 다시 온라인 hello 다음 도메인으로 이동 합니다. 현재 hello에서 실행 되는 유일한 hello 인스턴스를 중지 하 여 업그레이드 도메인에서는 Azure와 hello 서비스가 실행 되는 가능한 한 최소한 영향 toohello 업데이트가 발생 하는지 합니다. 자세한 내용은 참조 [hello 업데이트를 처리할 방법을](#howanupgradeproceeds) 이 문서의 뒷부분에 나오는 합니다.

> [!NOTE]
> Hello 용어 동안 **업데이트** 및 **업그레이드** Azure hello 컨텍스트에서 의미가 약간 다르지만, hello 프로세스와이 문서에 hello 기능 설명은 같은 의미로 사용 될 수 있습니다.
>
>

서비스는 해당 역할 업데이트 toobe 내부 가동 중지 시간 없이 대 한 역할의 인스턴스가 둘 이상 정의 해야 합니다. Hello 서비스 역할의 인스턴스가 하나만으로 구성 된 경우 서비스에 사용할 수 없게 됩니다 hello 내부 업데이트가 끝날 때까지 합니다.

이 항목에서는 hello 다음 Azure 업데이트에 대 한 정보를 다룹니다.

* [업데이트 중 허용된 서비스 변경 내용](#AllowedChanges)
* [업그레이드 진행 방법](#howanupgradeproceeds)
* [업데이트 롤백](#RollbackofanUpdate)
* [진행 중인 배포에 여러 변경 작업 시작](#multiplemutatingoperations)
* [업그레이드 도메인 간 역할의 배포](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>업데이트 중 허용된 서비스 변경 내용
hello 아래 표에 나와 hello 허용 된 변경 내용을 tooa 서비스 업데이트 하는 동안.

| Toohosting, 서비스 및 역할을 허용 하는 변경 | 전체 업데이트 | 스테이징(VIP 교체) | 삭제 및 다시 배포 |
| --- | --- | --- | --- |
| 운영 체제 버전 |예 |예 |예 |
| .NET 신뢰 수준 |예 |예 |예 |
| 가상 컴퓨터 크기<sup>1</sup> |예<sup>2</sup> |예 |예 |
| 로컬 저장소 설정 |증가만<sup>2</sup> |예 |예 |
| 서비스에서 역할 추가 또는 제거 |예 |예 |예 |
| 특정 역할의 인스턴스 수 |예 |예 |예 |
| 서비스에 대한 끝점의 개수 또는 유형 |예<sup>2</sup> |아니요 |예 |
| 구성 설정의 이름 및 값 |예 |예 |예 |
| 구성 설정의 값(이름 제외) |예 |예 |예 |
| 새 인증서 추가 |예 |예 |예 |
| 기존 인증서 변경 |예 |예 |예 |
| 새 코드 배포 |예 |예 |예 |

<sup>1</sup> 크기 변경 hello 클라우드 서비스에 대해 사용할 수 있는 크기의 toohello 하위 집합을 제한 합니다.

<sup>2</sup> Azure SDK 1.5 이상 버전이 필요합니다.

> [!WARNING]
> Hello 가상 컴퓨터 크기를 변경 하면 로컬 데이터가 소멸 됩니다.
>
>

다음 항목 hello 업데이트 하는 동안 지원 되지 않습니다.

* 역할의 hello 이름을 변경 합니다. 제거 하 고 hello 새 이름으로 hello 역할을 추가 합니다.
* Hello 업그레이드 도메인 수의 변경입니다.
* Hello 로컬 리소스 감소 hello 크기입니다.

로컬 리소스의 hello 크기 줄이기와 같은 tooyour 서비스의 정의 다른 업데이트 하는 경우 대신 VIP swap 업데이트를 수행 해야 합니다. 자세한 내용은 [교환 배포](https://msdn.microsoft.com/library/azure/ee460814.aspx)를 참조하세요.

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>업그레이드 진행 방법
Tooupdate 사용할지 결정할 수의 모든 서비스에 대 한 hello 역할 또는 hello 서비스에서 단일 역할입니다. 두 경우 모두 업그레이드 하는 중 및 toohello 첫 번째 업그레이드 도메인에 속해 있는 각 역할의 모든 인스턴스는 중지, 업그레이드 및 다시 온라인 상태로 전환 합니다. 다시 온라인 상태로 전환 된 hello hello 두 번째 업그레이드 도메인의 인스턴스 중지, 업그레이드 되며 다시 온라인 상태로 만듭니다. 클라우드 서비스는 한 번에 하나의 업그레이드를 활성화할 수 있습니다. hello 업그레이드는 hello hello 클라우드 서비스의 최신 버전에 대해 수행 됩니다.

hello 다음 다이어그램에서는 모든 hello 역할 hello 서비스에서 업그레이드 하는 경우 hello 업그레이드를 처리할 방법을 수행 합니다.

![서비스 업그레이드](media/cloud-services-update-azure-service/IC345879.png "서비스 업그레이드")

다음 다이어그램에서는 단일 역할만 업그레이드 하는 경우 hello 업데이트를 처리할 방법을 보여 줍니다.

![역할 업그레이드](media/cloud-services-update-azure-service/IC345880.png "역할 업그레이드")  

자동 업데이트를 사용 하는 동안 Azure 패브릭 컨트롤러 hello 주기적으로 평가 hello 클라우드 서비스 toodetermine의 hello 상태 안전 toowalk hello 다음 UD 됩니다. 이 상태 평가에 역할 단위로 수행 되 고 hello 최신 버전 (즉, 워크 이미 있는 Ud에서 인스턴스)의 인스턴스만 고려 합니다. 각 역할에 대해 최소 수의 역할 인스턴스가 만족스러운 터미널 상태로 수행됐는지 확인합니다.

### <a name="role-instance-start-timeout"></a>역할 인스턴스 시작 시간 제한
hello 패브릭 컨트롤러는 각 역할 인스턴스 tooreach 시작 됨 상태에 대 일 분 동안 대기 합니다. Hello 시간 제한 기간이 경과 하면 hello 패브릭 컨트롤러 toohello 다음 역할 인스턴스를 순환 계속 됩니다.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>클라우드 서비스 업그레이드 하는 동안 영향 toodrive 데이터

단일 인스턴스 toomultiple 인스턴스에서 서비스를 업그레이드 하는 경우 Azure 서비스 업그레이드 toohello 방식으로 인해 hello 업그레이드가 수행 될 동안 서비스 이동 됩니다. hello 서비스 수준 계약 서비스 가용성을 보장에 둘 이상의 인스턴스를 함께 배포 되는 tooservices만 적용 됩니다. hello 다음 목록은 각 Azure 서비스 업그레이드 시나리오에 따라 각 드라이브에 hello 데이터 영향:

|시나리오|C 드라이브|D 드라이브|E 드라이브|
|--------|-------|-------|-------|
|VM 재부팅|유지됨|유지됨|유지됨|
|포털 재부팅|유지됨|유지됨|제거됨|
|포털 이미지로 다시 설치|유지됨|제거됨|제거됨|
|전체 업그레이드|유지됨|유지됨|제거됨|
|노드 마이그레이션:|제거됨|제거됨|제거됨|

Note, 목록 위의 hello, hello e: 드라이브 hello 역할 루트 드라이브를 나타내고 하드 코딩 되지 않아야 합니다. 대신, hello를 사용 하 여 **% RoleRoot %** 환경 변수 toorepresent hello 드라이브입니다.

단일 인스턴스 서비스를 업그레이드할 때 toominimize hello 가동 중지 시간 새 다중 인스턴스 서비스 toohello 준비 서버를 배포 및 VIP 교체를 수행 합니다.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>업데이트 롤백
Azure는 hello Azure 패브릭 컨트롤러 하 여 hello 초기 업데이트 요청이 수락 되는 서비스에서 추가 작업을 시작할 수 있도록 하 여 업데이트 하는 동안 서비스를 관리에 유연성을 제공 합니다. 롤백을 수행할 수 있습니다만 업데이트 (구성 변경) 또는 업그레이드가 hello **진행에서** hello 배포의 상태입니다. 업데이트 또는 업그레이드 아직 새 버전을 업데이트 된 toohello hello 서비스의 인스턴스가 두 개 이상으로 진행 중인 toobe 간주 됩니다. tootest 롤백이 허용 되는지 여부를 확인 하 여 반환 된 hello RollbackAllowed 플래그의 hello 값 [배포 가져오기](https://msdn.microsoft.com/library/azure/ee460804.aspx) 및 [클라우드 서비스 속성 가져오기](https://msdn.microsoft.com/library/azure/ee460806.aspx) 작업 tootrue 설정 됩니다.

> [!NOTE]
> 만 의미 toocall 롤백에 사용 하면는 **내부** 업데이트 또는 업그레이드를 다른 서비스의 전체 하나의 실행 중인 인스턴스를 대체 VIP 스왑 업그레이드를 포함 하기 때문입니다.
>
>

진행 중인 업데이트 롤백 hello hello 배포에 영향을 뒤에 있습니다.

* 역할 인스턴스는 업데이트 또는 업그레이드 된 toohello 새 버전을 아직 되지 않은 업데이트 되거나 이러한 인스턴스는 이미 실행 되 고 hello 대상 버전의 hello 서비스 업그레이드 되지 않습니다.
* 모든 역할 인스턴스가 이미 업데이트는 또는 업그레이드 된 toohello 새 버전의 hello 서비스 패키지 (\*.cspkg) 파일 또는 hello 서비스 구성 (\*.cscfg) 파일 (또는 두 파일)은 되돌린된 toohello 업그레이드 이전 버전의 이러한 파일입니다.

이 기능적으로 제공한 hello 같은 기능:

* hello [롤백 업데이트 또는 업그레이드](https://msdn.microsoft.com/library/azure/hh403977.aspx) 구성 업데이트에서 호출 될 수 있는 작업 (호출에 의해 트리거됨 [배포 구성 변경](https://msdn.microsoft.com/library/azure/ee460809.aspx)) 또는 업그레이드 (호출에 의해 트리거됨 [ 업그레이드 배포](https://msdn.microsoft.com/library/azure/ee460793.aspx)) hello 서비스 중인 인스턴스를 하나 이상으로 toohello 새 버전을 업데이트는 아직 되지 않았습니다.
* hello의 hello 응답 본문의 일부로 반환 되는 잠금 요소와 hello RollbackAllowed 요소 hello [배포 가져오기](https://msdn.microsoft.com/library/azure/ee460804.aspx) 및 [클라우드 서비스 속성 가져오기](https://msdn.microsoft.com/library/azure/ee460806.aspx) 작업:

  1. hello 잠금 요소가 있습니다 toodetect을 때 지정된 된 배포에서 변경 작업을 호출할 수 있습니다.
  2. hello RollbackAllowed 요소를 있습니다 때 hello toodetect [업데이트 또는 업그레이드 롤백](https://msdn.microsoft.com/library/azure/hh403977.aspx) 지정된 된 배포에서 작업을 호출할 수 있습니다.

  순서 tooperform 롤백에에서 없는 toocheck hello Locked 및 RollbackAllowed 요소 hello 모두 합니다. 그 RollbackAllowed tootrue 설정 되어 있는지 tooconfirm을 충분 합니다. 이러한 요소는도 hello 요청 헤더를 사용 하 여 두이 메서드는 호출 하는 경우에 반환 됩니다 "x ms 버전: 2011-10-01" 이상 버전입니다. 버전 관리 헤더에 대한 자세한 내용은 [서비스 관리 버전 관리](https://msdn.microsoft.com/library/azure/gg592580.aspx)를 참조하세요.

업데이트 또는 업그레이드의 롤백이 지원되지 않는 경우는 다음과 같습니다.

* -로컬 리소스 감소 hello 업데이트 증가 hello 로컬 리소스는 역할에 대 한 hello Azure 플랫폼에서 허용 하지 않습니다 롤백 합니다.
* 할당량 한도-전보다 hello 업데이트를 축소 작업을 더 이상 수 없으면 toocomplete hello 롤백 작업에 대 한 충분 한의 계산 할당량. 각 Azure 구독에 연결 된 hello toothat 구독에 속하는 모든 호스팅된 서비스에서 사용할 수 있는 코어의 최대 수를 지정 하는 할당량입니다. 특정 업데이트의 롤백 수행으로 구독이 할당량을 초과하게 되는 경우 해당 롤백을 사용할 수 없습니다.
* 경합 상태-초기 업데이트가 hello 완료, 롤백 수는 없습니다.

업데이트 롤백 hello 유용할 수의 예로 hello를 사용 하는 경우 [업그레이드 배포](https://msdn.microsoft.com/library/azure/ee460793.aspx) 수동 모드 toocontrol hello 속도 주요 내부 업그레이드 tooyour Azure 호스팅 서비스에서 작업에 전달 합니다.

Hello 업그레이드의 롤아웃 hello 동안 호출 [업그레이드 배포](https://msdn.microsoft.com/library/azure/ee460793.aspx) 수동 모드에서 toowalk 업그레이드 도메인을 시작 합니다. Hello를 호출할 수 있으면 어느 시점 부터는 hello 업그레이드를 모니터링 하면서 hello 첫 번째 업그레이드 도메인 살펴보면의 일부 역할 인스턴스가 응답 하지 않는 했으면, [업데이트 또는 업그레이드 롤백](https://msdn.microsoft.com/library/azure/hh403977.aspx) hello 배포에 대 한 작업이 있는 아직 업그레이드 되지에 그대로 hello 인스턴스 두고 이었던 롤백 인스턴스 업그레이드 toohello 이전 서비스 패키지 및 구성 합니다.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>진행 중인 배포에 여러 변경 작업 시작
일부 경우에 tooinitiate 진행 중인 배포에서 여러 동시 변경 작업을 할 수 있습니다. 예를 들어 서비스 업데이트를 수행할 수 있습니다 하 고, 해당 업데이트는 여러 서비스 롤아웃 되는 동안 toomake 일부 변경 5d; 예: tooroll 업데이트 다시 hello, 다른 업데이트를 적용 하거나 삭제할 수 hello 배포 합니다. 필요할 수 있습니다 하는 경우 서비스 업그레이드 하는 업그레이드 된 역할 인스턴스 toorepeatedly 손상 시키는 버그가 있는 코드를 포함 하는 경우입니다. 이 경우 Azure 패브릭 컨트롤러 hello 수 toomake 계속 적용할 하 여 hello 업그레이드 도메인에 인스턴스 수가 부족 비정상 상태는 업그레이드 되지 않습니다. 이 상태는 참조 된 tooas는 *배포 중단*합니다. Hello 업데이트 롤백 또는 hello 하나 실패 맨 위에 새 업데이트를 적용 하 여 hello 배포 중단을 해결할 수 있습니다.

Hello 초기 요청 tooupdate 또는 업그레이드 hello 서비스는 hello Azure 패브릭 컨트롤러에서 받은, 되 면 후속 변경 작업을 시작할 수 있습니다. 즉, 않아도 toowait 초기 작업 toocomplete hello에 대 한 다른 변경 작업을 시작 하기 전에.

Hello 첫 번째 업데이트가 진행 중일 동안 두 번째 업데이트 작업을 시작 하는 비슷한 toohello 롤백 작업이 수행 합니다. Hello 두 번째 업데이트 자동 모드에 있으면 hello 첫 번째 업그레이드 도메인을 즉시 업그레이드 됩니다, 그리고 hello에 오프 라인 상태로 유지 하는 여러 업그레이드 도메인의 tooinstances 라인이 같은 지정 시간입니다.

hello 변경 작업은 다음과 같습니다: [배포 구성 변경](https://msdn.microsoft.com/library/azure/ee460809.aspx), [업그레이드 배포](https://msdn.microsoft.com/library/azure/ee460793.aspx), [업데이트 배포 상태](https://msdn.microsoft.com/library/azure/ee460808.aspx), [삭제 배포](https://msdn.microsoft.com/library/azure/ee460815.aspx), 및 [업데이트 또는 업그레이드 롤백](https://msdn.microsoft.com/library/azure/hh403977.aspx)합니다.

두 개의 작업 [배포 가져오기](https://msdn.microsoft.com/library/azure/ee460804.aspx) 및 [클라우드 서비스 속성 가져오기](https://msdn.microsoft.com/library/azure/ee460806.aspx), 지정된 된 배포에서 변경 작업을 호출할 수 있는지 여부를 검사 toodetermine 될 수 있는 hello 잠금 플래그를 반환 합니다.

순서 toocall hello 버전에서 이러한 메서드의 hello 잠금 플래그를 반환 하는 설정 해야 요청 헤더가 너무 "x ms 버전: 2011-10-01" 이상. 버전 관리 헤더에 대한 자세한 내용은 [서비스 관리 버전 관리](https://msdn.microsoft.com/library/azure/gg592580.aspx)를 참조하세요.

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>업그레이드 도메인 간 역할의 배포
Azure는 역할의 인스턴스를 여러 hello 서비스 정의 (.csdef) 파일의 일부로 구성 될 수 있는 업그레이드 도메인 수에 대해 균등 하 게 배포 합니다. hello 최대 업그레이드 도메인 수는 20 개이고, hello 기본값은 5입니다. 어떻게 toomodify hello 서비스 정의 파일에 대 한 자세한 내용은 참조 [Azure Service 정의 스키마 (.csdef 파일)](cloud-services-model-and-package.md#csdef)합니다.

예를 들어 역할에 10개의 인스턴스가 있는 경우 기본적으로 각 업그레이드 도메인에는 두 개의 인스턴스가 포함됩니다. 사용자의 역할 인스턴스가 14 세 인스턴스를 포함할 hello 업그레이드 도메인의 4 개는 다음 및 두 개의 도메인에 있습니다.

업그레이드 도메인 0 기반 인덱스로 식별 됩니다: hello 첫 번째 업그레이드 도메인은 0, ID 및 hello 두 번째 업그레이드 도메인은 ID가 1, 및 기타 등등.

hello 다음 다이어그램에서는 두 개의 업그레이드 도메인을 정의 하는 hello 서비스는 서비스를 두 개의 역할을 포함 하는 보다 어떻게 분포 되어 합니다. hello 웹 역할 인스턴스가 8 개인 및 hello 작업자 역할 인스턴스 9 개 hello 서비스가 실행 되 고 있습니다.

![업그레이드 도메인 배포](media/cloud-services-update-azure-service/IC345533.png "업그레이드 도메인 배포")

> [!NOTE]
> Azure는 업그레이드 도메인에 인스턴스가 할당되는 방식을 제어합니다. 가능한 toospecify 인스턴스 toowhich 도메인에 할당 되는 없습니다.
>
>

## <a name="next-steps"></a>다음 단계
[TooManage 클라우드 서비스 하는 방법](cloud-services-how-to-manage.md)  
[TooMonitor 클라우드 서비스 하는 방법](cloud-services-how-to-monitor.md)  
[TooConfigure 클라우드 서비스 하는 방법](cloud-services-how-to-configure.md)  
