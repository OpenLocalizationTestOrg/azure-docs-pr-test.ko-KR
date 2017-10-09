---
title: "Azure 저장소 가동 중단의 hello 이벤트에서 aaaWhat toodo | Microsoft Docs"
description: "Azure 저장소 가동 중단의 hello 이벤트에서 어떤 toodo"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: ee7eb71311c6e453dc078ec3566267ee0c2f444a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Azure 저장소 중단이 발생할 경우 어떤 toodo
Microsoft에서는 하드 toomake 서비스는 항상 사용할 수 있는지 파악 합니다. 경우에 따라 강제적으로 우리의 제어 영향을 벗어나 하나 이상의 지역에서 계획되지 않은 서비스 중단이 발생되는 경우가 있습니다. 이러한 드문 경우를 처리 하는 toohelp, Azure 저장소 서비스에 대 한 개략적인 지침을 따라 hello를 제공 합니다.

## <a name="how-tooprepare"></a>어떻게 tooprepare
모든 고객 tooprepare에는 자신의 재해 복구 계획 합니다. hello 노력 toorecover 저장소 중단이에서 일반적으로 관리자의 작업 및 순서 tooreactivate의 절차에서는 자동화 된 작동 상태에 응용 프로그램입니다. 참조 하십시오 toohello toobuild 아래 Azure 문서 재해 복구 계획:

* [Azure 응용 프로그램에 대한 재해 복구 및 고가용성](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Azure 복구력 기술 지침](../resiliency/resiliency-technical-guidance.md)
* [Azure Site Recovery 서비스](https://azure.microsoft.com/services/site-recovery/)
* [Azure 저장소 복제](storage-redundancy.md)
* [Azure 백업 서비스](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>어떻게 toodetect
hello 권장 방법은 toodetermine hello Azure 서비스 상태는 toosubscribe toohello [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/)합니다.

## <a name="what-toodo-if-a-storage-outage-occurs"></a>저장소 중단이 발생 하는 경우 어떤 toodo
하나 이상의 영역에 하나 이상의 저장소 서비스를 일시적으로 사용할 수 없으면 tooconsider 하기 위한 두 가지 옵션이 있습니다. 에 즉시 액세스 tooyour 데이터를 원하는 경우 옵션 2를 고려 하십시오.

### <a name="option-1-wait-for-recovery"></a>옵션 1: 복구 대기
이 경우에 사용자의 조치가 필요하지 않습니다. 노력 하 고 충분히 toorestore hello Azure 서비스 사용 가능 합니다. Hello에 hello 서비스 상태를 모니터링할 수 [Azure 서비스 상태 대시보드에서](https://azure.microsoft.com/status/)합니다.

### <a name="option-2-copy-data-from-secondary"></a>옵션 2: 보조에서 데이터 복사 
선택한 경우 [읽기 액세스 지역 중복 저장소 (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (권장) 저장소 계정에 대 한 나면 tooyour 데이터 읽기 액세스 hello 보조 지역에서 합니다. 와 같은 도구를 사용할 수 있습니다 [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), 및 hello [Azure 데이터 이동 라이브러리](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy 데이터로 hello 보조 지역에서 다른 저장소 계정에 unimpacted 영역과 가리킵니다 응용 프로그램 toothat 저장소 계정에 대 한 읽기 및 쓰기 가용성입니다.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>저장소 장애 조치가 발생할 경우 어떤 tooexpect
[GRS(지역 중복 저장소)](storage-redundancy.md#geo-redundant-storage) 또는 [RA-GRS(읽기 액세스 지역 중복 저장소)](storage-redundancy.md#read-access-geo-redundant-storage)(권장)를 선택한 경우 Azure Storage가 두 지역(기본 및 보조)에 데이터를 지속적으로 유지합니다. Azure 저장소는 두 지역에 여러 데이터 복제본을 계속 유지합니다.

지역적 재해 하면 기본 지역의 영향을 주는 경우 우리는 먼저 시도 해당 지역에서 toorestore hello 서비스 합니다. Hello 재해 및 일부 드문 경우 이지만에 그 영향의 hello 특성에 종속 되지 않을 수 수 toorestore hello 기본 지역입니다. 이때 지역 장애 조치(failover)를 수행합니다. hello 지역 간 데이터 복제는 아직 되지 않은 변경 내용이 복제 toohello 보조 지역 수도 있기 때문에 지연을 활성화 하는 비동기 프로세스 손실 될 수 있습니다. Hello를 쿼리할 수 [사용자의 저장소 계정 "마지막 동기화 시간"](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget hello 복제 상태에 대 한 내용은 합니다.

몇 가지 사항 hello 저장소 지리적 장애 조치 환경이 관련:

* 저장소 지리적 장애 조치만 hello Azure 저장소 팀에 의해 트리거될 – 고객 작업이 필요 하지 않습니다.
* Blob, 테이블, 큐 및 파일에 대 한 끝점 남습니다. 기존 저장소 서비스 hello hello 장애 조치 후 동일 hello DNS 항목 업데이트 toobe tooswitch hello 기본 지역 toohello 보조 지역에서 필요 합니다.
* 이전 및 hello 지리적 장애 조치 하는 동안 hello 재해의 toohello 영향 때문에 쓰기 액세스 tooyour 저장소 계정 없을 수 있지만 RA-GRS 항목으로 구성 된 저장소 계정의 경우 여전히 hello 보조에서 읽을 수 있습니다.
* Hello 지리적 장애 조치 완료 되 고 DNS 변경 내용이 전파 hello, 읽기 및 쓰기 액세스 tooyour 저장소 계정은 다시 시작 됩니다. 이 요소 toobe toowhat 사용 되는 경우 보조 끝점입니다. 
* Note GRS 또는 RA-GRS hello 저장소 계정에 구성 된 경우 쓰기 액세스를 해야 합니다. 
* 쿼리할 수 ["마지막 사용자의 저장소 계정 지리적 장애 조치 시간"](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget 더 자세히 설명 합니다.
* Hello 장애 조치 후 저장소 계정의 완벽 하 게 작동 수는 있지만 "성능이 저하 된" 상태에 있는 그대로 실제로 호스팅되는 지리적 복제 가능한 없는 사용 하 여 독립 실행형 영역에서. toomitigate 위험이 hello 원래 기본 지역 및 지리적 장애 복구를 수행 toorestore hello 원래 상태로 복원할 것입니다. 원래 기본 지역 hello를 복구할 수 없는 경우 다른 보조 지역을 할당 했습니다.
  Azure 저장소 지역 복제의 hello 인프라 대 한 자세한 내용은 참조 하십시오 toohello hello 저장소 팀 블로그 문서에 대 한 [중복 옵션 및 RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/)합니다.

## <a name="best-practices-for-protecting-your-data"></a>데이터 보호에 대한 모범 사례
정기적으로 저장소 데이터를 몇 가지 권장 되는 방법이 tooback이 있습니다.

* VM 디스크-사용 하 여 hello [Azure 백업 서비스](https://azure.microsoft.com/services/backup/) tooback Azure 가상 컴퓨터에서 사용 하는 hello VM 디스크를 구성 합니다.
* 블록 blob – 만들기는 [스냅숏](https://msdn.microsoft.com/library/azure/hh488361.aspx) 각 blob, 차단 하거나 hello blob tooanother 저장소 계정을 사용 하 여 다른 지역에 복사 [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), 또는 hello [ Azure 데이터 이동 라이브러리](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)합니다.
* 테이블-사용 하 여 [AzCopy](storage-use-azcopy.md) tooexport hello 테이블에 데이터를 다른 지역에 다른 저장소 계정입니다.
* 파일 – 사용 하 여 [AzCopy](storage-use-azcopy.md) 또는 [Azure PowerShell](storage-powershell-guide-full.md) toocopy 파일 tooanother 저장소 계정을 다른 지역에 있습니다.

Hello RA-GRS 기능을 완전 하 게 활용 하는 응용 프로그램을 만드는 방법에 대 한 내용은 확인 하세요 [항상 사용 가능한 응용 프로그램 설계 RA-GRS 저장소를 사용 하 여](storage-designing-ha-apps-with-ragrs.md)

