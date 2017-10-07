---
title: "aaaAzure 저장소 성능 및 확장성 검사 목록 | Microsoft Docs"
description: "성능이 뛰어난 응용 프로그램 개발 시 Azure 저장소에서 사용하기 위한 검증된 작업 방식에 대한 검사 목록."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 959d831b-a4fd-4634-a646-0d2c0c462ef8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2970c055d460070288d1810e4a77a7f056a4137
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-performance-and-scalability-checklist"></a>Microsoft Azure 저장소 성능 및 확장성 검사 목록
## <a name="overview"></a>개요
Hello Microsoft Azure 저장소 서비스의 hello 릴리스부터 Microsoft는 이러한 서비스를 사용 하 여 고성능 방식에서에 대 한 검증 된 사례 수를 개발 하며이 문서 역할 tooconsolidate hello 그 중 가장 중요 한 검사 목록 스타일 목록으로 합니다. 이 문서의 hello 위한 toohelp 응용 프로그램 개발자가 검증 된 사례를 사용 하 여 Azure 저장소 및 toohelp 채택 해야 다른 검증 된 사례를 식별 하는 확인입니다. 이 문서는 하지 toocover 모든 가능한 성능 및 확장성 최적화-미치는 영향이 작거나 광범위 하 게 적용할 수 있는 메서드를 제외 합니다. 이러한에 초기에 유의 하는 유용한 tookeep는 디자인 중 응용 프로그램의 동작을 hello toohello 익스텐트를 예측할 수 있는 성능 문제를 경험 합니다 tooavoid 디자인 합니다.  

Azure 저장소를 사용 하 여 모든 응용 프로그램 개발자 해야 hello 시간 tooread이이 문서 걸리고의 응용 프로그램의 hello 검증 된 사용법 아래에 나열 된 각을 따르는지 확인 하십시오.  

## <a name="checklist"></a>검사 목록
이 문서는 hello 그룹을 다음으로 입증 된 hello 사례를 구성 합니다. 검증된 작업 방식이 적용되는 대상은 다음과 같습니다.  

* 모든 Azure 저장소 서비스(Blob, 테이블, 큐, 파일)
* Blob
* 테이블
* 큐  

| 완료된 | 영역 | Category | 질문 |
| --- | --- | --- | --- |
| &nbsp; | 모든 서비스 |확장성 목표 |[설계 된 응용 프로그램 tooavoid 근접 하 고 확장성 목표 hello?](#subheading1) |
| &nbsp; | 모든 서비스 |확장성 목표 |[프로그램 명명 규칙 설계 tooenable 낫거나 부하 분산?](#subheading47) |
| &nbsp; | 모든 서비스 |네트워킹 |[클라이언트 쪽 장치 충분히 높은 대역폭 및 대기 시간이 짧은 tooachieve hello 성능 필요한 해야 합니까?](#subheading2) |
| &nbsp; | 모든 서비스 |네트워킹 |[클라이언트 쪽 장치의 링크 품질이 충분히 높습니까?](#subheading3) |
| &nbsp; | 모든 서비스 |네트워킹 |[클라이언트 응용 프로그램 hello 가까이 "" hello 저장소 계정?](#subheading4) |
| &nbsp; | 모든 서비스 |콘텐츠 배포 |[콘텐츠 배포를 위해 CDN을 사용합니까?](#subheading5) |
| &nbsp; | 모든 서비스 |직접 클라이언트 액세스 |[프록시 대신 SAS 및 CORS tooallow 직접 액세스 toostorage을 사용 하 고 있습니까?](#subheading6) |
| &nbsp; | 모든 서비스 |구성 |[응용 프로그램에서 반복적으로 사용되며 거의 변경되지 않는 데이터를 캐시합니까?](#subheading7) |
| &nbsp; | 모든 서비스 |구성 |[응용 프로그램에서 업데이트를 일괄 처리(클라이언트 쪽에서 업데이트를 캐시한 다음 더 큰 집합으로 업로드)합니까?](#subheading8) |
| &nbsp; | 모든 서비스 |.NET 구성 |[동시 연결 수가 충분 하 여 클라이언트 toouse 구성 했습니까?](#subheading9) |
| &nbsp; | 모든 서비스 |.NET 구성 |[.NET toouse 충분 한 수의 스레드 구성 했습니까?](#subheading10) |
| &nbsp; | 모든 서비스 |.NET 구성 |[가비지 수집 기능이 개선된 .NET 4.5 이상을 사용 중입니까?](#subheading11) |
| &nbsp; | 모든 서비스 |병렬 처리 |[클라이언트 기능 또는 hello 확장성 목표를 오버 로드 하지 않는 있도록 병렬 처리 수준 적절 하 게 제한 확인 게?](#subheading12) |
| &nbsp; | 모든 서비스 |도구 |[클라이언트 라이브러리 및 도구를 제공 된 최신 버전의 Microsoft hello를 사용 하 여 하나요?](#subheading13) |
| &nbsp; | 모든 서비스 |다시 시도 |[제한 시간 및 오류 제한을 위한 지수 백오프 다시 시도 정책을 사용하고 있습니까?](#subheading14) |
| &nbsp; | 모든 서비스 |다시 시도 |[응용 프로그램에서 다시 시도할 수 없는 오류 발생 시에는 작업을 다시 시도하지 않습니까?](#subheading15) |
| &nbsp; | Blob |확장성 목표 |[동시에 단일 개체에 액세스하는 클라이언트가 많이 있습니까?](#subheading46) |
| &nbsp; | Blob |확장성 목표 |[단일 blob에 대 한 hello 대역폭 또는 작업 확장성 목표 내에서 남아 있는 경우 응용 프로그램?](#subheading16) |
| &nbsp; | Blob |Blob 복사 |[Blob를 효율적으로 복사하고 있습니까?](#subheading17) |
| &nbsp; | Blob |Blob 복사 |[대량 Blob 복사에 AzCopy를 사용하고 있습니까?](#subheading18) |
| &nbsp; | Blob |Blob 복사 |[Azure 가져오기/내보내기 tootransfer 매우 많은 양의 데이터를 사용 중 인가요?](#subheading19) |
| &nbsp; | Blob |메타데이터 사용 |[자주 사용되는 Blob 관련 메타데이터를 해당 메타데이터에 저장하고 있습니까?](#subheading20) |
| &nbsp; | Blob |고속 업로드 |[Tooupload blob 하나를 신속 하 게 시도할 때 동시에 블록을 업로드 하 시겠습니까?](#subheading21) |
| &nbsp; | Blob |고속 업로드 |[를 시도할 때 tooupload 많은 blob 신속 하 게 병렬에서 blob 업로드 하려는?](#subheading22) |
| &nbsp; | Blob |올바른 Blob 유형 |[해당하는 경우 페이지 Blob 또는 블록 Blob를 사용합니까?](#subheading23) |
| &nbsp; | 테이블 |확장성 목표 |[초당 엔터티에 대 한 있습니다 근접 hello 확장성 목표?](#subheading24) |
| &nbsp; | 테이블 |구성 |[테이블 요청에 JSON을 사용하고 있습니까?](#subheading25) |
| &nbsp; | 테이블 |구성 |[하면 해제 한 Nagle 작은 요청의 tooimprove hello 성능을?](#subheading26) |
| &nbsp; | 테이블 |테이블 및 파티션 |[데이터를 적절하게 분할했습니까?](#subheading27) |
| &nbsp; | 테이블 |핫 파티션 |[추가 전용 및 앞에 추가 전용 패턴을 지양하고 있습니까?](#subheading28) |
| &nbsp; | 테이블 |핫 파티션 |[여러 파티션을 대상으로 삽입/업데이트를 수행합니까?](#subheading29) |
| &nbsp; | 테이블 |쿼리 범위 |[대부분의 경우 및 제한적으로 사용 하는 테이블 쿼리 toobe에 사용 된 지점 쿼리 toobe 프로그램 스키마 tooallow 디자인?](#subheading30) |
| &nbsp; | 테이블 |쿼리 밀도 |[일반적으로 쿼리가 응용 프로그램에서 사용할 행만 스캔하여 반환합니까?](#subheading31) |
| &nbsp; | 테이블 |반환되는 데이터 제한 |[필요 하지 않은 필터링 tooavoid 반환 엔터티 사용 중 인가요?](#subheading32) |
| &nbsp; | 테이블 |반환되는 데이터 제한 |[필요 하지 않은 속성을 반환 하는 프로젝션 tooavoid 사용 중 인가요?](#subheading33) |
| &nbsp; | 테이블 |비정규화 |[있어야 하면 비 정규화 된 데이터 tooget 데이터 하려고 할 때 비효율적인 쿼리 또는 여러 읽기 요청 방지 되도록?](#subheading34) |
| &nbsp; | 테이블 |삽입/업데이트/삭제 |[에 수행할 수 있습니다 hello 동일 또는 toobe를 트랜잭션 필요 여부를 지정 하는 요청을 일괄 처리는 tooreduce 왕복 시간?](#subheading35) |
| &nbsp; | 테이블 |삽입/업데이트/삭제 |[엔터티 정당한 toodetermine 검색 방지는 toocall 삽입 또는 업데이트 여부?](#subheading36) |
| &nbsp; | 테이블 |삽입/업데이트/삭제 |[자주 함께 검색할 일련의 데이터를 여러 엔터티가 아닌 단일 엔터티에 속성으로 저장하는 것을 고려한 적이 있습니까?](#subheading37) |
| &nbsp; | 테이블 |삽입/업데이트/삭제 |[배치로 쓸 수 있으며 항상 함께 검색할 엔터티(예: 시계열 데이터)에 대해 테이블이 아닌 Blob 사용을 고려한 적이 있습니까?](#subheading38) |
| &nbsp; | 큐 |확장성 목표 |[초당 메시지 수 근접 hello 확장성 목표는 되나요?](#subheading39) |
| &nbsp; | 큐 |구성 |[하면 해제 한 Nagle 작은 요청의 tooimprove hello 성능을?](#subheading40) |
| &nbsp; | 큐 |메시지 크기 |[Compact tooimprove hello 성능 hello 큐의 메시지에는?](#subheading41) |
| &nbsp; | 큐 |대량 검색 |[단일 "Get" 작업으로 여러 메시지를 검색합니까?](#subheading42) |
| &nbsp; | 큐 |폴링 빈도 |[응용 프로그램의 대기 시간을 인식 부족 tooreduce hello 자주 폴링하면?](#subheading43) |
| &nbsp; | 큐 |메시지 업데이트 |[사용 중 인가요 UpdateMessage toostore 진행률 메시지 처리에서에서 오류가 발생 한 경우 tooreprocess hello에 대 한 전체 메시지를 것?](#subheading44) |
| &nbsp; | 큐 |아키텍처 |[사용 하 고 큐 toomake 확장성이 뛰어난 응용 프로그램 전체를 유지 하 여 하지 hello 중요 한 경로 및 스케일 아웃 장기 실행 작업 후 독립적으로?](#subheading45) |

## <a name="allservices"></a>모든 서비스
이 섹션의 hello Azure 저장소 서비스 (blob, 테이블, 큐 또는 파일)의 적용 가능한 toohello 사용 하는 검증 된 사례를 나열 합니다.  

### <a name="subheading1"></a>확장성 목표
Hello Azure 저장소 서비스의 각 용량 (GB), 트랜잭션 속도 및 대역폭에 대 한 확장성 목표에 있습니다. 응용 프로그램에 도달 하거나 한 hello 확장성 목표를 초과, 증가 된 트랜잭션 대기 시간 또는 조정이 발생할 수 있습니다. 저장소 서비스 응용 프로그램을 제한, tooreturn "503 서버 사용 중" 또는 "500 작업 시간 초과" 오류 코드 일부 저장소 트랜잭션에 대 한 hello 서비스를 시작 합니다. 이 섹션에서는 특히 두 hello 일반적인 방법을 toodealing 확장성 목표와 대역폭 확장성 목표를 설명 합니다. 개별 저장소 서비스를 처리 하는 이후 섹션에서는 특정 서비스의 hello 컨텍스트에서 확장성 목표를 설명 합니다.  

* [Blob 대역폭 및 초당 요청 수](#subheading16)
* [초당 테이블 엔터티 수](#subheading24)
* [초당 큐 메시지 수](#subheading39)  

#### <a name="sub1bandwidth"></a>모든 서비스에 대한 대역폭 확장성 목표
작성 hello 시 hello 대역폭 목표 hello 미국 지역 중복 저장소 (GRS)에 대 한 계정에는 10 기가 비트 / 초 (Gbps) 수신에 대 한 (데이터 전송 됨 toohello 저장소 계정) 및 송신 (hello 저장소 계정에서 보낸 데이터)에 대 한 20 g b p s. 로컬 중복 저장소 (LRS) 계정에 대 한 hello 제한은 더 높은 – ingress 및 egress에 대 한 30 g b p s에 대 한 20 g b p s.  기타 국가의 대역폭 제한은 이보다 더 낮을 수 있습니다. 관련 정보는 [확장성 목표 페이지](http://msdn.microsoft.com/library/azure/dn249410.aspx)에서 확인할 수 있습니다.  Hello 저장소 중복 옵션에 대 한 자세한 내용은 hello 링크를 참조 하십시오 [유용한 리소스](#sub1useful) 아래 합니다.  

#### <a name="what-toodo-when-approaching-a-scalability-target"></a>확장성 목표에 도달할 때 어떤 toodo
응용 프로그램이 단일 저장소 계정에 대 한 hello 확장성 목표에 도달 하 고, 경우에 hello 다음 방법 중 하나를 채택 하는 것이 좋습니다.  

* 응용 프로그램 tooapproach 시키는 hello 작업을 다시 고려할 또는 hello 확장성 목표를 초과 합니다. 수 디자인 다르게 대역폭 또는 용량 또는 더 적은 수의 트랜잭션을 덜 toouse?
* 응용 프로그램 해야 hello 확장성 목표 중 하나를 초과 하는 경우 만들어야 여러 저장소 계정 및 파티션 응용 프로그램 데이터는 여러 저장소 계정에서 합니다. 이 패턴을 사용 하는 경우 다음 수 있는지 toodesign 응용 프로그램 부하 분산에 대 한 이후 hello에 저장소 계정을 더 추가할 수 있습니다. 작성 시점에 각 Azure 구독 too100 저장소 계정이 있을 수 있습니다.  또한 저장소 계정에는 저장하거나 전송하는 데이터 또는 수행하는 트랜잭션과 관련된 사용 요금 외의 기타 비용은 없습니다.
* 응용 프로그램 hello 대역폭 목표에 도달 하는 경우에 hello 클라이언트 tooreduce hello 필요한 대역폭 toosend hello 데이터 toohello 저장소 서비스에 데이터를 압축 하는 것이 좋습니다.  이렇게 하면 대역폭을 줄이고 네트워크 성능을 개선할 수는 있지만, 몇 가지 좋지 않은 영향도 있을 수 있습니다.  압축 및 압축 해제 하는 클라이언트 hello에에서 데이터 추가 처리 요구 사항 toohello 인해이 hello 성능 영향을 평가 해야 합니다. 또한 압축 된 데이터를 저장 하기가 더 어려운 tootroubleshoot 문제의 표준 도구를 사용 하 여 더 어렵게 tooview 저장 된 데이터를 될 수 없습니다.
* 응용 프로그램 hello 확장성 목표에 도달 하는 경우의 재시도 대 한 지 수 백오프를 사용 하 고 있는지 확인 합니다 (참조 [재시도](#subheading14)).  더 나은 toomake (사용 하 여 hello 위에 메서드 중 하나), hello 확장성 목표를 접근 하지 하지만 이렇게 하면 응용 프로그램에 있는지 유지 방금 신속 하 게 다시 시도, hello 나빠지는 제한 하 하지 않습니다.  

#### <a name="useful-resources"></a>유용한 리소스
링크를 따라 hello 확장성 목표에 추가 세부 정보를 제공 합니다.

* 확장성 목표에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) 를 참조하세요.
* 참조 [Azure 저장소 복제](storage-redundancy.md) hello 블로그 게시물 및 [Azure 저장소 중복 옵션 및 읽기 액세스 지역 중복 저장소](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx) 저장소 중복 옵션에 대 한 정보에 대 한 합니다.
* Azure 서비스 가격에 대한 최신 정보는 [Azure 가격 책정](https://azure.microsoft.com/pricing/overview/)을 참조하세요.  

### <a name="subheading47"></a>파티션 명명 규칙
Azure 저장소는 범위 기반 파티션 구성표 tooscale 및 부하 분산 hello 시스템을 사용합니다. hello 파티션 키는 toopartition 사용 되는 데이터를 범위로 하 고 이러한 범위는 부하 분산 된 hello 시스템 전체에서입니다. 즉, 어휘 (예: msftpayroll, msftperformance, msftemployees 등)을 순서 지정 또는 타임 스탬프 (log20160101, log20160102, log20160102 등)를 사용 하 여 같은 명명 규칙은 hello에 공동 배치할 잠재적으로 되 고 toohello 파티션에 적합 같은 파티션 서버에 부하 분산 작업을 더 작은 범위로 해당 분할 될 때까지 합니다. 예를 들어 hello 이러한 blob에 대 한 부하 필요로 할 때까지 추가 작업 재 분산 hello 파티션 범위 컨테이너 내 모든 blob 단일 서버에 의해 제공 될 수 있습니다. 마찬가지로, 어휘 순서로 정렬 된 해당 이름으로 부하가 적은 계정의 그룹에서 연결할 수 있습니다는 단일 서버 hello까지 하나에서 로드 하거나 이러한 계정을 모두 필요한 toobe 분할 여러 파티션 서버입니다. Hello 작업 중 각 부하 분산 작업에서 저장소 호출의 hello 대기 시간 영향을 줄 수 있습니다. 트래픽 tooa 파티션의 갑자기 버스트 hello 로드 작업을 균형 조정 될 때까지 hello 확장성 단일 분할 서버에 의해 제한 되는 hello 시스템의 기능 toohandle 작동 기능 및 hello 파티션 키 범위를 변경 합니다.  

이러한 작업의 몇 가지 모범 사례 tooreduce hello 주파수를 따를 수 있습니다.  

* 계정, 컨테이너, blob, 테이블 및 큐에 대 한 밀접 하 게 사용 하는 hello 명명 규칙을 검사 합니다. 계정 이름에 요구 사항에 가장 적합한 해싱 함수를 사용하는 3자릿수 해시의 접두사를 추가해 보십시오.  
* 타임 스탬프 또는 사이의 숫자 식별자를 사용 하 여 데이터를 구성 하는 경우 추가 전용 (또는 앞 으로만 이동 가능한) 트래픽 패턴을 사용 하지 않는 tooensure를 해야 합니다. 이러한 패턴은 범위에 적합 하지 않은-기반의 시스템, 분할 및 수 리드 tooall hello 트래픽 하락 tooa 단일 파티션 및 제한 hello 시스템에서 효과적으로 부하 분산 합니다. 예를 들어, 매일 있으면 일일 작업에 대 한 다음 모든 hello 트래픽 yyyymmdd 같은 타임 스탬프를 갖는 blob 개체를 사용 하는 작업 전송 tooa 단일 분할 서버에 의해 제공 되는 단일 개체. Hello blob 당 제한 여부를 확인 하 고 파티션당 제한 요구 사항을 충족 하 고 필요한 경우 여러 blob으로이 작업을 분할 하는 것이 좋습니다. 합니다. 마찬가지로, 테이블의 시계열 데이터를 저장 하는 경우 모든 hello 트래픽을 수 toohello hello 키 네임 스페이스의 마지막 부분을 이동 합니다. 타임 스탬프 또는 숫자 Id를 사용 해야 하는 경우 3 자리 해시 또는 ssyyyymmdd 같은 hello 시간의 타임 스탬프 hello 초 부분을 접두사의 경우 hello hello id를 접두사입니다. 열거 및 쿼리 작업을 일상적으로 수행하는 경우 쿼리 수를 제한하는 해시 함수를 선택합니다. 다른 경우에는 임의의 접두사로도 충분할 수 있습니다.  
* Azure 저장소에 사용 되는 체계를 분할 하는 hello에 대 한 자세한 내용은 hello SOSP 문서를 읽을 [여기](http://sigops.org/sosp/sosp11/current/2011-Cascais/printable/11-calder.pdf)합니다.

### <a name="networking"></a>네트워킹
Hello API 문제를 호출 하는 동안 hello 응용 프로그램의 실제 네트워크 제한 종종 hello 성능에 상당한 영향을는. hello 다음 사용자가 발생할 수는 제한 사항 중 일부를 설명 합니다.  

#### <a name="client-network-capability"></a>클라이언트 네트워크 기능
##### <a name="subheading2"></a>처리량
대역폭, hello 문제는 종종 hello 클라이언트의 hello 기능입니다. 예를 들어, 단일 저장소 계정의 10gbps 이상 ingress 처리할 수 하는 동안 (참조 [대역폭 확장성 목표](#sub1bandwidth)), "Small" Azure 작업자 역할 인스턴스에서 hello 네트워크 속도 약 100 개의 Mbps 수만 있습니다. 대규모 Azure 인스턴스에는 용량이 더 많은 NIC가 포함되므로 컴퓨터 하나의 네트워크 제한을 높여야 하는 경우에는 더 큰 인스턴스나 더 많은 VM을 사용하는 것이 좋습니다. 온-프레미스 응용 프로그램에서 저장소 서비스를 액세스 하는 경우 hello 동일한 규칙이 적용 됩니다: hello 클라이언트 장치 및 네트워크 연결 toohello hello Azure 저장소 위치 hello 네트워크 기능을 이해 하 고 보다 개선 필요에 따라 또는 기능 내에서 응용 프로그램 toowork 프로그램을 디자인 합니다.  

##### <a name="subheading3"></a>링크 속도
네트워크를 어떤 방식으로 사용하든 네트워크의 상태로 인해 오류와 패킷 손실이 발생하면 효율적인 처리량을 달성하는 시간이 길어집니다.  WireShark 또는 NetMon을 사용하면 이 문제를 진단하는 데 도움이 될 수 있습니다.  

##### <a name="useful-resources"></a>유용한 리소스
가상 컴퓨터 크기 및 할당된 대역폭에 대한 자세한 내용은 [Windows VM 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Linux VM 크기](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.  

#### <a name="subheading4"></a>위치
모든 분산된 환경에서 최상의 성능을 얻으려면 hello에 전달 hello 클라이언트 toohello 서버 근처에 배치 합니다. 대기 시간이 가장 하는 hello 사용 하 여 Azure 저장소 액세스에 대 한 hello 내 클라이언트에 대 한 hello 가장 좋은 위치는 동일한 Azure 지역에 있습니다. 예를 들어 Azure 웹 사이트에서 Azure 저장소를 사용하는 경우 웹 사이트와 저장소를 모두 단일 하위 지역(예: 미국 서부 또는 동남 아시아) 내에 배치해야 합니다. 이렇게 하면 hello 대기 시간 및 hello 비용 감소-쓰기의 hello 시 단일 지역 내 대역폭 사용량은 무료입니다.  

응용 프로그램 호스트 되지 Azure 내에서 (모바일 장치 앱 같은 또는 프레미스 엔터프라이즈 서비스), 그리고 클라이언트 대기 시간 일반적으로 인해 됩니다 hello 저장소 계정, 액세스 하는 toohello 장치 가까이 지역에 배치 합니다. 클라이언트가 일부는 북아메리카에 있고 일부는 유럽에 있는 등 광범위하게 분산되어 있다면 여러 저장소 계정(하나는 북아메리카 지역에 있고 하나는 유럽 지역에 있음)을 사용해야 합니다. 이 두 지역에서 사용자에 대 한 대기 시간 tooreduce 도움이 됩니다. 이 방법은 일반적으로 더 쉽게 tooimplement 경우 hello hello 응용 프로그램 데이터 저장소 연결이 특정 tooindividual 사용자 저장소 계정 간에 데이터를 복제 하지 않아도 됩니다.  광범위 한 콘텐츠 배포를 위해 CDN을 사용 하는 것이 좋습니다-hello에 대 한 자세한 내용은 다음 섹션을 참조 합니다.  

### <a name="subheading5"></a>콘텐츠 배포
경우에 따라 하나에 있는 동일한 콘텐츠 toomany 사용자 (예:: 웹 사이트의 hello 홈 페이지에서 사용 되는 비디오 데모 제품)가 하는 응용 프로그램 요구 tooserve hello hello 동일 또는 여러 영역입니다. 이 시나리오에서 CDN 콘텐츠 배달 네트워크 () 같은 Azure CDN을 사용 해야 하 고 hello CDN은 hello hello 데이터 원본으로 Azure 저장소를 사용 합니다. 단일 지역에 존재 하 고 tooother 영역 짧은 대기 시간으로 콘텐츠를 제공 없습니다 하는 Azure 저장소 계정, 달리 Azure CDN hello 전 세계 여러 데이터 센터에서 서버를 사용 합니다. 또한 CDN은 일반적으로 단일 저장소 계정보다 더 높은 송신 제한을 지원합니다.  

Azure CDN에 대한 자세한 내용은 [Azure CDN](https://azure.microsoft.com/services/cdn/)을 참조하세요.  

### <a name="subheading6"></a>SAS 및 CORS 사용
Azure 저장소에서 휴대폰 앱 tooaccess 데이터 또는 사용자의 웹 브라우저에서 JavaScript 같은 tooauthorize 코드 필요한 경우 한 가지 방법은 toouse 프록시로 웹 역할에서 응용 프로그램: hello 사용자의 장치 설정에 hello 웹 역할을 사용 하 여 인증 hello 저장소 서비스를 인증합니다. 이러한 방식을 사용하면 안전하지 않은 장치에서 저장소 계정 키가 노출되는 상황을 방지할 수 있습니다. 그러나 이렇게 하면 큰 오버 헤드가 hello 웹 역할에서 모든 hello 데이터 hello 사용자의 장치 간에 전송 되 고 hello 저장소 서비스를 통과 해야 hello 웹 역할입니다. 사용 하 여 웹 역할을 프록시로 hello 저장소 서비스에 대 한 공유 액세스 서명 (SAS) 경우에 따라 헤더 크로스-원본 자원 공유 (CORS)와 함께에서 사용 하 여 방지할 수 있습니다. SAS를 사용 하 여 사용자의 장치 toomake tooa 저장소 서비스는 제한 된 액세스 토큰을 사용 하 여 직접 요청을 허용할 수 있습니다. 예를 들어 사용자가 tooupload 사진 tooyour 응용 프로그램을 웹 역할 수 생성 되 고 toohello 사용자의 장치 (지나면 hello SAS 토큰에 만료) 30 분간 권한 toowrite tooa 특정 blob 이나 hello에 대 한 컨테이너를 부여 하는 SAS 토큰을 보냅니다.

일반적으로 브라우저 "PUT" tooanother 도메인과 같은 하나의 도메인 tooperform 특정 작업에 대 한 웹 사이트에서 호스팅되는 페이지에서 JavaScript를 허용 하지 않습니다. 예를 들어 "contosomarketing.cloudapp.net"와 원하는 toouse 클라이언트 쪽 JavaScript tooupload "contosoproducts.blob.core.windows.net"에서 blob tooyour 저장소 계정에서 웹 역할을 호스트 하는 경우 브라우저의 hello "동일 원본 정책" 반해 됩니다 작업입니다. CORS는 hello 대상 도메인 (이 경우 hello 저장소 계정)에서 toocommunicate toohello 브라우저 트러스트 요청 hello 원본 도메인 (이 경우 hello 웹 역할)에서 발생 하는 수 있는 브라우저 기능입니다.  

이 두 기술을 사용하면 웹 응용 프로그램에서 불필요한 로드와 병목 현상을 방지할 수 있습니다.  

#### <a name="useful-resources"></a>유용한 리소스
SAS에 대 한 자세한 내용은 참조 [공유 액세스 서명, 1 부: SAS 모델 이해 hello](../storage-dotnet-shared-access-signature-part-1.md)합니다.  

CORS에 대 한 자세한 내용은 참조 [hello Azure 저장소 서비스에 대 한 크로스-원본 자원 공유 (CORS) 지원을](http://msdn.microsoft.com/library/azure/dn535601.aspx)합니다.  

### <a name="caching"></a>구성
#### <a name="subheading7"></a>데이터 가져오기
일반적으로는 서비스에서 데이터를 가져오는 횟수가 적을수록 좋습니다. 50MB blob 콘텐츠 tooa 사용자로 hello 저장소 서비스 tooserve에서 이미 검색에 웹 역할에서 실행 되는 MVC 웹 응용 프로그램의 hello 예제를 참조 하세요. hello 응용 프로그램 검색할 수 같은 해당 blob 될 때마다 사용자가 요청을 캐시할 수 것 또는 로컬로 후속 사용자 요청에 대 한 toodisk 및 재사용 hello 캐시 된 버전입니다. 또한 사용자 hello 데이터를 요청 될 때마다 hello 응용 프로그램 문제를 가져올 수는 조건부 헤더를 사용는 표시 되지 않도록 hello 전체 blob 수정 되지 않은 경우 수정 시간에 대 한 합니다. 이 동일한 패턴 tooworking 테이블 엔터티를 적용할 수 있습니다.  

경우에 따라 응용 프로그램이 해당 hello blob는, 및을이 기간 hello 하는 동안 응용 프로그램 필요는 없습니다 toocheck hello blob이 수정 된 경우를 검색 한 후 짧은 기간 동안 유효한 상태로 남아 가정할 수를 결정할 수 있습니다.

구성, 조회 및 항상 hello 응용 프로그램에서 사용 되는 기타 데이터 캐싱에 대 한 적합 한 항목 됩니다.  

.NET을 사용 하 여 어떻게 tooget 속성 toodiscover hello blob의 마지막으로 수정한 날짜에 대 한 예제 참조 [집합을 검색 속성 및 메타 데이터](../blobs/storage-properties-metadata.md)합니다. 조건부 다운로드에 대한 자세한 내용은 [Blob의 로컬 복사본을 조건부로 새로 고침](http://msdn.microsoft.com/library/azure/dd179371.aspx)을 참조하세요.  

#### <a name="subheading8"></a>데이터 일괄 업로드
데이터를 로컬로 집계한 다음 각 데이터 부분을 즉시 업로드하는 대신 주기적으로 일괄 업로드할 수 있는 응용 프로그램 시나리오가 있습니다. 예를 들어 웹 응용 프로그램 작업의 로그 파일을 가질 수 있습니다: hello 응용 프로그램 하나을 업로드할 수 모든 활동의 세부 정보 (엔드가, 저장소 작업 수) 테이블 항목으로 발생 하지 않거나 활동 세부 정보 tooa 로컬 로그 파일을 저장할 수 대로 했다가 구분 기호로 분리 된 파일 tooa blob으로 모든 작업 세부 정보를 주기적으로 업로드 합니다. 각 로그 항목은 크기가 1KB, 수천 (단일 트랜잭션 내에서 크기가 too64MB의 blob를 업로드할 수) 단일 "Put Blob" 트랜잭션에서 업로드할 수 있습니다. 물론, hello 로컬 컴퓨터에 이전 toohello 업로드 충돌할 경우 잠재적으로 손실 됩니다 일부 로그 데이터: hello 응용 프로그램 개발자 hello 가능성이 클라이언트 장치에 대 한 디자인 하거나 오류를 업로드 해야 합니다.  Hello 활동 데이터 toobe (하나가 아니라 활동) 시간에 대 한 다운로드 한 경우, blob는 테이블에 대해 권장 됩니다.

### <a name="net-configuration"></a>.NET 구성
.NET Framework hello를 사용 하 여, 하는 경우이 섹션 toomake 성능이 크게 향상 된 기능을 사용할 수 있는 몇 가지 빠른 구성 설정을 나열 합니다.  다른 언어를 사용 하 여 비슷한 개념 선택한 언어에 적용 하는 경우 toosee를 확인 합니다.  

#### <a name="subheading9"></a>기본 연결 제한 늘리기
.NET 코드 다음 hello 증가 (이 일반적으로 클라이언트 환경에 2 또는 서버 환경에서 10) hello 기본 연결 제한 too100 합니다. 일반적으로 응용 프로그램에서 사용 되는 스레드 hello 값 tooapproximately hello 번호를 설정 해야 합니다.  

```csharp
ServicePointManager.DefaultConnectionLimit = 100; //(Or More)  
```

모든 연결을 열기 전에 hello 연결도 설정 해야 합니다.  

다른 프로그래밍 언어에 대 한 해당 언어 설명서 toodetermine tooset hello 연결 제한 하는 방법을 참조 하세요.  

자세한 내용은 hello 블로그 게시물을 참조 하십시오. [웹 서비스: 동시 연결](http://blogs.msdn.com/b/darrenj/archive/2005/03/07/386655.aspx)합니다.  

#### <a name="subheading10"></a>비동기 작업에서 동기 코드를 사용하는 경우 스레드 풀의 최소 스레드 수 늘리기
이 코드는 hello 스레드 풀의 min 스레드 증가 합니다.  

```csharp
ThreadPool.SetMinThreads(100,100); //(Determine hello right number for your application)  
```

자세한 내용은 [ThreadPool.SetMinThreads 메서드](http://msdn.microsoft.com/library/system.threading.threadpool.setminthreads%28v=vs.110%29.aspx)를 참조하세요.  

#### <a name="subheading11"></a>.NET 4.5 가비지 수집 기능 활용
서버 가비지 수집의 성능 향상의 클라이언트 응용 프로그램 tootake 이점은 hello에 대 한.NET 4.5 이상을 사용 합니다.

자세한 내용은 hello 문서 참조 [는 개요의 성능 향상.NET 4.5에서](http://msdn.microsoft.com/magazine/hh882452.aspx)합니다.  

### <a name="subheading12"></a>제한 없는 병렬 처리
여러 작업자 tooaccess를 사용 하 여 바인딩되지 않은 병렬 처리 (hello 스레드 및/또는 병렬 요청 수에 제한 없음) tooupload 또는 다운로드 데이터 여러 파티션을 사용 하는 방법에 대 한 병렬 처리 하는 성능에 좋지 동안 조심 (컨테이너, 큐, 또는 파티션 테이블)에 hello 동일한 저장소 계정 또는 tooaccess hello에 여러 항목이 동일한 파티션에 합니다. Hello 병렬 처리 수준 제한이 없으면, 응용 프로그램 hello 클라이언트 장치 용량을 초과 하거나 더 긴 대기 시간이 않으며 제한 저장소 계정의 확장성 목표 hello 수 있습니다.  

### <a name="subheading13"></a>저장소 클라이언트 라이브러리 및 도구
항상 hello 최신 Microsoft에서 제공 클라이언트 라이브러리 및 도구를 사용 합니다. 쓰기를 hello 시점에는 다른 언어에 대 한 미리 보기 라이브러리 뿐만 아니라.NET, Windows Phone, Windows 런타임, Java 및 c + +에서 사용할 수 있는 클라이언트 라이브러리입니다. 또한 Microsoft에서는 Azure 저장소 작업을 위해 PowerShell cmdlet 및 Azure CLI 명령도 출시했습니다. Microsoft은 적극적으로 개발 하 고, 성능 염두에서 함께 이러한 도구, toodate 서로 hello 최신 서비스 버전을 구성 하 게 보관할을 처리 하는 다양 한 성능 사례를 내부적으로 입증 된 hello.  

### <a name="retries"></a>다시 시도
#### <a name="subheading14"></a>제한/서버 작업 중
경우에 따라 hello 저장소 서비스 수 있습니다 제한 응용 프로그램 또는 될 수 있습니다 단순히 일시적인 상태의 경우 toosome 인해 없습니다 tooserve hello 요청일 수 하 고 "503 서버 사용 중" 메시지 또는 "500 Timeout"를 반환 합니다.  이 응용 프로그램에 도달 하 고 hello 확장성 목표 중 하나 또는 hello 시스템 처리량이 늘어나며 여 분할 된 데이터 tooallow 리 밸런스는 경우에 발생할 수 있습니다.  hello 클라이언트 응용 프로그램 해야 하면 이러한 오류가 발생 하는 hello 작업을 다시 시도 일반적으로: hello 동일 나중에 요청을 시도 성공할 수 있습니다. 그러나 hello 저장소 서비스 응용 프로그램 확장성 목표를 초과 하기 때문에 제한 하거나 hello 서비스는 어떤 다른 이유로 없습니다 tooserve hello 요청에서 하는 경우에 적극적으로 다시 시도 hello 문제가 심각 일반적으로 확인 합니다. 이러한 이유로 지 수 (hello 클라이언트 라이브러리 기본 toothis 동작) 백오프을 사용 해야 합니다. 예를 들어 응용 프로그램은 작업을 2초, 4초, 10초, 30초 후에 다시 시도한 다음 계속 실패하면 작업을 완전히 포기할 수 있습니다. 이 동작은 크게 hello 서비스에서의 로드 줄이는 것이 아니라 모든 문제를 악화 시키는 것에 응용 프로그램에서 발생 합니다.  

연결 오류가 다시 시도할 수 즉시 때문에 제한의 결과로 hello 없는 일시적인 예상된 toobe note 합니다.  

#### <a name="subheading15"></a>다시 시도할 수 없는 오류
hello 클라이언트 라이브러리는 오류는 다시 시도 가능한와 하지 않을 인식있지 않습니다. 그러나 hello 저장소 REST API에 대해 사용자 고유의 코드를 작성 하는 경우 기억 하지 다시 시도해 야 하는 몇 가지 오류가: 400 (잘못 된 요청)이 응답 나타냅니다 hello 클라이언트 응용 프로그램 때문에 처리 하지 못한 요청을 전송 하는 예를 들어 것 예상 된 형태로 없습니다. 이 요청을 다시 전송 될 것을 다시 시도 중에 포인터가 없는 하므로 매번 같은 응답 hello 합니다. Hello 저장소 REST API에 대해 사용자 고유의 코드를 작성 하는 경우 (또는 비공유) hello 오류 코드 평균과 hello 적절 한 방법은 tooretry 고려해 야 채 각 항목에 대 한 합니다.  

#### <a name="useful-resources"></a>유용한 리소스
저장소 오류 코드에 대 한 자세한 내용은 참조 [상태 및 오류 코드](http://msdn.microsoft.com/library/azure/dd179382.aspx) hello Microsoft Azure 웹 사이트에 있습니다.  

## <a name="blobs"></a>Blob
에 대 한 사례를 입증 된 더하기 toohello에서 [모든 서비스](#allservices) 앞에서 설명한 검증 된 사용법 hello 다음 특히 toohello blob 서비스를 적용 합니다.  

### <a name="blob-specific-scalability-targets"></a>Blob 관련 확장성 목표
#### <a name="subheading46"></a>동시에 단일 개체를 액세스하는 여러 클라이언트
단일 개체를 동시에 액세스 하는 클라이언트 수가 많은 경우에 개체 및 저장소 계정 확장성 목표 당 tooconsider를 해야 합니다. 단일 개체에 액세스할 수 있는 클라이언트의 수를 정확 하 게 hello 메시지가 hello 개체의 크기를 hello hello 개체를 동시에 요청 된 클라이언트 hello 수 등의 요인에 따라 달라 집니다 (네트워크 상태 등).

Hello 개체를 통해 배포할 수 있습니다는 CDN 이미지 또는 비디오와 같은 웹 사이트에서 처리 한 다음 CDN을 사용 해야 합니다. [여기](#subheading5)를 참조하세요.

공학용 시뮬레이션 hello 데이터는 기밀로 유지와 같은 다른 시나리오에서는 두 가지 옵션이 있습니다. hello toostagger 워크 로드의 같은 액세스 개체 hello 하는 동시에 액세스 하는 시간 및 기간을 통해 액세스 되는 있습니다. 또는 개체당 및 저장소 계정에서 총 IOP hello 하므로 증가 하는 hello 개체 toomultiple 저장소 계정을 일시적으로 복사할 수 있습니다. 제한 된 테스트에 약 25 Vm (각 VM의 hello 다운로드 스레드 32 개를 사용 하 여 병렬화 되었습니다) 병렬로 100GB blob를 동시에 다운로드할 수 있습니다. Tooaccess hello 개체가 필요 합니다. 클라이언트 수가 100 개을 설치한 경우 먼저 tooa 두 번째 저장소 계정 및 다음 첫 번째 blob 처음 50 개 Vm 액세스 hello hello가 복사한 50 두 번째 Vm 액세스 hello 두 번째 blob hello 합니다. 결과는 응용 프로그램 동작에 따라 다르므로 설계 중에 이 동작을 테스트해야 합니다. 

#### <a name="subheading16"></a>Blob당 대역폭 및 작업
읽거나 tooa 최대 60MB/초를에서 한 tooa 단일 blob을 쓸 수 있습니다 (이 많은 네트워크 클라이언트 측의 hello 기능을 초과 하는 약 480 Mbps (hello 클라이언트 장치에 물리적 NIC hello 포함). 또한 단일 blob 초당 too500 요청을 지원합니다. Tooread 해야 하는 여러 클라이언트가 있는 경우 hello 동일한 blob 및 될 수 있습니다 이러한 한도 초과 CDN을 사용 하 여 hello blob를 배포 하는 것이 좋습니다.  

Blob의 목표 처리량에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.  

### <a name="copying-and-moving-blobs"></a>Blob 복사 및 이동
#### <a name="subheading17"></a>Blob 복사
REST API 버전 2012-02-12 hello 저장소 계정 간에 hello 유용한 기능 toocopy blob 도입: hello 저장소 서비스 toocopy (다른 저장소 계정)에 있는 다른 원본에서 blob를 지시 하 고 hello 하 게 하는 클라이언트 응용 프로그램 수 서비스는 hello 복사본을 비동기적으로 수행 합니다. Toodownload 필요 하지 않으며 hello 데이터를 업로드 하기 때문에 다른 저장소 계정에서 데이터를 마이그레이션하는 경우 hello 응용 프로그램에 필요 하는 hello 대역폭이 대폭 감소할 수 있습니다이 있습니다.  

하지만 그 중 하나, 저장소 계정 사이 복사할 때 있다는 점입니다 hello 복사본을 완료 하는 경우 시간 보장할 수 없습니다. 응용 프로그램에 필요한 toocomplete blob 제어 신속 하 게 복사 하는 경우 더 나은 toocopy hello blob tooa VM을 다운로드 하 고 다음 toohello 대상 업로드 수 있습니다.  이러한 상황에서는 전체 예측에 대 한 hello 복사본 수행 되도록 hello에서 실행 중인 VM에서 같은 Azure 지역. 그렇지 않으면 네트워크 상태 수 (및이 더) 성능에 영향을 복사 합니다.  또한 비동기 복사본의 hello 진행률을 프로그래밍 방식으로 모니터링할 수 있습니다.  

일반적으로 동일한 저장소 계정 자체 신속 하 게 완료 hello 내에서 복사 하는 참고 합니다.  

자세한 내용은 [Blob 복사](http://msdn.microsoft.com/library/azure/dd894037.aspx)를 참조하세요.  

#### <a name="subheading18"></a>AzCopy 사용
hello Azure 저장소 팀 "AzCopy" 명령줄 도구를 릴리스 했습니다 업그레이드용은 toohelp 즉, 및 저장소 계정에서 여러 blob를 전송 하는 대량 사용 합니다.  이 도구는 이러한 시나리오용으로 최적화되어 있으며 높은 전송 속도를 제공할 수 있습니다.  대량 업로드, 다운로드 및 복사 시나리오에는 이 도구를 사용하는 것이 좋습니다. 항목에 대 한 자세한 toolearn 다운로드를 참조 하세요 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md)합니다.  

#### <a name="subheading19"></a>Azure 가져오기/내보내기 서비스
데이터 (1TB 이상)의 매우 큰 볼륨 hello Azure 저장소는 hello을 업로드 하 고 하드 드라이브를 배송 하 여 blob 저장소에서 다운로드할 수 있는 가져오기/내보내기 서비스를 제공 합니다.  하드 드라이브에 데이터를 설정 하 고 업로드를 tooMicrosoft 보낼 하거나 빈 하드 드라이브 tooMicrosoft toodownload 데이터를 보낼 수 있습니다.  자세한 내용은 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](../storage-import-export-service.md)합니다.  이 업로드/다운로드 로그 데이터의이 양이 hello 네트워크를 통해 보다 훨씬 더 효율적일 수 있습니다.  

### <a name="subheading20"></a>메타데이터 사용
hello blob 서비스는 hello blob에 대 한 메타 데이터를 포함할 수 있는 헤드 요청을 지원 합니다. 예를 들어 응용 프로그램이 필요한 사진 부족 hello EXIF 데이터, 경우 hello 사진을 검색 하 고 압축을 풀고 수 것입니다. toosave 대역폭 및 성능 향상, 응용 프로그램 데이터를 저장할 수 hello EXIF hello blob의 메타 데이터에 hello 응용 프로그램 hello 사진 업로드 하는 경우: 다음 데이터를 검색할 수 hello EXIF HEAD 요청만 사용 하 여 메타 데이터에 중요 한 대역폭 절약 고 hello 처리 시간 tooextract hello EXIF 데이터 각 시간 hello blob을 읽이 필요 합니다. 이 방법이 필요한 hello 메타 데이터 및 전체 내용을 blob의 hello 시나리오에서 유용 합니다.  참고 blob 당 8KB만 메타 데이터를 저장할 수 있습니다 (hello 서비스를 허용 하지 것입니다 요청 toostore 그 보다 큰), 가능 하지 않습니다 hello 데이터 크기에 맞지 않을 경우 하므로 수 수 toouse이 방법을이 사용 합니다.  

방법의 예에 대 한 tooget.NET을 사용 하 여 blob의 메타 데이터 참조 [집합을 검색 속성 및 메타 데이터](../blobs/storage-properties-metadata.md)합니다.  

### <a name="uploading-fast"></a>고속 업로드
빠른 tooupload blob, 첫 번째 질문 tooanswer hello는: 업로드 한 blob 또는 많은 입니까?  아래 시나리오에 따라 지침 toodetermine hello 적절 한 방법 toouse hello를 사용 합니다.  

#### <a name="subheading21"></a>큰 Blob 하나를 빠르게 업로드
큰 단일 신속 하 게 blob tooupload, 클라이언트 응용 프로그램의 블록 또는 페이지 (되 고 각 blob 및 전체적으로 hello 저장소 계정에 대 한 hello 확장성 목표에 주의) 동시에 업로드 합니다.  Hello 공식 Microsoft 제공 RTM 저장소 클라이언트 라이브러리 (.NET, Java)가 hello 기능 toodo이 참고 합니다.  각 hello 라이브러리에 대 한 동시성의 지정 된 개체/속성 tooset hello 수준 보다 hello를 사용 합니다.  

* 사용 되는 BlobRequestOptions 개체 toobe.NET: 집합 ParallelOperationThreadCount 합니다.
* Java/Android: BlobRequestOptions.setConcurrentRequestCount()를 사용합니다.
* Node.js: hello blob 서비스 또는 hello 요청 옵션 중 하나에서 parallelOperationThreadCount를 사용 합니다.
* C + +: hello blob_request_options:: set_parallelism_factor 메서드를 사용 합니다.

#### <a name="subheading22"></a>여러 Blob을 빠르게 업로드
신속 하 게 blob 많은 tooupload 병렬에서 blob 업로드 합니다. 이 hello 저장소 서비스의 여러 파티션에서 hello 업로드 분산 되므로 한 번에 단일 blob을 블록 병렬 업로드와 함께 업로드 하는 보다 빠릅니다. 단일 Blob은 초당 60MB(약 480Mbps)의 처리량만을 지원합니다. 작성 hello 시 미국 LRS 계정에서는 최대 지원 too20 개별 blob에서 지 원하는 hello 처리량 보다 훨씬 많은 g b p s 수신 합니다.  이 시나리오에서는 기본적으로 업로드를 병렬로 수행하는 [AzCopy](#subheading18)를 사용하는 것이 좋습니다.  

### <a name="subheading23"></a>Blob의 hello 올바른 유형을 선택 하면
Azure Storage는 두 가지 형식의 Blob 즉, *페이지* Blob과 *블록* Blob을 지원합니다. 특정된 사용 시나리오의 경우에 대 한 blob 유형 선택한 솔루션의 hello 성능 및 확장성에 영향을 합니다. 블록 blob는 tooupload 많은 양의 데이터를 효율적으로 하려는 경우 적절 한: tooupload 사진이 나 비디오 tooblob 저장소 클라이언트 응용 프로그램 예를 들어 할 수 있습니다. 페이지 blob는 tooperform hello 데이터에 대해 임의 쓰기를 hello 응용 프로그램에서 필요로 하는 경우에 적합 합니다: 예를 들어 Azure Vhd는 페이지 blob으로 저장 됩니다.  

자세한 내용은 [블록 Blob, 추가 Blob 및 페이지 Blob 이해](http://msdn.microsoft.com/library/azure/ee691964.aspx)를 참조하세요.  

## <a name="tables"></a>테이블
에 대 한 사례를 입증 된 더하기 toohello에서 [모든 서비스](#allservices) 앞에서 설명한 검증 된 사용법 hello 다음 특히 toohello 테이블 서비스를 적용 합니다.  

### <a name="subheading24"></a>테이블 관련 확장성 목표
또한 toohello 대역폭의 제한 사항 전체 저장소 계정, 테이블 특정 확장성 한계에 따라 hello를 갖고 있습니다.  Hello 시스템 로드를 균형 조정 하면 트래픽이 증가 함에 따라 되지만 가능 하지 않습니다 트래픽이 급격 한 증가 있으면 즉시 수 tooget 처리량이이 많은 수 있습니다.  하는 동안 시간 제한을 hello 저장소 서비스로 자동으로 버스트를 hello 및/또는 toosee 조정 될 때, 패턴에 급증 하는 경우 테이블 아웃 부하를 분산 합니다.  Hello 시스템 시간 tooload 균형을 적절 하 게 제공 하는 대로 더 나은 결과 있을 것으로 예상 일반적으로 느린 있습니다.  

#### <a name="entities-per-second-account"></a>초당 엔터티 수(계정)
테이블에 액세스 하는 hello 확장성 제한 된 too20, 000 엔터티 (1KB 각) 계정에 대 한 초당 최대입니다.  일반적으로는 삽입, 업데이트, 삭제 또는 스캔하는 각 엔터티가 이 목표 수 계산에 포함됩니다.  따라서 엔터티 100개가 포함된 일괄 삽입을 수행하면 엔터티가 100개로 계산됩니다.  마찬가지로 1,000개 엔터티를 스캔하여 5를 반환하는 쿼리의 경우 엔터티가 1,000개로 계산됩니다.  

#### <a name="entities-per-second-partition"></a>초당 엔터티 수(파티션)
단일 파티션 내에서 확장성 목표 hello 초당 2, 000 엔터티 (1KB 각)은 테이블에 액세스를 사용 하 여 hello 동일한 계산 hello 이전 섹션에 설명 된 대로 합니다.  

### <a name="configuration"></a>구성
이 섹션에는 hello 테이블 서비스에 toomake 성능이 크게 향상 된 기능을 사용할 수 있는 몇 가지 빠른 구성 설정을 나열 합니다.  

#### <a name="subheading25"></a>JSON 사용
저장소 서비스 버전 2013-08-15부터 hello 테이블 서비스 hello AtomPub XML 기반 형식 대신 JSON을 사용 하 여 테이블 데이터를 전송 하기 위한 지원 합니다. 75%에서 페이로드 크기를 줄일 수 하 고 응용 프로그램의 hello 성능을 크게 향상 시킬 수 있습니다.

자세한 내용은 hello 게시물을 참조 하세요. [Microsoft Azure 테이블: JSON 소개](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/05/windows-azure-tables-introducing-json.aspx) 및 [테이블 서비스 작업에 대 한 페이로드 형식](http://msdn.microsoft.com/library/azure/dn535600.aspx)합니다.

#### <a name="subheading26"></a>Nagle 해제
Nagle 알고리즘은 널리 수단 tooimprove 네트워크 성능으로 TCP/IP 네트워크를 통해 구현 됩니다. 그러나 대화형 작업을 많이 수행하는 환경 등 일부 상황에서는 이 알고리즘이 적합하지 않습니다. Azure 저장소에 대 한 Nagle 알고리즘에는 요청 toohello 테이블 및 큐 서비스의 hello 성능에 부정적인 영향 및 가능한 경우 비활성화 해야 합니다.  

자세한 내용은 블로그 게시물을 참조 하십시오. [Nagle 알고리즘은 작은 요청으로 친숙 하지](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx), Nagle 알고리즘 요청, 테이블 및 큐와 제대로 상호 작용 하 고 표시 이유를 설명 하 방법을 toodisable 클라이언트에서 응용 프로그램입니다.  

### <a name="schema"></a>스키마
나타내고 데이터를 쿼리는 hello 가장 큰 단일 요소 hello 테이블 서비스의 hello 성능에 영향을 주는입니다. 각 응용 프로그램별로 다르기는 하지만 이 섹션에서는 다음 항목과 관련된 일반적인 검증된 작업 방식 중 몇 가지에 대해 간략하게 설명합니다.  

* 테이블 디자인
* 효율적인 쿼리
* 효율적인 데이터 업데이트  

#### <a name="subheading27"></a>테이블 및 파티션
테이블은 파티션으로 구분됩니다. 저장 된 모든 엔터티를 파티션으로 공유 hello 동일한 파티션 키 및 고유한 행 키 tooidentify에 해당 파티션 내에서. 파티션을 사용하는 경우에는 이점도 있지만 확장성 제한도 적용됩니다.  

* 이점: hello too100 별도 저장소 작업 (총 크기가 4MB 제한)을 포함 하는 단일 원자성 일괄 처리 트랜잭션은 동일한 파티션에의 엔터티를 업데이트할 수 있습니다. 동일한 수 hello 가정 엔터티 toobe 검색의 쿼리할 수도 있습니다는 단일 파티션 내에서 데이터 파티션을 (하지만 읽기에서 추가 테이블 데이터 쿼리에 대 한 권장 사항은)에 걸쳐 있는 데이터 보다 더 효율적으로 합니다.
* 확장성 한계: 단일 파티션에 저장 된 액세스 tooentities 없습니다 수 부하 분산 된 파티션을 원자성 일괄 처리 트랜잭션을 지원 합니다. 이러한 이유로 개별 테이블 파티션에 대 한 hello 확장성 목표 보다 낮습니다 hello 테이블 서비스에 대 한 전체.  

테이블 및 파티션에의 이러한 특성으로 인해 디자인 원칙을 따르는 hello를 채택 해야 합니다.  

* 자주 업데이트 / 쿼리 작업의 동일한 논리 단위에 배치 해야 하는 hello 클라이언트 응용 프로그램 데이터를 동일한 파티션에 hello 합니다.  응용 프로그램 쓰기를 집계 하기 때문에 또는 원자성 일괄 처리 작업이 tootake 활용 하려고 하기 때문에 수 있습니다.  또한 단일 쿼리에서는 여러 파티션에 분산된 데이터보다 단일 파티션의 데이터를 더 효율적으로 쿼리할 수 있습니다.
* 클라이언트 응용 프로그램 또는 하지 않는 삽입/업데이트 작업 (예: 단일 쿼리 또는 일괄 처리 업데이트)의 동일한 논리 단위에 배치 해야 하는 hello에 쿼리 데이터를 별도 디스크입니다.  중요 한 정보 하므로 문제가 되지 않습니다 하 고 성능 영향을 주지 않을 파티션 키의 있는 단일 테이블의 파티션 키 수 없는 제한 toohello 된다는 점입니다.  예를 들어 사용자 로그인을 사용 하는 인기 있는 웹 사이트 응용 프로그램을 사용 하는 경우 hello 사용자 Id를 사용 하 여 hello 파티션 키로 적합 한 선택 수 있습니다.  

#### <a name="hot-partitions"></a>핫 파티션
핫 파티션 하나 hello 트래픽 tooan 계정의 불균형 비율을 수신 하는 이며 없습니다 부하 분산 될 단일 파티션이 있기 때문에 있습니다.  일반적으로는 다음의 두 가지 방식 중 하나로 핫 파티션을 만듭니다.  

##### <a name="subheading28"></a>추가 전용 및 앞에 추가 전용 패턴
hello "추가" 패턴은 모든 (또는 거의 모든) hello 트래픽 tooa의 PK 제공 증가 하 고 현재 시간에 따라 toohello 감소 위치입니다.  예로 경우 응용 프로그램으로 사용 하는 hello 현재 날짜 로그 데이터에 대 한 파티션 키입니다.  이 인해 모든 테이블의 마지막 파티션의 toohello 라인으로 전환 하는 hello 삽입 및 hello 쓰기 모두에 테이블의 지속적인 toohello 끝 hello 시스템 균형을 로드할 수 없습니다.  트래픽 toothat 파티션의 hello 볼륨 hello 파티션 수준 확장성 목표를 초과 하면 제한에서 발생 합니다.  것이 더 나은 tooensure 보내지는 트래픽을 toomultiple 파티션을 tooenable 부하 균형 hello 테이블을 통해 요청 합니다.  

##### <a name="subheading29"></a>트래픽이 많은 데이터
에서는 단일 파티션의 파티션 구성표 결과 방금가 있으면 다른 파티션에 보다 훨씬 더 많은 사용 되는 데이터도 표시 제한 해당 파티션의 단일 파티션에 대 한 확장성 목표 hello 가까워질수록 합니다.  것이 더 나은 toomake 있는지 없는 단일 파티션 구성표 결과 근접 hello 확장성 목표를 분할 합니다.  

#### <a name="querying"></a>쿼리
이 섹션에서는 hello 테이블 서비스를 쿼리 하기 위한 검증 된 사례를 설명 합니다.  

##### <a name="subheading30"></a>쿼리 범위
여러 가지 방법으로 toospecify hello 다양 한 엔터티 tooquery 가지가 있습니다.  hello 다음은 각각의 hello 사용에 대 한 내용은입니다.  

일반적으로 (단일 엔터티 보다 큰 쿼리) 검사를 방지할 하지만 검색 해야 하는 경우 시도 tooorganize 데이터는 사용자 검색 hello 필요한 데이터를 검색 하거나 상당한 양의 않아도 엔터티를 반환 하지 않고 검색 하도록 합니다.  

###### <a name="point-queries"></a>지점 쿼리
지점 쿼리에서는 엔터티를 하나만 검색합니다. Hello 파티션 키와 행 키의 hello 엔터티 tooretrieve 지정 하 여 수행 합니다. 이러한 쿼리는 매우 효율적이므로 가능한 경우 항상 사용해야 합니다.  

###### <a name="partition-queries"></a>파티션 쿼리
파티션 쿼리는 공통 파티션 키를 공유하는 데이터 집합을 검색하는 쿼리입니다. 일반적으로 hello 쿼리는 또한 tooa 파티션 키에 행 키 값의 범위 또는 일부 엔터티 속성의 값 범위를 지정합니다. 파티션 쿼리는 지점 쿼리보다 효율성이 낮으므로 꼭 필요할 때만 사용해야 합니다.  

###### <a name="table-queries"></a>테이블 쿼리
테이블 쿼리는 공통 파티션 키를 공유하지 않는 엔터티 집합을 검색하는 쿼리입니다. 이러한 쿼리는 효율적이지 않으므로 가능하면 사용하지 않아야 합니다.  

##### <a name="subheading31"></a>쿼리 밀도
쿼리 효율에 또 다른 핵심 요소는 hello 비교 toohello 스캔 한 toofind hello 설정 반환 되는 엔터티 수로 반환 되는 엔터티 수입니다. 응용 프로그램 1의 %만 hello 데이터 공유를 hello 쿼리는 검색는 100 개의 엔터티가 반환 마다 하나의 엔터티에 대 한 속성 값에 대 한 필터와 함께 테이블에 대 한 쿼리를 수행 합니다. hello 설명 하는 테이블 확장성 목표 이전에 모두 검색 하는 엔터티의 toohello 수 및 관련 반환 된 엔터티 수를 hello 하지: 낮은 쿼리 밀도 쉽게 될 수 있습니다 hello 테이블 서비스 toothrottle 응용 프로그램 너무 많은 스캔 해야 하기 때문에 원하는 엔터티 tooretrieve hello 엔터티.  아래의 hello 섹션을 참조에 [비 정규화](#subheading34) 방법에 대 한 자세한 내용은 tooavoid이 있습니다.  

##### <a name="limiting-hello-amount-of-data-returned"></a>크기의 데이터를 반환 하는 hello 제한
###### <a name="subheading32"></a>필터링
쿼리 hello 클라이언트 응용 프로그램에서 필요 없는 엔터티를 반환 합니다 있는지 알고 hello 반환 되는 집합의 필터 tooreduce hello 크기를 사용 하는 것이 좋습니다. Hello 엔터티 반환 되지 않습니다. toohello 클라이언트 hello 확장성 제한에 여전히 포함, 응용 프로그램 성능을 감소 hello 네트워크 페이로드 크기 때문에 향상 되며 클라이언트 응용 프로그램에서 처리 해야 하는 엔터티 수를 줄여 hello .  그러나에 참고 위의 참조 [쿼리 밀도](#subheading31), 많은 엔터티를 필터링 하는 쿼리 수 제한 발생할 수, 몇 개의 엔터티가 반환 된 경우에 있으므로 hello 확장성 목표 검색, 엔터티의 toohello 수 관련 – 합니다.  

###### <a name="subheading33"></a>프로젝션
클라이언트 응용 프로그램이 제한 된 집합의 테이블에 대 한 hello 엔터티에서 속성을 필요한 경우 데이터 집합을 반환 하는 hello의 프로젝션 toolimit hello 크기를 사용할 수 있습니다. 필터링와 마찬가지로 이렇게 하면 tooreduce 네트워크 로드 하 고 클라이언트 처리 합니다.  

##### <a name="subheading34"></a>비정규화
관계형 데이터베이스를 사용 하는 달리 hello 검증 된 사례 테이블 데이터를 효율적으로 쿼리 하기 위한 될 toodenormalizing 데이터. 즉, 여러 엔터티에 동일한 데이터를 복제 hello (하나 각 키에 대 한 toofind hello 데이터를 사용할 수 있습니다) toominimize hello toofind hello 데이터 hello 클라이언트 요구 대신 tooscan 수가 많은 엔터티 toofind 쿼리 검사 해야 하는 엔터티 수 hello 데이터 응용 프로그램에 필요 합니다.  예를 들어 전자 상거래 웹 사이트에서 좋습니다 toofind 한 정렬을 모두 hello 고객 ID (이 고객의이 주문이 제공)으로 hello 날짜 (제공 주문 날짜에).  테이블 저장소는 편이 최상의 toostore hello 엔터티 (또는 참조 tooit) 두 번 – 테이블 이름, PK 및 RK toofacilitate 찾기 hello 날짜 여 찾기 toofacilitate 한 번 고객 ID 기준으로 합니다.  

#### <a name="insertupdatedelete"></a>삽입/업데이트/삭제
이 섹션에서는 hello 테이블 서비스에 저장 된 엔터티를 수정 하기 위한 검증 된 사례를 설명 합니다.  

##### <a name="subheading35"></a>일괄 처리
일괄 처리 트랜잭션은으로 엔터티 그룹 트랜잭션 (ETG) Azure 저장소;에 라고 합니다. 단일 테이블에서 단일 파티션에 ETG 내의 모든 hello 작업 이어야 합니다. 가능한 경우, 일괄 처리로 ETGs tooperform 삽입, 업데이트 및 삭제를 사용 합니다. 이 클라이언트 응용 프로그램 toohello 서버에서 hello 라운드트립 횟수를 감소, hello 청구 가능 트랜잭션 수 (ETG는 청구 용 단일 트랜잭션으로 계산 하며 too100 저장소 작업을 포함할 수 있습니다.), 줄어들고 원자성을 사용 하도록 설정 (모든 작업이 성공 또는 실패는 ETG 내에서 모든)를 업데이트 합니다. 모바일 장치와 같이 대기 시간이 긴 환경에서는 ETG를 사용하면 매우 효율적입니다.  

##### <a name="subheading36"></a>Upsert
가능한 경우에는 항상 테이블 **Upsert** 작업을 사용합니다. **Upsert**에는 두 가지 형식이 있으며, 두 형식 모두 기존의 **Insert** 및 **Update** 작업보다는 비효율적일 수 있습니다.  

* **InsertOrMerge**: tooupload hello 엔터티 속성의 하위 집합을 원하는 경우에 사용 되지만 확실 하지 않은 hello 엔터티 이미 존재 하는지 여부입니다. 이 호출은 hello에 포함 된 hello 속성 hello 엔터티가 존재 하는 경우 업데이트 **Upsert** 작업, 및는 대로 모든 기존 속성을 유지, 엔터티가 없는 경우 hello, hello 새 엔터티를 삽입 합니다. 쿼리에서 비슷한 toousing 프로젝션 tooupload hello 속성을 변경 하는 해야 한다는 점에서입니다.
* **InsertOrReplace**: tooupload 완전히 새로운 엔터티의 싶지만 확실 하지 않은 이미 존재 하는지 여부는 경우에 사용 합니다. 이 설정을 사용 해야 hello 이전 엔터티를 완전히 덮어쓰기 때문에 완전히 올바른지 알고 있을 때 해당 hello 엔터티를 새로 업로드 합니다. 예를 들어 tooupdate hello 엔터티 hello 응용 프로그램 hello 사용자;에 대 한 위치 데이터에 이전에 저장 하는 여부에 관계 없이 사용자의 현재 위치를 저장 하 시겠습니까 새 위치 엔터티 hello 완료 되며 이전 엔터티만의 모든 정보를 필요가 없습니다.

##### <a name="subheading37"></a>단일 엔터티에 데이터 계열 저장
응용 프로그램에서 일련의 필요 하다 고 판단 자주 tooretrieve 한 번에 데이터를 저장 하는 경우에 따라: 예를 들어 응용 프로그램 추적 CPU 사용량 순서 tooplot hello 데이터의 롤링 차트에에서는 시간이 지남에 따라 hello에서 지난 24 시간입니다. 한 가지 방법은 toohave 한 테이블 엔터티 시간당 각 엔터티는 특정 시간을 나타내고 해당 시간에 대 한 hello CPU 사용량을 저장 합니다. tooplot hello 응용 프로그램이 데이터를 tooretrieve hello 엔터티 가장 최근 24 시간 동안 hello에서 hello 데이터를 보유 해야 합니다.  

응용 프로그램의 단일 엔터티 별도 속성으로 각 시간에 대 한 hello CPU 사용량을 저장할 수 있습니다 또는: tooupdate 매시간 응용 프로그램 צ ְ ײ 단일 **InsertOrMerge Upsert** tooupdate hello 값 hello에 대 한 호출 가장 최근 시간입니다. tooplot hello 데이터 hello 응용 프로그램 하기만 tooretrieve 24, 매우 효율적인 쿼리를 만드는 대신 단일 엔터티 (에 토론 위의 참조 [쿼리 범위](#subheading30)).

##### <a name="subheading38"></a>Blob에 구조적 데이터 저장
구조적 데이터를 테이블에 저장해야 하는 경우도 있지만 엔터티 범위는 항상 함께 검색되며 일괄로 삽입할 수 있습니다.  이와 관련한 좋은 예가 로그 파일입니다.  몇 분 동안의 로그를 일괄로 생성하여 삽입할 수 있으며 항상 몇 분 동안의 로그를 한 번에 검색할 수도 있습니다.  이 경우 성능을 위해 것 이므로 더 나은 toouse blob, 테이블 대신 있습니다 수 hello 많은 개체 작성/반환을 크게 줄일 뿐만 아니라 일반적으로 수행 해야 하는 요청 수를 hello입니다.  

## <a name="queues"></a>큐
에 대 한 사례를 입증 된 더하기 toohello에서 [모든 서비스](#allservices) 앞에서 설명한 검증 된 사용법 hello 다음 특히 toohello 큐 서비스를 적용 합니다.  

### <a name="subheading39"></a>확장성 제한
단일 큐는 초당 약 2,000개의 메시지(각각 1KB)를 처리할 수 있습니다(여기서는 각 AddMessage, GetMessage 및 DeleteMessage를 메시지로 계산). 응용 프로그램에 대해 충분 하지 않으면에 여러 큐를 사용 하 고 hello 메시지에 이러한 분산 해야 합니다.  

[Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)에서 현재 확장성 목표를 봅니다.  

### <a name="subheading40"></a>Nagle 해제
테이블 구성 hello Nagle 알고리즘을 설명 하는 hello 섹션을 참조 하십시오.-hello Nagle 알고리즘은 일반적으로 큐 요청의 hello 성능에 부정적 하 고 사용 하지 않도록 설정 해야 합니다.  

### <a name="subheading41"></a>메시지 크기
메시지 크기가 증가함에 따라 큐 성능 및 확장성은 감소합니다. 메시지에만 hello hello 수신기 필요한 정보를 배치 해야 합니다.  

### <a name="subheading42"></a>일괄 검색
한 번에 큐에서 too32 메시지를 검색할 수 있습니다. 모바일 장치 등의 환경에 특히 유용한 hello 클라이언트 응용 프로그램에서 대기 시간이 긴 hello 왕복 횟수를 줄일 수 있습니다이.  

### <a name="subheading43"></a>큐 폴링 간격
대부분의 응용 프로그램은 해당 응용 프로그램에 대 한 트랜잭션 hello 가장 큰 원인 중 하나일 수 있는 큐에서 메시지를 폴링합니다. 폴링 간격을 현명 하 게 선택: 너무 자주 폴링으로 인해 응용 프로그램 tooapproach hello 큐에 대 한 hello 확장성 목표입니다. 그러나 (작성 hello 시점)에 $0.01에 대 한 200000 트랜잭션을에서 한 달에 대 한 초당 비용 보다 작거나 15 센트 않으므로 비용 면 폴링 단일 프로세서 아닌 경우 일반적으로 선택 하는 폴링 간격에 영향을 주는 요인  

최신 비용 정보는 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요.  

### <a name="subheading44"></a>UpdateMessage
사용할 수 있습니다 **UpdateMessage** tooincrease hello 표시 안 함 시간 제한 또는 tooupdate 상태 정보 메시지입니다. 강력한 이지만, 각 기억 **UpdateMessage** 작업 hello 확장성 목표에 합산 됩니다. 그러나에서 전달 되는 작업 하나의 큐 toohello 다음으로 hello 작업의 각 단계를 완료 하는 대로 워크플로 사용 하는 보다 훨씬 더 효율적인 방법이 될 수 있습니다. Hello를 사용 하 여 **UpdateMessage** 작업 응용 프로그램 toosave hello 작업 상태 toohello 메시지를 허용 하 고 서 hello hello 작업 단계를 완료 될 때마다의 다음 단계에 대 한 hello 메시지를 다시 큐 대신 작업을 계속 합니다.  

자세한 내용은 hello 문서 참조 [하는 방법: 대기 중인된 메시지의 hello 내용을 변경](../queues/storage-dotnet-how-to-use-queues.md#change-the-contents-of-a-queued-message)합니다.  

### <a name="subheading45"></a>응용 프로그램 아키텍처
큐 toomake 확장 가능한 응용 프로그램 아키텍처를 사용 해야 합니다. hello 다음에는 확장성이 뛰어난 응용 프로그램 큐 toomake를 사용할 수 있는 몇 가지 방법을 보여 줍니다.  

* 처리에 대 한 작업의 toocreate 백로그 큐를 사용할 수 있으며 응용 프로그램에서 작업 부하를 매끄럽게 있습니다. 예를 들어 사용자가 tooperform 프로세서 업로드 된 이미지 크기 조정 등 많은 작업에서 요청을 큐 대기 수 있습니다.
* 있습니다 수에 독립적으로 확장할 수 있도록 응용 프로그램의 큐 toodecouple 부분을 사용할 수 있습니다. 예를 들어 웹 프런트 엔드에서 나중에 분석 및 저장하기 위해 사용자의 설문 조사 결과를 큐에 저장할 수 있습니다. 더 많은 작업자 역할 인스턴스 tooprocess hello 필요에 따라 큐 데이터를 추가할 수 있습니다.  

## <a name="conclusion"></a>결론
이 문서 검증 된 Azure 저장소를 사용 하는 경우 성능을 최적화 하기 위한 사용법을 가장 일반적인 hello 중 일부에 대해 설명 합니다. 모든 응용 프로그램 개발자 tooassess 사례 위의 hello 각각에 대해 해당 응용 프로그램 들이 하 고 hello 권장 사항 tooget Azure 저장소를 사용 하는 응용 프로그램에 대 한 뛰어난 성능 작업을 수행 하십시오.
