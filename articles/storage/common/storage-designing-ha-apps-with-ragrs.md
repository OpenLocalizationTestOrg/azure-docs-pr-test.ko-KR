---
title: "aaaDesigning Azure 읽기 액세스 지리적 중복 저장소 (RA-GRS)를 사용 하는 항상 사용 가능한 응용 프로그램입니다. | Microsoft Docs"
description: "어떻게 toouse Azure RA-GRS 저장소 tooarchitect 유연한 항상 사용 가능한 응용 프로그램을 충분 한 toohandle 중단 합니다."
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
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>RA-GRS를 사용하여 항상 사용 가능한 응용 프로그램 설계

클라우드 기반 인프라의 일반적인 기능은 응용 프로그램 호스팅을 위해 항상 사용할 수 있는 플랫폼을 제공하는 것입니다. 클라우드 기반 응용 프로그램 개발자가 고려해 야 방법을 신중 하 게 tooleverage이 플랫폼 toodeliver 항상 사용 가능한 응용 프로그램 tootheir 사용자입니다. 본이 문서에서는 사용할 수 있는 응용 프로그램 개발자가 Azure 저장소 읽기 액세스 지역 중복 저장소 (RA-GRS) toomake hello 사용 방법에 대해서만 설명 합니다.

중복 옵션에는 LRS(로컬 중복 저장소), ZRS(영역 중복 저장소), GRS(지역 중복 저장소) 및 RA-GRS(읽기 액세스 지역 중복 저장소)라는 네 가지 옵션이 있습니다. 이 문서의 toodiscuss GRS 및 RA-GRS 하겠습니다. Grs를 사용할 경우 3 개의 데이터 복사본이 hello 저장소 계정을 설정할 때 선택한 hello 기본 지역에 유지 됩니다. 세 개의 추가 복사본은 Azure에서 지정된 보조 지역에 비동기적으로 유지됩니다. RA-GRS는 점을 제외 하 고 있는 경우 읽기 권한 toohello 보조 복사본 GRS와 같은 작업을 hello 합니다. Hello 다른 Azure 저장소 중복 옵션에 대 한 자세한 내용은 참조 [Azure 저장소 복제](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy)합니다. 또한 hello 복제 아티클을 hello hello 기본 지역과 보조 지역 쌍을 표시합니다.

이 문서 및 다운로드 하 고 실행할 수 있는 hello 끝에서 링크 tooa 전체 샘플에 포함 된 코드 조각이 있습니다.

## <a name="key-features-of-ra-grs"></a>RA-GRS의 주요 기능

방법에 대 한 하기 전에 toouse RA-GRS 저장소 속성 및 동작에 대해 살펴보겠습니다.

* 보조 지역; 하면 기본 지역의에 저장 된 hello 데이터의 읽기 전용 복사본을 유지 하는 azure 저장소 위에서 언급 한 대로 hello 저장소 서비스는 hello 보조 지역의 hello 위치를 결정 합니다.

* hello 읽기 전용 복사본은 [결국 일관 된](https://en.wikipedia.org/wiki/Eventual_consistency) hello 기본 지역의 hello 데이터를 사용 합니다.

* Blob, 테이블 및 큐에 대 한 hello에 대 한 보조 영역을 쿼리할 수 있습니다는 *마지막 동기화 시간* hello 기본 toohello 보조 지역에서 복제를 마지막 hello 발생 했을 때 알려 주는 값입니다. (현재 RA-GRS 중복 옵션이 없는 Azure File Storage에 대해서는 지원되지 않습니다.)

* Hello 저장소 클라이언트 라이브러리 toointeract hello 기본 또는 보조 지역 중 하나에 hello 데이터와 함께 사용할 수 있습니다. 또한 리디렉션할 수 읽기 요청 toohello 기본 지역 시간이 초과 되 면 읽기 요청 자동으로 toohello 보조 지역입니다.

* 기본 지역의 hello hello 데이터의 hello 액세스 가능성에 영향을 주는 주요 문제 이면 hello Azure 팀은 지리적 장애 조치, 이때 toohello 기본 지역 가리키는 DNS 항목을 hello 됩니다 변경 된 toopoint toohello 보조 지역을 트리거할 수 있습니다.

* 지리적 장애 조치 발생 하는 경우 Azure는 새 보조 위치를 선택 하 고 hello 데이터 toothat 위치 복제 다음 가리킵니다 hello 보조 DNS 항목 tooit. hello 보조 끝점을 hello 저장소 계정에서 복제를 완료할 때까지 사용할 수 없게 됩니다. 자세한 내용은 참조 하십시오 [Azure 저장소 중단이 발생할 경우 어떤 toodo](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance)합니다.

## <a name="application-design-considerations-when-using-ra-grs"></a>RA-GRS를 사용하는 경우 응용 프로그램 설계 고려 사항

이 문서의 주요 목적은 hello는 tooshow toodesign에서에서 계속 됩니다 toofunction (하지만 제한 된 용량) hello 주 데이터에서 중요 재해가의 hello 이벤트에도 응용 프로그램의 가운데 어떻게 있습니다. 문제가 있으면 tooread hello 보조 지역에서 전환 하 고 기본 지역 hello를 다시 사용할 수 있는 경우 되돌리십시오 여 toohandle 일시적이 응용 프로그램 또는 장기 실행 문제를 포함 하면이 작업을 수행 합니다.

### <a name="using-eventually-consistent-data"></a>결과적으로 일치하는 데이터 사용

이 제안된 솔루션 것 이라고 가정 해도 괜 찮 tooreturn 부실 데이터 toohello 호출 응용 프로그램 일 합니다. 되기 때문에 hello 보조 데이터는 결국 일치를 hello 데이터가 toohello 기본 기록 있지만 hello 업데이트 toohello 보조 복사본이 hello 기본 지역 액세스할 수 없게 된 경우 복제를 완료 하지 않습니다.

예를 들어 고객 성공 하는 업데이트를 제출할 수 및 hello 업데이트 되기 전에 보조 전파 toohello hello 기본 다운 될 수는 다음 합니다. 이 경우 다음 hello 고객 tooread hello를 다시 데이터를 요청 하면 hello 부실 데이터를 업데이트 하는 hello 데이터 대신 수신 합니다. Hello 고객 메시지가 방법 이렇게, 그리고 있다면를 결정 해야 합니다. 보조 hello 최신 상태 이면 toocheck에서 마지막 동기화 시간에이 문서 toosee의 뒷부분에 나오는 hello 보조 데이터에 hello 하는 방법을 확인할 수 있습니다.

### <a name="handling-services-separately-or-all-together"></a>서비스를 개별적으로 또는 모두 함께 처리

동안 있지 않을 가능성이 있기 하나의 서비스 toobecome 사용할 수 없음에 대 한 hello 다른 서비스는 계속 완벽 하 게 작동 하는 동안. 있습니다 수 핸들 hello 다시 시도 되 고 각각에 대해 읽기 전용 모드로 서비스를 별도로 (blob, 큐, 테이블) 또는 모든 hello 저장소 서비스에 대 한 일반적으로 재시도 함께 처리할 수 있습니다.

예를 들어 응용 프로그램에서 큐 및 blob을 사용 하는 경우 이러한 각 항목에 대 한 별도 코드 toohandle 다시 시도 가능한 오류가 tooput를 결정할 수 있습니다. 그런 다음 hello blob 서비스에서 다시 시도 가져오지만 hello 큐 서비스가 계속 작동 하는 경우 blob을 처리 하는 응용 프로그램의 hello 부분에만 영향을 미칩니다. 결정 한 경우 toohandle 모든 저장소 서비스는 일반적으로 다시 시도 하 고 호출 toohello blob 서비스는 다시 시도 가능한 오류를 반환 합니다. 다음 요청 tooboth hello blob 서비스 및 큐 서비스 hello 영향을 받습니다.

궁극적으로, 응용 프로그램의 hello 복잡성에 따라 다릅니다. 서비스에 의해 toohandle hello 실패 하지를 결정할 수 있습니다 하지만 대신 tooredirect 읽은 모든 저장소 서비스 toohello 보조 지역에 대 한 요청 hello 기본 지역에서 모든 저장소 서비스의 문제를 발견 하는 경우 읽기 전용 모드로 hello 응용 프로그램을 실행 합니다.

### <a name="other-considerations"></a>기타 고려 사항

이러한 다른 고려 사항 hello이이 문서의 나머지 부분에 대해 설명 합니다 hello 됩니다.

*   Hello 회로 차단기 패턴을 사용 하 여 읽기 요청의 재시도 처리

*   결국 일관 된 데이터 및 hello 마지막 동기화 시간

*   테스트

## <a name="running-your-application-in-read-only-mode"></a>읽기 전용 모드에서 응용 프로그램 실행

RA-GRS 저장소 toouse 있습니다 수 toohandle 모두 실패 읽기 요청 및 업데이트 요청 수 (이 경우 삽입, 업데이트 및 삭제를 의미 하는 업데이트) 실패 했습니다. Hello 주 데이터 센터 실패 읽기 요청에 리디렉션된 toohello 보조 데이터 센터 수는 있지만 hello 보조 읽기 전용 이므로 업데이트 요청 수 없습니다. 이 따라서 몇 가지 방식으로 toorun 읽기 전용 모드에서 응용 프로그램이 필요합니다.

예를 들어 모든 업데이트 요청 toohello 저장소 서비스에 제출 하기 전에 확인 하는 플래그를 설정할 수 있습니다. 를 통해 전달 hello 업데이트 요청 중 하나 것을 건너뛰고 적절 한 응답 toohello 고객을 반환 합니다. 도 hello 문제가 해결 될 때까지 toodisable 특정 기능을 모두 선택 하 고 이러한 기능은 일시적으로 사용할 수 없는 사용자에 게 알릴 수 있습니다.

각 서비스에 대 한 toohandle 오류를 별도로 결정 해야 합니다 toohandle hello 기능 toorun 읽기 전용 모드에서 응용 프로그램 서비스에 의해 합니다. 사용할 수 있는 각 서비스에 대 한 읽기 전용 플래그를 지정할 수 있습니다 및 사용 안 함 및 핸들 hello hello 코드의 적절 한 위치에서 적절 한 플래그입니다.

읽기 전용 모드에서 응용 프로그램에 다른 부수적인 혜택 – 제공 수 toorun 되 고 hello 기능 tooensure 주요 응용 프로그램 업그레이드를 사용 하는 동안 기능을 제한 합니다. 업그레이드를 수행 하는 동안 hello 기본 지역의 hello 데이터에 액세스 하는 사람이 보장 읽기 전용 모드 및 지점이 toohello 보조 데이터 센터에서 응용 프로그램 toorun 프로그램 트리거할 수 있습니다.

## <a name="handling-updates-when-running-in-read-only-mode"></a>읽기 전용 모드에서 실행하는 경우 업데이트 처리

여러 가지 방법으로 읽기 전용 모드에서 실행할 때 toohandle 업데이트를 요청 합니다. 이 내용에 대해서는 포괄적인 경우 대신 일반적인 경우와 몇 가지 고려해야 할 패턴을 언급하겠습니다.

1.  Tooyour 사용자 응답할 수 있으며 현재 업데이트를 수락 하지 않습니다을 설명할 수 있습니다. 예를 들어 연락처 관리 시스템 고객 tooaccess 연락처 정보를 사용 하도록 설정 수 있지만 업데이트를 확인 하지 않습니다.

2.  업데이트를 다른 지역의 큐에 넣을 수 있습니다. 이 경우 있습니다는 보류 중인 업데이트 요청 tooa 큐 다른 지역에 작성 한 다음 방식으로 tooprocess 이러한 요청 hello 기본 데이터 센터를 다시 온라인 상태로 돌아온 후. 이 시나리오에서 요청 하는 hello 업데이트는 나중에 처리에 대 한 큐에 대기 알고 hello 고객을 알려야 합니다.

3.  업데이트 tooa 저장소 계정이 다른 지역에 작성할 수 있습니다. 다음 경우 hello 기본 데이터 센터 온라인 상태가 되 면 할 수 있습니다 방식으로 toomerge hello hello 데이터 구조에 따라 hello 기본 데이터에 해당 업데이트 합니다. 예를 들어 hello 이름에 날짜/시간 스탬프와 별도 파일을 만드는 경우 해당 파일 백 toohello 기본 지역으로 복사할 수 있습니다. 이러한 방식은 로깅 및 iOT 데이터와 같은 워크로드에 적합합니다.

## <a name="handling-retries"></a>다시 시도 처리

어떤 오류를 다시 시도할 수 있는지 어떻게 할 수 있을까요? 이 hello 저장소 클라이언트 라이브러리에 의해 결정 됩니다. 예를 들어 404 오류 (리소스를 찾을 수 없습니다.) 없는 경우 다시 시도할 수 아니므로 것을 다시 시도의 성공 가능성 tooresult Hello를 500 오류는 다시 시도할 수 때문에 서버 오류를 일시적인 문제가 단순히는 것입니다. 자세한 내용은 체크 아웃 hello [hello ExponentialRetry 클래스에 대 한 소스 코드를 열고](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) hello.NET 저장소 클라이언트 라이브러리의 합니다. (ShouldRetry 메서드 hello에 대 한 확인).

### <a name="read-requests"></a>읽기 요청

기본 저장소에 문제가 읽기 요청 리디렉션된 toosecondary 저장 될 수 있습니다. 에 앞서 언급 같이 [를 사용 하 여 결국 일관 된 데이터](#using-eventually-consistent-data), 응용 프로그램 toopotentially 부실 데이터를 읽을 수용 가능 해야 합니다. Hello 저장소 클라이언트 라이브러리 tooaccess RA-GRS 데이터를 사용 하는 경우 hello에 대 한 값을 설정 하 여 hello 다시 시도 동작이 읽기 요청을 지정할 수 있습니다 **LocationMode** 속성 tooone hello 다음 중:

*   **Primaryonly에 따라** (기본 hello)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Hello를 설정 하는 경우 **LocationMode** 너무**PrimaryThenSecondary**hello 초기 요청 toohello 기본 끝점이 오류로 실패, hello 클라이언트에 자동으로 다른 읽기는 읽기, toohello 보조 끝점을 요청 합니다. Hello 오류는 서버 시간 초과, 다음 hello 클라이언트 경우 toowait timeout tooexpire hello에 대 한 다시 시도 가능한 오류가 hello 서비스에서 받기 전에 있습니다.

결정할 때 기본적으로 두 가지 시나리오 tooconsider 사항이 어떻게 toorespond tooa 다시 시도 가능한 오류:

*   격리 된 문제 이며 후속 요청 toohello 기본 끝점 오류로 반환 하지 않습니다. 이런 경우가 발생할 수 있는 예는 일시적인 네트워크 오류가 있는 경우입니다.

    이 시나리오에서는 있는 상당한 성능 저하는 없으며 있는에서 **LocationMode** 도**PrimaryThenSecondary** 만 이런 상황이 발생 빈도가으로 합니다.

*   이 hello 기본 지역의 hello 저장소 서비스 중 하나 이상에 문제가 및 모든 후속 요청 toothat 서비스 hello 기본 지역에 가능성이 tooreturn 다시 시도 가능한 오류 일정 기간에 대 한 합니다. 이러한 예로 hello 기본 지역 완전히 액세스할 수 없는 경우입니다.

    이 시나리오에서 성능이 저하 되므로 모든 읽기 요청이 됩니다 hello 기본 끝점을 먼저 시도, hello timeout tooexpire 될 때까지 기다린 후 전환 toohello 보조 끝점입니다.

이러한 시나리오에 대 한 식별 해야 있는지 hello 기본 끝점으로 진행 중인 문제가 되 고 toohello 보조 끝점을 설정 하 여 hello 직접 모든 읽기 요청을 보낼 **LocationMode** 속성 너무 **SecondaryOnly**합니다. 이번에 읽기 전용 모드에서 응용 프로그램 toorun hello를 변경 해야 합니다. 이 방법은 hello 라고 [회로 차단기 패턴](https://msdn.microsoft.com/library/dn589784.aspx)합니다.

### <a name="update-requests"></a>업데이트 요청

hello 회로 차단기 패턴에 적용 된 tooupdate 요청 될 수도 있습니다. 그러나 업데이트 요청에 리디렉션된 toosecondary 저장소는 읽기 전용를 수 없습니다. 이러한 요청에 대 한 유지 해야 합니다. hello **LocationMode** 속성이 너무 설정**primaryonly에 따라** (기본 hello). toohandle 이러한 오류 행 –에 10 개의 오류와 같은 메트릭 toothese 요청-를 적용 하 고 임계값이 충족 되 면 hello 응용 프로그램을 읽기 전용 모드로 전환할 수 있습니다. 사용할 수 있습니다 hello 회로 차단기 패턴에 대 한 hello 다음 섹션에서 아래 설명 된 것과 tooupdate 모드를 반환 하는 데 동일한 방법을 hello 합니다.

## <a name="circuit-breaker-pattern"></a>회로 차단기 패턴

Hello 회로 차단기 패턴을 사용 하 여 응용 프로그램에서 반복 해 서 가능성이 toofail은 작업을 다시 시도해도 별다른 방지할 수 있습니다. 지 수 적으로 hello 작업을 다시 시도 하는 동안 시간을 차지 하는 것이 아니라 응용 프로그램 toocontinue toorun hello 수 있습니다. 또한 hello 오류 수정 되 면, 시간 hello 응용 프로그램을 hello 작업을 다시 시도할 수를 검색 합니다.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>어떻게 tooimplement hello 회로 차단기 패턴

tooidentify는 진행 중인 문제가 기본 끝점, hello 클라이언트에서 다시 시도 가능한 오류가 발생 하는 빈도 모니터링할 수 있습니다. Toodecide 있는 각각의 경우 다르기 때문에 hello 임계값에 toouse hello 의사 결정 tooswitch toohello 보조 끝점에 대 한을 읽기 전용 모드로 hello 응용 프로그램을 실행 합니다. 예를 들어 없는 성공 사용 하 여 행 10 오류가 발생 하는 경우 tooperform hello 스위치를 결정할 수 있습니다. 또 다른 예로 2 분 동안에서 hello 요청의 90% 실패 하는 경우 tooswitch 합니다.

Hello 첫 번째 시나리오에서는 단순히 hello 오류 개수 등에 도달 하기 전에 성공 최대, 설정 hello count 백 toozero hello 없을 경우. Hello 두 번째 시나리오에 대 한 한 가지 방법은 tooimplement toouse는 hello MemoryCache 개체 (.NET). 각 요청에 대 한 CacheItem toohello 캐시 추가 hello 값 toosuccess (1) 또는 실패 (0)을 설정한 hello 만료 시간 too2 분 지금 (또는 시간 제한 무엇이)에서 설정 합니다. 항목의 만료 시간에 도달 하면 hello 항목이 자동으로 제거 됩니다. 이렇게 하면 2분 기간으로 롤링하게 됩니다. 요청 toohello 저장소 서비스를 만들 때마다 먼저 쿼리를 사용 Linq hello MemoryCache 개체 toocalculate hello 성공 백분율 간에 hello 값 합계를 구하고 hello 수로 나누어 여 합니다. Hello 성공 백분율 (예: 10%) 일부 임계값 아래로 떨어지면 설정 hello **LocationMode** 속성에 대 한 읽기 요청을 너무**SecondaryOnly** hello 응용 프로그램을 하기 전에 읽기 전용 모드로 전환 계속 진행 합니다.

오류의 hello 임계값 toodetermine를 사용할 toomake hello 스위치 구성 가능한 매개 변수를 만들어 고려해 야 하므로 응용 프로그램에서 서비스 tooservice에서 달라질 수 있습니다. 이기도 toohandle 각 서비스에서 다시 시도 가능한 오류를 별도로 결정 하는 경우 또는 1로, 이전에 설명한 대로 합니다.

또 다른 고려 사항은 어떻게 toohandle 응용 프로그램의 여러 인스턴스 및 다시 시도 가능한 오류 각 인스턴스를 검색 하는 경우 어떤 toodo 합니다. 예를 들어 20 대의 Vm 동일한 응용 프로그램이 로드 하는 hello로 실행을 할 수 있습니다. 각 인스턴스를 별도로 처리할까요? 하나의 인스턴스가 시작 하는 데 문제가, toolimit hello 응답 toojust 하나 들어 아니면 tootry toohave 원하는 경우 모든 인스턴스 hello에 동일한 방식으로 때 응답 인스턴스 하나에 문제가 있습니까? Hello 인스턴스를 별도로 처리 하는 것이 toocoordinate hello 응답을 것 보다 훨씬 더 간단 하지만이 방법은 응용 프로그램의 아키텍처에 따라 달라 집니다.

### <a name="options-for-monitoring-hello-error-frequency"></a>Hello 오류 주파수 모니터링 옵션

세 가지 옵션이 있습니다 주 toohello 보조 지역 및 변경 tooswitch hello 읽기 전용 모드에서 응용 프로그램 toorun 때 hello 주파수 hello 기본 지역의 순서 toodetermine에 다시 시도 모니터링 합니다.

*   Hello에 대 한 처리기를 추가 [ **다시 시도 중** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) hello에 이벤트 [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) tooyour 저장소 요청을 전달 하면 –이 hello 개체 메서드가이 문서에 표시 되며 hello 함께 나타날 샘플에에서 사용 합니다. Hello 클라이언트는 요청을 다시 시도할 때마다이 이벤트가 발생, 수 있게 해 주는 tootrack 얼마나 자주 hello 클라이언트 기본 끝점에 다시 시도 가능한 오류가 발생 합니다.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   Hello에 [ **평가** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) 사용자 지정 다시 시도 정책에 대 한 메서드를 다시 시도 하 여 수행 될 때마다 사용자 지정 코드를 실행할 수 있습니다. 다시 시도 하 여 경우 기회 toomodify 다시 시도 동작이 hello 제공도 또한 toorecording에 있습니다.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   hello 세 번째 방법은 tooimplement 지속적으로 더미 사용 하 여 기본 저장소 끝점을 ping 하는 응용 프로그램에서 사용자 지정 모니터링 구성 요소 읽기 요청 (예: 소규모 blob을 읽는 중) toodetermine의 상태입니다. 이렇게 하려면 리소스가 소비되지만 그 양은 많지 않습니다. 임계값에 도달 하는 문제가 발견 되는 경우 다음 수행 hello 스위치 너무**SecondaryOnly** 및 읽기 전용 모드입니다.

어느 시점 부터는 tooswitch 백 toousing hello에 대 한 기본 끝점 및 업데이트 허용 합니다. 위에 나열 된 hello 처음 두 방법 중 하나를 사용 하는 경우 수을 하기만 하면 뒤로 toohello 기본 끝점을 전환 작업의 수 또는 임의로 선택 된 시간 만큼 수행 된 후 업데이트 모드를 사용 하도록 설정 합니다. Hello 재시도 논리를 통해 다시 버릴 수 수 있습니다 있습니다. Hello 문제가 해결 되었는지 toouse hello에 대 한 기본 끝점을 계속 되며 업데이트를 허용 합니다. 문제가 계속 되 면 한 번 더 전환지 것입니다 백 toohello 보조 끝점 및 읽기 전용 모드 hello 조건을 설정 하면 실패 한 후.

Hello 세 번째 시나리오에 대 한 핑 hello 기본 저장소 끝점 다시, 성공적인 해지면를 트리거할 수 있습니다 hello 스위치 다시 너무**primaryonly에 따라** 하 고 계속 업데이트를 허용 합니다.

## <a name="handling-eventually-consistent-data"></a>결과적으로 일치하는 데이터 처리

RA-GRS 트랜잭션을 hello 기본 toohello 보조 지역에서 복제 하 여 작동 합니다. 이 복제 프로세스 hello 보조 영역에 있는 hello 데이터 임을 보장 *결국 일관 된*합니다. 이 있을 수 있음을 지연 현상이 발생 하기 전에 하지만 hello 기본 지역에 있는 모든 hello 트랜잭션을 결국 hello 보조 영역에 표시 됨을 의미 하 고는 보장은 없습니다 hello 트랜잭션이 동일한 순서와 hello에 hello 보조 지역에 도착 원래 적용 된 hello 기본 지역에서입니다. 거래 순서를 다르게 hello 보조 지역에 도착 하는 경우 있습니다 *수* hello 서비스에서 처리할 때까지 데이터에 일관성이 없는 상태에 hello 보조 지역 toobe 것이 좋습니다.

hello 다음 표에서 모양의 예제가 나와 직원 toomake의 hello 세부 정보를 업데이트 하는 경우 어떻게 될 그녀는 hello 소속 *관리자* 역할입니다. 이 예의 hello 위해서이 위해서는 hello 업데이트 **직원** 엔터티와 업데이트는 **관리자 역할** hello 관리자의 총 수와 함께 엔터티. Hello 업데이트 적용 순서가 hello 보조 지역에 확인 합니다.

| **Time** | **트랜잭션**                                            | **복제**                       | **마지막 동기화 시간** | **결과** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | 트랜잭션 A: <br> 주 지역에 <br> 직원 엔터티 삽입 |                                   |                    | 트랜잭션 A tooprimary, 삽입<br> 아직 복제되지 않음 |
| T1       |                                                            | 트랜잭션 A가 <br> 보조 지역에<br> 복제됨 | T1 | 트랜잭션 A toosecondary 복제. <br>마지막 동기화 시간이 업데이트됨.    |
| T2       | 트랜잭션 B:<br>주 지역에서<br> 직원 엔터티<br> 업데이트  |                                | T1                 | 트랜잭션 B tooprimary, 작성<br> 아직 복제되지 않음  |
| T3       | 트랜잭션 C:<br> 주 지역에서 <br>관리자 역할<br>엔터티<br>업데이트 |                    | T1                 | 트랜잭션 기록 tooprimary, C<br> 아직 복제되지 않음  |
| *T4*     |                                                       | 트랜잭션 C가 <br>보조 지역에<br> 복제됨 | T1         | 트랜잭션이 C toosecondary를 복제 합니다.<br>트랜잭션 B가 아직 복제되지 않아서 <br>LastSyncTime이 업데이트되지 않음|
| *T5*     | 보조 지역의 <br>엔터티 읽기                           |                                  | T1                 | Hello 직원에 대 한 오래 된 값을 가져올 수 <br> 않아서 직원 엔터티에 대해 <br> 부실한 값을 얻음 Hello에 대 한 새 값을 가져올 수<br> 관리자 역할 엔터티에 대해<br> 새 값을 얻음 트랜잭션 B가 복제되지 않았기<br> 때문에 마지막 동기화 시간이<br> 아직 업데이트되지 않음. 엔터티 날짜/시간이 마지막<br>동기화 시간보다 나중이기 때문에 <br>hello 엔터티 날짜/시간 이후 이므로 <br>hello 마지막 동기화 시간입니다. |
| *T6*     |                                                      | 트랜잭션 B가<br> 보조 지역에<br> 복제됨 | T6                 | *T6* – C까지 모든 트랜잭션이 <br>복제됨. 마지막 동기화<br> 시간이 업데이트됨 |

이 예제에서는 t 5에 hello 보조 지역에서 hello 클라이언트 스위치 tooreading를 가정 합니다. Hello를 성공적으로 읽을 수 **관리자 역할** 이때 엔터티 하지만 hello 엔터티 hello 수가 일치 하지 않는 관리자 hello 개수에 대 한 값이 포함 된 **직원** 엔터티 이 이번에 hello 보조 지역에서 관리자로 표시 합니다. 클라이언트는 hello 위험 일관 되지 않은 정보가 인지이 값을 표시 하기만 하면 못했습니다. 또는 클라이언트 hello을 시도할 수 toodetermine 해당 hello **관리자 역할** hello 업데이트 순서를 다르게 나타나므로 나 다음이 팩트의 hello 사용자에 게 알리는 때문에 잠재적으로 일관성이 없는 상태입니다.

잠재적으로 일치 하지 않는 데이터가 있는지 toorecognize, hello 클라이언트 hello의 hello 값을 사용할 수 *마지막 동기화 시간* 저장소 서비스를 쿼리하여 언제 든 지 파악할 수 있습니다. 네트워크 인지 hello 보조 영역에 있는 hello 데이터 된 마지막 hello 시간 일관 된 모든 hello 서비스에 적용 될 때 트랜잭션을 이전 toothat 지점 시간에서에 hello 및 합니다. Hello 서비스는 hello를 삽입 한 후 위의 hello 예에서 **직원** hello 보조 영역에 엔터티를 hello 마지막 동기화 시간 설정 되어 너무*T1*합니다. 에 그대로 유지 됩니다 *T1* hello 서비스는 hello 업데이트 될 때까지 **직원** hello 너무 설정 되어 있는 경우 보조 영역에 엔터티*T6*합니다. Hello 클라이언트 hello에 hello 엔터티를 읽을 때 마지막 동기화 시간을 검색 하는 경우 *T5*, hello 엔터티의 hello 타임 스탬프와 비교할 수 있습니다. Hello 엔터티 hello 타임 스탬프 hello 보다 이후인 경우 시간, 마지막 동기화 후 hello 엔터티 잠재적으로 일치 하지 않는 상태 이며 무엇이 hello 응용 프로그램에 대 한 적절 한 조치를 취할 수 있습니다. 이 필드를 사용 하 여 hello 마지막 업데이트 toohello 기본 완료 된 시기를 알고 있어야 합니다.

## <a name="testing"></a>테스트

응용 프로그램의 다시 시도 가능한 오류가 발생 하는 경우 예상 대로 동작 하는 중요 한 tootest 것 합니다. 예를 들어 응용 프로그램 스위치 toohello 보조 hello tootest 해야 및 읽기 전용 모드에는 문제가 발견 되 고 전환 합니다. 때 기본 지역 hello를 다시 사용할 수 있습니다. toodo이 방식으로 toosimulate 다시 시도 가능한 오류 필요 하 고 발생 빈도 제어 합니다.

사용할 수 있습니다 [Fiddler](http://www.telerik.com/fiddler) toointercept 및 스크립트에서 HTTP 응답을 수정 합니다. 이 스크립트는 기본 끝점에서 제공 하는 응답을 식별 하 고 hello HTTP 상태 코드 tooone 저장소 클라이언트 라이브러리는 다시 시도 가능한 오류를 인식 하는 hello를 변경할 수 있습니다. 이 코드 조각은 hello에 대 한 응답 tooread 요청을 차단 하는 Fiddler 스크립트의 간단한 예를 보여 줍니다. **employeedata** 테이블 tooreturn 502 상태:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

이 예제에서는 toointercept 보다 넓은 범위의 요청을 확장 하 고 hello에만 변경할 수 **responseCode** 그 중 일부에 toobetter 실제 시나리오 시뮬레이션 합니다. Fiddler 스크립트를 사용자 지정 하는 방법에 대 한 자세한 내용은 참조 [요청 또는 응답 수정](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) hello Fiddler 설명서에에서 있습니다.

응용 프로그램 tooread 전용 모드에 구성 가능한 전환을 위한 hello 임계값 내용을 보다 쉽게 tootest hello에 대 한 동작 비-프로덕션 트랜잭션 볼륨 됩니다.

## <a name="next-steps"></a>다음 단계

* 자세한 내용은 대 한 읽기 액세스 지리적 중복을 참조 하십시오 hello LastSyncTime 설정 되는 방법의 다른 예제를 포함 하 여 [Windows Azure 저장소 중복 옵션 및 읽기 액세스 지역 중복 저장소](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/)합니다.

* Toomake hello 기본 및 보조 끝점 간에 앞뒤로 스위치 hello 하는 방법을 보여 주는 전체 샘플을 참조 하십시오 [사용 하 여 Azure 예제 – RA-GRS 저장소가 있는 회로 차단기 패턴 hello](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs)합니다.
