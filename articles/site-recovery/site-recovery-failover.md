---
title: "사이트 복구에서 aaaFailover | Microsoft Docs"
description: "Azure Site Recovery hello 복제, 장애 조치 및 복구 가상 컴퓨터와 물리적 서버와 조정합니다. 장애 조치 tooAzure 또는 보조 데이터 센터에 알아봅니다."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>사이트 복구에서 장애 조치
이 문서에서는 toofailover 가상 컴퓨터와 물리적 서버와 사이트 복구에서 보호 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>필수 조건
1. 장애 조치를 수행 하기 전에 수행 된 [테스트 장애 조치](site-recovery-test-failover-to-azure.md) tooensure 모든 것이 예상 대로 작동 하는 합니다.
1. [Hello 네트워크 준비](site-recovery-network-design.md) 장애 조치를 수행 하기 전에 대상 위치에 있습니다.  


## <a name="run-a-failover"></a>장애 조치(Failover) 실행
이 절차에서는 설명 방법에 대 한 장애 조치 한 toorun는 [복구 계획](site-recovery-create-recovery-plans.md)합니다. 또는 hello에서 단일 가상 컴퓨터 또는 실제 서버에 대 한 hello 장애 조치를 실행할 수도 **복제 된 항목이** 페이지


![장애 조치(failover)](./media/site-recovery-failover/Failover.png)

1. **복구 계획** > *recoveryplan_name*을 선택합니다. **장애 조치(Failover)**를 클릭합니다.
2. Hello에 **장애 조치** 화면에서 한 **복구 지점** toofailover 하 합니다. Hello 다음 옵션 중 하나를 사용할 수 있습니다.
    1.  **최신** (기본값):이 옵션은 먼저 tooit을 통해이 중지 하기 전에 보낸된 tooSite 복구 서비스 toocreate 각 가상 컴퓨터에 대 한 복구 지점이 된 모든 hello 데이터를 처리 합니다. 이 옵션은 hello 제공 hello 가상 컴퓨터와 모든 hello 데이터를 포함 하는 장애 조치 후에 생성 된 가장 낮은 RPO (Recovery Point Objective)는 hello 장애 조치 트리거된 경우 tooSite 복구 서비스를 복제 합니다.
    1.  **최신 처리**: hello 복구 계획 toohello 최근 복구 지점 Site Recovery 서비스에서 이미 처리 된 모든 가상 컴퓨터를 통해이 옵션에 실패 합니다. 가상 컴퓨터의 테스트 장애 조치를 수행 하는 타임 스탬프 hello 최근 처리 된 복구 지점 표시 됩니다. 복구 계획의 장애 조치를 수행 하는 경우 tooindividual 가상 컴퓨터를 이동 하 고 확인 수 **최신 복구 지점을** tooget이이 정보를 바둑판식으로 합니다. 시간이 없는 tooprocess hello 처리 되지 않은 데이터,이 옵션은 낮은 RTO (복구 시간 목표) 장애 조치 옵션을 제공 합니다.
    1.  **최신 응용 프로그램에 일관 된**:이 옵션의 hello 복구 계획 toohello 최신 응용 프로그램 일치 복구 지점 Site Recovery 서비스에서 이미 처리 된 모든 가상 컴퓨터를 통해 실패 합니다. 가상 컴퓨터의 테스트 장애 조치를 수행 하는 hello 최신 응용 프로그램 일치 복구 지점의 타임 스탬프 표시 됩니다. 복구 계획의 장애 조치를 수행 하는 경우 tooindividual 가상 컴퓨터를 이동 하 고 확인 수 **최신 복구 지점을** tooget이이 정보를 바둑판식으로 합니다.
    1.  **최신 다중 VM 처리**: 이 옵션은 다중 VM 일관성이 켜져 있는 하나 이상의 가상 컴퓨터가 포함된 복구 계획에만 사용할 수 있습니다. 가상 컴퓨터는 복제 그룹 장애 조치 toohello 최신 일반적인 다중 VM 일관성 복구의 일부인 가리킵니다. 다른 가상 컴퓨터 장애 조치 tootheir 최신 처리 된 복구 지점입니다.  
    1.  **최신 다중 VM 앱 일치**: 이 옵션은 다중 VM 일관성이 켜져 있는 하나 이상의 가상 컴퓨터가 포함된 복구 계획에만 사용할 수 있습니다. 복제의 일부인 가상 컴퓨터 장애 조치 toohello 최신 일반적인 다중 VM 응용 프로그램 일치 복구 지점을 그룹화 합니다. 다른 가상 컴퓨터 장애 조치 tootheir 최신 응용 프로그램 일치 복구 지점입니다.
    1.  **사용자 지정**: 가상 컴퓨터의 테스트 장애 조치를 수행 하는 경우이 옵션 toofailover tooa 특정 복구 지점을 사용할 수 있습니다.

    > [!NOTE]
    > hello 옵션 toochoose 복구 지점은 tooAzure를 통해 실패 하는 경우에 사용할 수 있습니다.
    >
    >


1. 이전 장애 조치 된 일부 hello 복구 계획에서 가상 컴퓨터 hello 및 사용 하 여 소스와 대상 위치에 hello 가상 컴퓨터가 활성화 되어, 이제 경우 **방향을 변경** toodecide hello 방향 옵션 hello 장애 조치가 수행 되어야 합니다.
1. TooAzure로는 장애 조치 하는 hello 클라우드 (VMM 서버에서 hyper-v 가상 컴퓨터를 보호 하는 경우에 적용 됨)에 대 한 데이터 암호화를 사용 하는 경우, **암호화 키** 선택 hello 발급 된 인증서를 때 있습니다 hello VMM 서버에 설치 하는 동안 데이터 암호화를 사용할 수 있습니다.
1. 선택 **장애 조치를 시작 하기 전에 컴퓨터를 종료** hello 장애 조치를 트리거하기 전에 원본 가상 컴퓨터의 종료 tooattempt toodo 사이트 복구 하려는 경우. 종료가 실패하더라도 장애 조치는 계속됩니다.  

    > [!NOTE]
    > Hyper-v 가상 컴퓨터의 경우이 옵션에 아직 보내지 않은 toohello 서비스 hello 장애 조치를 트리거하기 전에 toosynchronize hello 온-프레미스 데이터 하려고 시도 합니다.
    >
    >

1. Hello에 hello 장애 조치가 진행 상황을 따를 수 **작업** 페이지. 계획 되지 않은 장애 조치 중에 오류가 발생 하는 경우에 hello 복구 계획에는 완료 될 때까지 실행 합니다.
1. Hello 장애 조치 후 tooit에 로그인 하 여 hello 가상 컴퓨터를 확인 합니다. Hello 가상 컴퓨터용 toogo 다른 복구 지점을 사용할 경우 사용할 수 있습니다 **복구 지점을 변경할** 옵션입니다.
1. 가상 컴퓨터를 조치할 hello, 했으면 다음을 할 수 있습니다 **커밋** hello 장애 조치 합니다. 그러면 hello 서비스와 함께 사용할 수 있는 모든 hello 복구 지점이 삭제 및 **복구 지점을 변경할** 옵션을 더 이상 사용할 수 없습니다.

## <a name="planned-failover"></a>계획된 장애 조치
Site Recovery를 사용하여 보호되는 Hyper-V 가상 컴퓨터는 장애 조치와는 별도로 **계획된 장애 조치**도 지원합니다. 이는 데이터 무손실 장애 조치 옵션입니다. 계획된 된 장애 조치 트리거되면 원본 가상 컴퓨터 종료 hello 데이터 동기화 toobe 동기화 되 고 장애 조치 후 트리거되는 아직 hello 먼저 합니다.

> [!NOTE]
> 하나에서 가상 컴퓨터를 hyper-v 장애 조치 하면 온-프레미스 사이트 tooanother 때 온-프레미스 사이트, toocome 백 toohello 기본 온-프레미스 사이트로 toofirst 있는 **역방향 복제** hello 가상 컴퓨터 다시 tooprimary 사이트 및 그런 다음 장애 조치를 트리거하십시오. 주 가상 컴퓨터 hello 다음 너무 시작 하기 전에 사용할 수 없으면**역방향 복제** 백업에서 toorestore hello 가상 컴퓨터가 있는 합니다.   
>
>

## <a name="failover-job"></a>장애 조치 작업

![장애 조치(Failover)](./media/site-recovery-failover/FailoverJob.png)

장애 조치가 트리거되면 다음 단계를 수행합니다.

1. 필수 조건 확인: 장애 조치에 필요한 모든 조건이 충족되는지 확인합니다.
1. 장애 조치:이 단계 hello 데이터를 처리 하 고 옵트아웃 Azure 가상 컴퓨터를 만들 수 있도록 준비 만듭니다. 선택한 경우 **최신** 복구 지점을이 단계는 toohello 서비스 보낸 hello 데이터에서 복구 지점의 만듭니다.
1. 시작:이 단계는 hello 이전 단계에서 처리 하는 hello 데이터를 사용 하 여 Azure 가상 컴퓨터를 만듭니다.

> [!WARNING]
> **진행 중인 취소 안 함 장애 조치**: hello 가상 컴퓨터에 대 한 복제 장애 조치를 시작 되기 전에 중지 합니다. 경우 있습니다 **취소** 는 진행 중인 작업에서 장애 조치 중지 하지만 hello 가상 컴퓨터가 시작 되지 것입니다 tooreplicate 합니다. 복제를 다시 시작할 수 없습니다.
>
>

## <a name="time-taken-for-failover-tooazure"></a>장애 조치 tooAzure에 걸린 시간

경우에 따라 가상 컴퓨터의 장애 조치 일반적으로 약 8 too10 분 toocomplete 받아들이는 중간 단계를 수행 해야 합니다. 여기에 해당하는 경우는 다음과 같습니다.

* 9.8 이전 버전의 모바일 서비스를 사용하는 VMware 가상 컴퓨터
* 물리적 서버 
* VMware Linux 가상 컴퓨터
* 물리적 서버로 보호되는 Hyper-V 가상 컴퓨터
* 다음 드라이버가 부팅 드라이버로 제공되지 않는 VMware 가상 컴퓨터 
    * storvsc 
    * vmbus 
    * storflt 
    * intelide 
    * atapi
* DHCP 또는 고정 IP 주소 사용 여부와 관계없이 DHCP 서비스를 사용할 수 없는 VMware 가상 컴퓨터

모든 hello에 다른 경우가 중간 단계 필요 하지 않으며 hello 장애 조치에 걸리는 hello 훨씬 낮습니다. 





## <a name="using-scripts-in-failover"></a>장애 조치에서 스크립트 사용
장애 조치를 수행 하는 동안 tooautomate 특정 작업을 할 수 있습니다. 스크립트를 사용할 수 있습니다 또는 [Azure 자동화 runbook](site-recovery-runbook-automation.md) 에 [복구 계획](site-recovery-create-recovery-plans.md) toodo입니다.

## <a name="other-considerations"></a>기타 고려 사항
* **드라이브 문자** -장애 조치 후 가상 컴퓨터에서 tooretain hello 드라이브 문자 hello를 설정할 수 있습니다 **SAN 정책** 가상 hello에 대 한 컴퓨터 너무**OnlineAll**합니다. [자세히 알아보기](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>다음 단계
가상 컴퓨터를 통해 실패 하 고 hello 온-프레미스 데이터 센터를 사용할 수를 수행 해야 [ **다시 보호** ](site-recovery-how-to-reprotect.md) VMware 가상 컴퓨터 백업 toohello 온-프레미스 데이터 센터입니다.

사용 하 여 [ **계획 된 장애 조치** ](site-recovery-failback-from-azure-to-hyper-v.md) 옵션**장애 복구** hyper-v 가상 컴퓨터는 Azure에서 tooon 온-프레미스를 백업 합니다.

실패 한 경우 hyper-v 가상 컴퓨터 tooanother 온-프레미스 데이터에 대해 VMM 서버와 hello 기본 데이터 센터에서 관리 센터를 사용 하 여 **역방향 복제** 옵션 toostart hello 복제 백 toohello 기본 데이터 센터입니다.
