---
title: "응용 프로그램 업그레이드 항목 aaaAdvanced | Microsoft Docs"
description: "이 문서에서는 tooupgrading 서비스 패브릭 응용 프로그램 관련 된 몇 가지 고급 항목에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>서비스 패브릭 응용 프로그램 업그레이드: 고급 항목
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>응용 프로그램을 업그레이드하는 동안 서비스 추가 또는 제거
새 서비스는 이미 배포 되 고 게시 tooan 응용 프로그램 업그레이드로 추가 되 면 hello 새 서비스는 추가 된 toohello 배포 응용 프로그램.  이러한 업그레이드 이미 hello 응용 프로그램의 일부인 hello 서비스의에 영향을 주지 않습니다. 그러나 hello 새 서비스 toobe 활성화에 대 한 추가 된 hello 서비스의 인스턴스 시작 해야 합니다 (hello를 사용 하 여 `New-ServiceFabricService` cmdlet).

업그레이드의 일부로 응용 프로그램에서 서비스를 제거할 수도 있습니다. 하지만 Hello 업그레이드를 계속 하기 전에 hello 삭제 하려는 서비스의 모든 현재 인스턴스를 중지 해야 (hello를 사용 하 여 `Remove-ServiceFabricService` cmdlet).

## <a name="manual-upgrade-mode"></a>수동 업그레이드 모드
> [!NOTE]
> 실패 한 또는 일시 중단 된 업그레이드에 대 한 hello 모니터링 되지 않는 수동 모드를 고려할 수 있습니다. hello 모니터링된 모드는 hello 권장 서비스 패브릭 응용 프로그램에 대 한 업그레이드 모드입니다.
>
>

Azure 서비스 패브릭 toosupport 개발 및 프로덕션 클러스터 업그레이드는 여러 모드를 제공합니다. 선택한 배포 옵션은 환경마다 다를 수 있습니다.

응용 프로그램을 모니터링 하는 hello 롤링 업그레이드는 hello 프로덕션 환경에서 가장 일반적인 업그레이드 toouse hello 합니다. Hello 업그레이드 정책이 지정 된, 서비스 패브릭 hello 업그레이드 진행 전에 hello 응용 프로그램 정상 인지 확인 합니다.

 응용 프로그램 관리자에 게 hello 수동 롤링 응용 프로그램 업그레이드 모드 toohave 완전히 제어 hello 업그레이드 진행률 hello 통해 다양 한 업그레이드 도메인을 사용할 수 있습니다. 이 모드는 사용자 정의 된 또는 복잡 한 상태 평가 정책의 필요한 경우 또는 기본이 아닌 업그레이드가 발생 하는 경우에 유용 (예를 들어 hello 응용 프로그램은 이미 데이터가 손실).

마지막으로, hello 자동화 된 롤링 응용 프로그램 업그레이드는 서비스를 개발 하는 동안 빠른 반복 주기 개발 또는 테스트 환경 tooprovide 하는 데 유용 합니다.

## <a name="change-toomanual-upgrade-mode"></a>Toomanual 업그레이드 모드 변경
**수동**-hello 현재 UD 및 변경 hello에서 중지 hello 응용 프로그램 업그레이드 모드 tooUnmonitored 수동 업그레이드 합니다. hello 관리자가 toomanually 호출 **MoveNextApplicationUpgradeDomainAsync** tooproceed hello로 업그레이드 하거나 새 업그레이드를 시작 하 여 rollback을 트리거합니다. Hello 업그레이드 hello 수동 모드를 시작 되 면 상태로 유지 hello 수동 모드에서 새 업그레이드를 시작할 때까지 합니다. hello **GetApplicationUpgradeProgressAsync** 명령이 반환 패브릭\_응용 프로그램\_업그레이드\_상태\_롤링\_앞으로\_보류 중입니다.

## <a name="upgrade-with-a-diff-package"></a>diff 패키지로 업그레이드
완전한 자체 포함 응용 프로그램 패키지로 프로비전하여 서비스 패브릭 응용 프로그램을 업그레이드할 수 있습니다. 응용 프로그램 에서만 업데이트 hello 응용 프로그램 파일을 포함 하는 차이 패키지를 사용 하 여 업그레이드할 수 있습니다, 그리고 hello hello 서비스 매니페스트 파일 응용 프로그램 매니페스트를 업데이트 합니다.

전체 응용 프로그램 패키지를 모든 hello 파일 필요한 toostart를 포함 하 고 서비스 패브릭 응용 프로그램을 실행 합니다. Diff 패키지 hello 마지막 프로 비전 하 고 hello 현재 업그레이드 중 변경 된 hello 파일만 포함 및 hello 전체 응용 프로그램 매니페스트 및 hello 서비스 매니페스트 파일입니다. 모든 참조 hello 응용 프로그램 매니페스트 또는 hello 빌드 레이아웃에서 찾을 수 없는 서비스 매니페스트 hello 이미지 저장소에서 검색 됩니다.

전체 응용 프로그램 패키지는 hello 처음 설치 하는 응용 프로그램 toohello 클러스터에 필요 합니다. 후속 업데이트는 전체 응용 프로그램 패키지도 가능하고 diff 패키지도 가능합니다.

다음과 같은 경우에는 diff 패키지를 사용하는 것이 좋습니다.

* 여러 서비스 매니페스트 파일 및/또는 여러 코드 패키지, config 패키지 또는 데이터 패키지를 참조하는 대형 응용 프로그램 패키지가 있는 경우에는 diff 패키지가 좋습니다.
* 응용 프로그램 빌드 프로세스에서 직접 hello 빌드 레이아웃을 생성 하는 배포 시스템을 사용 하는 경우 diff 패키지를 사용 하는 것이 좋습니다. 이 경우 hello 코드가 변경 되지 않은 경우에 새로 빌드된 어셈블리는 서로 다른 체크섬을 가져옵니다. 전체 응용 프로그램 패키지를 사용 하 여 있습니다 tooupdate hello에 버전 모든 코드 패키지가 필요 합니다. Diff 패키지를 사용 하 여 있습니다만 변경 하는 hello 파일 및 hello 매니페스트 파일 제공 hello 버전이 변경 되었습니다.

Visual Studio를 사용 하 여 응용 프로그램 업그레이드 되 면 hello diff 패키지 자동으로 게시 됩니다. toocreate diff 패키지 응용 프로그램 매니페스트를 수동으로 hello 및 hello 서비스 매니페스트를 업데이트 해야 하지만 패키지에만 변경 하는 hello hello 최종 응용 프로그램 패키지에 포함 되어야 합니다.

예를 들어 응용 프로그램 (버전 번호가 이해 하기 쉽도록 제공)를 수행 하는 hello로 시작 하겠습니다.

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

이제 tooupdate만 hello 코드 패키지 service1의 PowerShell을 사용 하는 차이 패키지를 사용 한다고 가정 합니다. 이제 업데이트 된 응용 프로그램에 다음 폴더 구조는 hello에:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

이 경우 hello 응용 프로그램 매니페스트 too2.0.0 및 service1 tooreflect hello 코드 패키지 업데이트에 대 한 서비스 매니페스트 hello 업데이트합니다. 응용 프로그램 패키지에 대 한 hello 폴더 구조를 다음 hello 갖기:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

응용 프로그램 업그레이드를 학습 하 여 호환 되도록 어떻게 toouse [데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)합니다.

toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)합니다.
