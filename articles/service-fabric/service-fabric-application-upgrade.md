---
title: "패브릭 응용 프로그램 업그레이드: aaaService | Microsoft Docs"
description: "이 문서에서는 소개 tooupgrading 업그레이드 모드 선택 및 성능의 상태 검사를 포함 하 여 서비스 패브릭 응용 프로그램을 제공 합니다."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>서비스 패브릭 응용 프로그램 업그레이드
Azure 서비스 패브릭 응용 프로그램은 서비스의 컬렉션입니다. 업그레이드 하는 동안 서비스 패브릭 비교 hello 새 [응용 프로그램 매니페스트](service-fabric-application-model.md#describe-an-application) hello 이전 버전으로 hello 응용 프로그램에서 서비스 업데이트 필요를 결정 합니다. 서비스 패브릭 hello 이전 버전의 hello 버전 번호를 가진 숫자 hello 서비스에서 매니페스트 hello 버전을 비교 합니다. 서비스가 변경되지 않으면 해당 서비스가 업그레이드되지 않습니다.

## <a name="rolling-upgrades-overview"></a>롤링 업그레이드 개요
응용 프로그램 롤링 업그레이드를 hello 업그레이드 단계로 수행 됩니다. 각 단계에서 hello 업그레이드가 적용된 tooa 업데이트 도메인 이라고 하는 hello 클러스터의 노드 하위 집합입니다. 결과적으로, hello 응용 프로그램 남아 hello 업그레이드 전체에서 사용할 수 있습니다. Hello 업그레이드 하는 동안 hello 클러스터 hello 이전 및 새 버전의 혼합을 포함할 수 있습니다.

이런 이유로 hello 두 버전 해야 앞 이나 뒤로 호환 됩니다. 호환 되지 않는, 경우 응용 프로그램 관리자에 게는 여러 단계 업그레이드 toomaintain 가용성을 준비 하는 일을 담당 합니다. Hello 첫 번째 단계를 여러 단계 업그레이드 중에 tooan hello 이전 버전과 호환 되는 hello 응용 프로그램의 중간 버전을 업그레이드 하 고 있습니다. hello 두 번째 단계는 hello 업데이트 이전 버전과 호환성을 중단 하지만 hello 중간 버전와 호환 되는 tooupgrade hello 최종 버전입니다.

업데이트 도메인은 hello 클러스터를 구성할 때 hello 클러스터 매니페스트에 지정 됩니다. 업데이트 도메인은 업데이트를 특정 순서로 받지 않습니다. 업데이트 도메인은 응용 프로그램에 대한 배포의 논리 단위입니다. 업그레이드 하는 동안 고가용성에서 hello 서비스 tooremain를 허용 하는 업데이트 도메인.

비 롤링 업그레이드는 hello 업그레이드 하는 hello hello 응용 프로그램에 하나의 업데이트 도메인에 있을 때 hello 클러스터의 적용 된 tooall 노드 있으면 가능 합니다. Hello 서비스 작동이 중단 하 고 업그레이드 hello 시간에 사용할 수 없는 되므로이 방법은 권장 되지 않습니다. 또한 업데이트 도메인 하나로 클러스터를 설정할 경우 Azure에서 어떤 보증도 제공하지 않습니다.

## <a name="health-checks-during-upgrades"></a>업그레이드 동안 상태 검사
업그레이드에 대 한 상태 정책 설정 toobe (하거나 기본값을 사용할 수 있습니다). 성공적으로 업그레이드 하는 라는 용어가 사용은 제한 시간, 지정 된 모든 업데이트 도메인은 hello 내에서 업그레이드 하는 경우 및 모든 업데이트 도메인 정상 여겨지는 합니다.  정상 업데이트 도메인 hello 상태 정책에 지정 된 모든 hello 상태 검사를 통과 하는 hello 업데이트 도메인을 의미 합니다. 예를 들어 상태 정책에 따라 응용 프로그램 인스턴스의 모든 서비스가 *정상*이어야 하고, 상태는 Service Fabric에서 정의됩니다.

업그레이드가 진행되는 동안 서비스 패브릭에서 수행하는 상태 정책 및 상태 검사는 서비스 및 응용 프로그램을 구분하지 않습니다. 즉, 서비스별 테스트를 수행하지 않습니다.  예를 들어 서비스 처리량 요구 사항이 있을 수 있지만 서비스 패브릭 hello 정보 toocheck 처리량이 없습니다. Toohello 참조 [상태 문서](service-fabric-health-introduction.md) 수행 하는 hello 검사에 대 한 합니다. hello 인스턴스가 시작 되었고 여부 hello 응용 프로그램 패키지를 올바르게 복사 하는지 여부에 대 한 업그레이드 테스트는 동안 발생 하는 hello 검사 및 기타 등등.

hello 응용 프로그램 상태가 hello 자식 엔터티 hello 응용 프로그램의 집계입니다. 즉, 서비스 패브릭 hello 응용 프로그램에 보고 된 hello 상태를 통해 hello 응용 프로그램의 hello 상태를 평가 합니다. Hello 상태 hello 응용 프로그램에 대 한 모든 hello 서비스의 이러한 방식으로 계산합니다. 서비스 패브릭 추가 hello 서비스 복제본 같이 해당 자식 항목의 hello 상태를 집계 하 여 hello 응용 프로그램 서비스의 hello 상태를 평가 합니다. Hello 응용 프로그램 상태 정책이 충족 되 면 hello 업그레이드를 진행할 수 있습니다. Hello 상태 정책 위반 되 면 hello 응용 프로그램 업그레이드가 실패 합니다.

## <a name="upgrade-modes"></a>업그레이드 모드
응용 프로그램 업그레이드에 대해 권장 하는 hello 모드는 hello 일반적으로 사용 되는 모드 모니터링 hello 모드입니다. 모니터링된 모드에서 한 번의 업데이트 도메인 hello 업그레이드를 수행 하 고 모든 상태를 확인 하는 경우 hello 정책 지정) (당 패스 toohello 다음 업데이트 도메인에 자동으로 이동 합니다.  상태 검사에 실패할 경우 시간 제한에 도달 하면, hello 업그레이드 하거나 hello 업데이트 도메인에 대 한 롤백되거나 hello 모드 변경 된 toounmonitored 수동입니다. Hello 업그레이드 toochoose 실패 한 업그레이드를 위해 이러한 두 모드 중 하나를 구성할 수 있습니다. 

모니터링 되지 않는 수동 모드로 업그레이드 하는 업데이트 도메인에 모든, tookick hello 다음 업데이트 도메인에서 hello 업그레이드 해제 한 후 수동 작업이 필요합니다. 서비스 패브릭 상태 검사가 수행되지 않습니다. 관리자에 게 hello 다음 업데이트 도메인에 있는 hello 업그레이드를 시작 하기 전에 hello 상태 또는 상태 검사를 수행 합니다.

## <a name="upgrade-default-services"></a>기본 서비스 업그레이드
서비스 패브릭 응용 프로그램 내에서 기본 서비스 응용 프로그램의 hello 업그레이드 프로세스 중 업그레이드할 수 있습니다. 기본 서비스는 hello에 정의 된 [응용 프로그램 매니페스트](service-fabric-application-model.md#describe-an-application)합니다. 기본 서비스 업그레이드 hello 표준 규칙은입니다.

1. 기본 서비스에서 새 hello [응용 프로그램 매니페스트](service-fabric-application-model.md#describe-an-application) hello 클러스터에 존재 하지 않는 만들어집니다.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) toobe tootrue tooenable hello 규칙을 설정 하는 필요 합니다. 이 기능은 v5.5에서 지원됩니다.

2. 이전 [응용 프로그램 매니페스트](service-fabric-application-model.md#describe-an-application) 및 새 버전 모두에 있는 기존 서비스가 업데이트됩니다. Hello 새 버전의 서비스 설명 hello 클러스터에 이미 없는 덮어씁니다. 기본 서비스 실패를 업데이트하는 경우 응용 프로그램 업그레이드가 자동으로 롤백됩니다.
3. 기본 서비스에서 이전 hello [응용 프로그램 매니페스트](service-fabric-application-model.md#describe-an-application) 하지만 hello 새 버전에 없는 삭제 합니다. **기본 서비스를 삭제하는 작업은 되돌릴 수 없습니다.**

응용 프로그램의 업그레이드가 롤백되면 하는 경우 기본 서비스 업그레이드가 시작 전에 되돌린된 toohello 상태를 됩니다. 하지만 삭제된 서비스를 만들 수 없습니다.

## <a name="application-upgrade-flowchart"></a>응용 프로그램 업그레이드 순서도
이 단락이 다음 hello 순서도 서비스 패브릭 응용 프로그램의 hello 업그레이드 프로세스를 이해 하는 데 유용 합니다. 특히 hello 흐름 설명 방법을 포함 하 여 제한 시간, hello *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, 및 *UpgradeHealthCheckInterval*, 성공 또는 실패 한 업데이트 도메인에 있는 hello 업그레이드도 간주 되 면 제어할 수 있습니다.

![서비스 패브릭 응용 프로그램에 대 한 hello 업그레이드 프로세스][image]

## <a name="next-steps"></a>다음 단계
[Visual Studio를 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial.md) 에서는 Visual Studio를 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[Powershell을 사용하여 응용 프로그램 업그레이드](service-fabric-application-upgrade-tutorial-powershell.md) 에서는 PowerShell을 사용하여 응용 프로그램 업그레이드를 진행하는 방법을 안내합니다.

[업그레이드 매개 변수](service-fabric-application-upgrade-parameters.md)를 사용하여 응용 프로그램 업그레이드 방법을 제어합니다.

응용 프로그램 업그레이드를 학습 하 여 호환 되도록 어떻게 toouse [데이터 직렬화](service-fabric-application-upgrade-data-serialization.md)합니다.

Toouse 너무 참조 하 여 응용 프로그램을 업그레이드 하는 동안 기능에 고급 하는 방법에 대해 알아봅니다[고급 항목](service-fabric-application-upgrade-advanced.md)합니다.

toohello 단계를 참조 하 여 응용 프로그램 업그레이드의 일반적인 문제를 수정 [응용 프로그램 업그레이드 문제 해결](service-fabric-application-upgrade-troubleshooting.md)합니다.

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
