---
title: "hello Azure 포털에서에서 Azure 검색에 대 한 aaaService 관리"
description: "Azure 검색에서는 hello Azure 포털을 사용 하 여 Microsoft Azure에서 호스팅된 클라우드 검색 서비스를 관리 합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Hello Azure 포털에서에서 Azure 검색 서비스 관리
> [!div class="op_single_selector"]
> * [포털](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Azure Search는 사용자 지정 앱에 풍부한 검색 환경을 구축하기 위해 사용되는 완전히 관리되는 클라우드 기반 검색 서비스입니다. 이 문서에서는 hello *관리 서비스* hello에서 수행할 수 있는 작업 [Azure 포털](https://portal.azure.com) 이미 프로 비전 하는 검색 서비스에 대 한 합니다. *관리 서비스* 기본적으로 작업을 수행 하는 제한 된 toohello 간단 합니다.

* 관리 하 고 보안 액세스 toohello *api-key* tooyour 서비스 읽기 또는 쓰기 액세스를 위해 사용 합니다.
* 파티션과 복제본의 hello 할당을 변경 하 여 서비스 용량을 조정 합니다.
* 서비스 계층의 상대 toomaximum 제한, 리소스 사용을 모니터링 합니다.

**이 문서에서 다루지 않는 내용** 

*콘텐츠 관리* (또는 인덱스 관리) toooperations 참조 검색 트래픽 toounderstand 대량 쿼리를 분석 하는 검색 및 얼마나 성공적인 검색 결과가 원래에 고객 toospecific 반영 되도록 사용자 단어는 검색 인덱스의 문서 수입니다. 이 영역에 대한 도움말은 [Azure Search를 위한 검색 트래픽 분석](search-traffic-analytics.md)을 참조하십시오.

*쿼리 성능이* 이 문서의 hello 다루지 이기도 합니다. 자세한 내용은 [사용 및 쿼리 메트릭 모니터링](search-monitor-usage.md) 및 [성능 및 최적화](search-performance-optimization.md)를 참조합니다.

*업그레이드*는 관리 작업이 아닙니다. Hello 서비스 프로 비전 될 때 리소스가 할당 되므로 새 서비스 이동 tooa 다른 계층에 필요 합니다. 자세한 내용은 [Azure Search 서비스 만들기](search-create-service-portal.md)를 참조하세요.

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>관리자 권한
Azure 구독 관리자 또는 공동 관리자가 프로 비전 또는 hello 서비스 자체를 서비스 해제를 수행할 수 있습니다.

서비스 내에서 액세스 toohello 서비스 URL에 있는 모든 사용자 및 관리자 api 키에 대 한 읽기 / 쓰기 액세스 toohello 서비스가 됩니다. Hello 기능 tooadd를 제공 하는 읽기 / 쓰기 액세스, 삭제 또는 서버 개체를 포함 하 여 api 키, 인덱스, 인덱서, 데이터 원본, 일정 및 역할 할당을 통해 구현 수정 [RBAC 정의 된 역할](#rbac)합니다.

Azure 검색의 모든 사용자 상호 작용이 모드 중 하나에 포함: 읽기 / 쓰기 액세스 toohello 서비스 (관리자 권한) 또는 읽기 전용 액세스 toohello 서비스 (쿼리 권한). 자세한 내용은 참조 [hello api 키를 관리](#manage-keys)합니다.

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>관리 액세스에 대한 RBAC 역할 설정
Azure에서 제공 된 [글로벌 역할 기반 권한 부여 모델](../active-directory/role-based-access-control-configure.md) hello 포털 또는 리소스 관리자 Api를 통해 관리 되는 모든 서비스에 대 한 합니다. 소유자, 참가자 및 독자 역할에는 Active Directory 사용자, 그룹 및 보안 주체 tooeach 할당 된 역할에 대 한 서비스 관리 hello 수준을 결정합니다. 

Azure 검색에 대 한 RBAC 사용 권한을 관리 작업을 수행 하는 hello를 결정 합니다.

| 역할 | 작업 |
| --- | --- |
| 소유자 |만들거나 hello 서비스 또는 api 키, 인덱스, 인덱서, 인덱서 데이터 원본 및 인덱서 일정을 포함 하는 hello 서비스에서 개체를 삭제 합니다.<p>개수 및 저장소 크기를 포함하여 서비스 상태를 봅니다.<p>역할 멤버 자격을 추가하거나 삭제합니다(소유자만 역할 멤버 자격을 관리할 수 있음).<p>구독 관리자와 서비스 소유자 hello 소유자 역할에 자동 구성원 자격이 있어야 합니다. |
| 참여자 |RBAC 역할 관리를 제외하고 소유자와 같은 수준의 액세스 권한입니다. 예를 들어, 참여자는 `api-key`를 보고 다시 생성할 수 있지만 역할 멤버 자격을 수정할 수 없습니다. |
| 리더 |서비스 상태와 쿼리 키를 봅니다. 이 역할의 멤버는 서비스 구성을 변경할 수 없고 관리 키도 볼 수 없습니다. |

역할은 액세스 권한 toohello 서비스 끝점을 부여 하지 마세요. 인덱스 관리, 인덱스 채우기 및 검색 데이터 쿼리와 같은 검색 서비스 작업은 역할이 아니라 api-key를 통해 제어합니다. 자세한 내용은 [역할 기반 액세스 제어](../active-directory/role-based-access-control-what-is.md)에서 "관리 및 데이터 작업에 대한 권한 부여"를 참조하세요.

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>로깅 및 시스템 정보
Azure 검색 hello 포털 또는 프로그래밍 인터페이스를 통해 개별 서비스에 대 한 로그 파일을 노출 하지 않습니다. Hello 기본 계층에서 한 위에 Microsoft 서비스 수준 계약 (SLA) 당 99.9%의 가용성에 대 한 모든 Azure 검색 서비스를 모니터링합니다. Hello 서비스가 느립니다 요청 처리량 SLA 임계값 미만으로 떨어질 경우 지원 팀 hello 로그 파일 사용 가능한 toothem 및 주소 hello 문제를 검토 합니다.

서비스에 대 한 일반 정보를 기준으로 다음 방법으로 hello에 대 한 정보를 얻을 수 있습니다.

* 알림, 속성 및 상태 메시지를 통해 hello 서비스 대시보드에서 hello 포털에서
* 사용 하 여 [PowerShell](search-manage-powershell.md) 또는 hello [관리 REST API](https://docs.microsoft.com/rest/api/searchmanagement/) 너무[서비스 속성 가져오기](https://docs.microsoft.com/rest/api/searchmanagement/services), 또는 인덱스 리소스 사용에 대 한 상태입니다.
* 이전에 설명한 것처럼 [검색 트래픽 분석](search-traffic-analytics.md)을 통해 정보를 얻습니다.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>api-key 관리
모든 요청 tooa 검색 서비스가 서비스에 대해 특별히 생성 된 api-키가 필요 합니다. 이 api 키는 액세스 tooyour 검색 서비스 끝점을 인증 하기 위한 hello 유일한 메커니즘입니다. 

api-key는 임의로 생성된 숫자 및 문자로 구성된 문자열입니다. 통해 [RBAC 사용 권한을](#rbac), 삭제 하거나 hello 키를 읽을 수 있지만 사용자 정의 암호로 키를 바꿀 수 없습니다. 

두 가지 유형의 키 검색 서비스 tooaccess 사용된 됩니다.

* 관리 (hello 서비스에 대 한 읽기 / 쓰기 작업에 대해 유효함)
* 쿼리(인덱스에 대한 쿼리와 같은 읽기 전용 작업에 유효)

관리자 api 키 hello 서비스 프로 비전 될 때 생성 됩니다. 로 지정 된 두 개의 관리자 키가 *기본* 및 *보조* tookeep 직선, 하지만 실제로 사용이 가능 합니다. 각 서비스를 롤백할 수 있습니다 하나를 통해 액세스 tooyour 서비스 그대로 유지 하면서 두 개의 관리 키에 있습니다. 두 관리자 키를 다시 생성할 수 있지만 toohello 총 관리자 키 수를 추가할 수 없습니다. 검색 서비스당 최대 두 개의 관리 키가 있습니다.

쿼리 키는 검색을 직접 호출하는 클라이언트 응용 프로그램을 위해 설계되었습니다. Too50 쿼리 키를 만들 수 있습니다. 응용 프로그램 코드에서 hello 검색 URL과 쿼리 api 키 tooallow 읽기 전용 액세스 toohello 서비스를 지정합니다. 응용 프로그램 코드는 또한 응용 프로그램에서 사용 하는 hello 인덱스를 지정 합니다. 함께 hello 끝점 읽기 전용 액세스 및 대상 인덱스에 대 한 api 키 hello 연결 클라이언트 응용 프로그램에서 hello 범위 및 액세스 수준을 정의 합니다.

tooget 또는 regenerate api-key를 열기 hello 서비스 대시보드 합니다. 클릭 **키** tooslide hello 키 관리 페이지를 엽니다. 다시 생성 하거나 키 만들기에 대 한 hello hello 페이지 위쪽에 있습니다. 기본적으로 관리 키만 만들어집니다. 쿼리 api-key를 수동으로 만들어야 합니다.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>api-key 보안
주요 보안 hello 포털 또는 리소스 관리자 인터페이스 (PowerShell 또는 명령줄 인터페이스)를 통해 액세스를 제한 하 여 보장 됩니다. 설명한 것처럼 구독 관리자는 모든 api-key를 보고 다시 생성할 수 있습니다. 예방 조치로 서 액세스 toohello 관리자 키를 가진 역할 할당 toounderstand를 검토 합니다.

1. Hello 서비스 대시보드에서 hello 액세스 아이콘 tooslide 열기 hello 사용자 블레이드를 클릭 합니다.
   ![][7]
2. 사용자에서 기존 역할 할당을 검토합니다. 예상 대로 구독 관리자에 대 한 모든 권한을 toohello 서비스 hello 소유자 역할을 통해 이미 있는 합니다.
3. 또한 toodrill 클릭 **구독 관리자** 검색 서비스에서 공동 관리 권한이 있는 hello 역할 할당 목록을 toosee를 차례로 확장 합니다.

또 다른 방법은 tooview 액세스 권한을 tooclick **역할** hello 사용자 블레이드의 합니다. 이렇게 하면 사용 가능한 역할 및 사용자 또는 그룹 할당 된 tooeach 역할 hello 수 표시 됩니다.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>리소스 사용 모니터링
Hello 대시보드 리소스 모니터링은 hello 서비스를 쿼리하여 얻을 수 있는 몇 가지 사항과 hello 서비스 대시보드에 표시 되는 제한 된 toohello 정보입니다. Hello 서비스 대시보드에서 hello 사용 섹션은 응용 프로그램에 대 한 적절 한 파티션 리소스 수준을 있는지 신속 하 게 확인할 수 있습니다.

Hello 검색 서비스 API를 사용 하 여 문서 및 인덱스에 대 한 개수를 가져올 수 있습니다. hello 가격 책정 계층에 따라이 개수와 연결 된 하드 제한이 있습니다. 자세한 내용은 [검색 서비스 제한](search-limits-quotas-capacity.md)을 참조하세요. 

* [인덱스 통계 가져오기](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [문서 수 계산](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> 캐싱 동작 때문에 한도가 일시적으로 과장될 수 있습니다. 예를 들어 hello 공유 서비스를 사용할 때 표시 될 수 있습니다는 문서 수의 10, 000 문서 hello 하드 제한 초과 합니다. hello 과장은 임시적 이며 hello 다음 제한이 적용 검사에서 검색 됩니다. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>재해 복구 및 서비스 중단

데이터를 복원할 수 우리, 하지만 hello 클러스터 또는 데이터 센터 수준에서 중단 되는 경우 Azure 검색 hello 서비스의 즉각적인 장애 조치가 제공 하지 않습니다. Hello 데이터 센터에서 실패 하면 클러스터 hello 운영 팀에서는 검색 하 고 작업 toorestore 서비스입니다. 서비스를 복원하는 동안 가동 중지가 발생할 수 있습니다. 서비스 크레딧 toocompensate hello 당 서비스 가용성을 요청할 수 있습니다 [서비스 수준 계약 (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/)합니다. 

Microsoft의 컨트롤 외부에서 치명적 오류의 hello 이벤트에서 지속적인 서비스에 필요한 경우 수 [추가 서비스를 프로 비전](search-create-service-portal.md) 다른 지역 및 구현에 지리적 복제 전략 tooensure 인덱스 모든 서비스에서 완전 한 중복 됩니다.

사용 하 여 고객 [인덱서](search-indexer-overview.md) toopopulate 및 새로 고침 인덱스 hello를 활용 하 여 특정 지역 인덱서를 통해 재해 복구를 처리할 수 있는 동일한 데이터 원본입니다. 각는 인덱서를 실행 하는 서로 다른 지역에 있는 두 서비스 수에서 인덱스 hello 동일한 데이터 원본 tooachieve 지리적 중복 됩니다. 지역 중복 데이터 원본에서 인덱싱하는 경우 Azure Search 인덱서는 주 복제본에서만 증분 인덱싱을 수행할 수 있습니다. 장애 조치 이벤트가 있는지 toore 지점 hello 인덱서 toohello 새로운 주 복제본 수입니다. 

인덱서를 사용 하지 않는 경우에 동시에 응용 프로그램 코드 toopush 개체와 데이터 toodifferent 검색 서비스를 사용 합니다. 자세한 내용은 [Azure Search에서 성능 및 최적화](search-performance-optimization.md)를 참조하세요.

## <a name="backup-and-restore"></a>백업 및 복원

Azure Search는 기본 데이터 저장소 솔루션이 아니므로 셀프 서비스 백업 및 복원에 대한 공식적인 메커니즘을 제공하지 않습니다. 인덱스를 실수로 삭제 하면 만들고 인덱스를 채우는 데 사용 하 여 응용 프로그램 코드는 hello 사실상 복원 옵션으로 지정 합니다. 

toorebuild 인덱스를 삭제 (있는 경우), hello 서비스에서 hello 인덱스를 다시 만드십시오 하는 주 데이터 저장소에서 데이터를 검색 하 여 다시 로드 합니다. 또는 교류할 수 너무[고객 지원]() toosalvage 지역 가동 중단 없는 경우를 인덱싱합니다.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>확장 또는 축소
모든 검색 서비스는 최소 복제본 한 개와 파티션 한 개로 시작됩니다. 등록 하지 않은 경우에 [전용된 리소스를 제공 하는 계층](search-limits-quotas-capacity.md), hello 클릭 **배율** hello 서비스 대시보드 tooadjust 리소스 사용량에 바둑판식으로 배열 합니다.

두 리소스를 통해 용량을 추가 하면 hello 서비스 사용을 자동으로 합니다. 추가 작업이 없으므로 필요 하지 않습니다, 하지만 약간의 지연이 전에 hello 새 리소스의 hello 영향 실현 됩니다. 이 지나야 15 분 또는 자세한 tooprovision 추가 리소스입니다.

 ![][10]

### <a name="add-replicas"></a>복제본 추가
QPS(초당 쿼리 수)를 높이거나 고가용성을 구현하려면 복제본을 추가합니다. 각 복제본에는 인덱스의 복사본이 두 개 있으므로 tooone 변환 하나 더 많은 복제본을 추가 서비스 쿼리 요청을 처리할 수 있는 더 많은 인덱스. 고가용성을 위해서는 복제본이 최소 3개 필요합니다(자세한 내용은 [용량 계획](search-capacity-planning.md) 을 참조하세요).

더 많은 복제본을 포함하는 검색 서비스는 쿼리 요청의 부하를 다수의 인덱스에 분산할 수 있습니다. 쿼리 볼륨의 수준이 제공 쿼리 처리량이 것 toobe 더 빠르게 더 많은 hello 인덱스 사용 가능한 tooservice hello 요청 복사본에 있는 경우입니다. 쿼리 대기 시간이 발생 하는 경우 추가 복제본 hello 온라인는 성능에 긍정적인 영향을 기대할 수 있습니다.

복제본을 추가한 것 처럼 쿼리 처리량 위로 올라가면서, 있지만 하지 정확 하 게 두 번 않거나 tooyour 서비스 복제본을 추가한 것 처럼 삼중 합니다. 모든 검색 응용 프로그램 제목 tooexternal 있는 요인이 쿼리 성능이 떨어질 수 있습니다. 복잡 한 쿼리 및 네트워크 대기 시간 toovariations 쿼리 응답 시간에 영향을 주는 두 개의 요소는입니다.

### <a name="add-partitions"></a>파티션 추가
대부분의 서비스 응용 프로그램에는 기본적으로 파티션보다 더 많은 수의 복제본이 필요합니다. 문서 수를 늘려야 하는 경우 표준 서비스에 등록했으면 파티션을 추가할 수 있습니다. 기본 계층은 추가 파티션을 제공하지 않습니다.

Hello 표준 계층에서는 파티션을 12의 배수로 추가 됩니다 (특히, 1, 2, 3, 4, 6, 또는 12). 이는 분할의 아티팩트입니다. 인덱스는 12개 분할로 만들어지며 모두 하나의 파티션에 저장되거나 2, 3, 4, 6 또는 12개 파티션(파티션당 하나의 분할)에 똑같이 나뉠 수 있습니다.

### <a name="remove-replicas"></a>복제본 제거
쿼리 볼륨이 많은 기간이 지나고 검색 쿼리 부하가 정규화되면(예: 휴일 할인이 종료된 후) 복제본을 줄일 수 있습니다.

toodo이, 이동 hello 복제본 슬라이더 백 tooa 낮은 값입니다. 필요한 추가 단계는 없습니다. Hello 데이터 센터의 가상 컴퓨터를 포기 lowering hello 복제본 수입니다. 이제 이전보다 적은 VM에서 쿼리 및 데이터 수집 작업이 실행됩니다. hello 최소 제한은 하나의 복제본입니다.

### <a name="remove-partitions"></a>파티션 제거
복제본을 위해 별도의 추가 작업 없이 필요한 제거 달리 줄일 수 있습니다 보다 많은 저장소를 사용 하는 경우 일부 작업 toodo가 있을 수 있습니다. 예를 들어 솔루션 3 개의 파티션과 사용 하는 경우 가짐 tooone 또는 두 개의 파티션이 오류가 발생 합니다는 hello 새 저장소 공간이 필요한 것 보다 작은 경우. 예상 대로 선택 사항을 toodelete 인덱스 또는 공간을 관련 된 인덱스가 toofree 내에서 문서 또는 hello 현재 구성을 유지 합니다.

특정 파티션에 저장되는 인덱스 분할을 알려주는 검색 방법은 없습니다. 각 파티션에 있는 파티션 hello 번호로 될 수 있는 tooreduce 저장소 tooa 크기 해야 하므로 25GB 저장소에서 제공 합니다. Toorevert tooone 파티션 하려는 경우 모든 12 개 분할 toofit이 필요 합니다.

향후 계획 toohelp, toocheck 저장소 할 수 있습니다 (사용 하 여 [인덱스 통계 가져오기](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee 실제로 사용 얼마나 합니다. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>규모 및 배포에 대한 모범 사례
이 30분 분량의 비디오는 지역으로 분산된 워크로드를 포함한 고급 배포 시나리오에 대한 모범 사례를 검토합니다. 볼 수 있습니다 [성능 및 Azure 검색에 최적화](search-performance-optimization.md) 도움말 페이지는 커버 hello에 대 한 동일한 가리킵니다.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>다음 단계
서비스 관리 hello 개념을 이해 하면 사용 하 여 고려 [PowerShell](search-manage-powershell.md) tooautomate 작업 합니다.

또한 좋습니다 hello 검토 [성능 및 최적화 문서](search-performance-optimization.md)합니다.

또 다른 권장은 toowatch hello 비디오 hello 이전 섹션에서 설명한 것입니다. 이 섹션에 언급 된 hello 기법 하위 수준 검사를 제공 합니다.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



