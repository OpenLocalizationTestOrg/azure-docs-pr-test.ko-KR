---
title: "aaaIntroduction tooAzure 저장소 | Microsoft Docs"
description: "Azure 저장소, hello 클라우드에서 Microsoft의 온라인 데이터 저장소의 개요. Toouse 응용 프로그램에서 가장 사용 가능한 클라우드 저장소 솔루션을 hello 하는 방법에 대해 알아봅니다."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Azure 저장소 소개 tooMicrosoft

## <a name="overview"></a>개요
Azure 저장소는 내구성, 가용성 및 고객의 확장성 toomeet hello 요구를 사용 하는 최신 응용 프로그램에 대 한 hello 클라우드 저장소 솔루션입니다. 이 문서를 통해 개발자, IT 전문가 및 비즈니스 의사 결정자는 다음에 대한 내용을 배울 수 있습니다.

* Azure Storage의 정의 및 클라우드, 모바일, 서버 및 데스크톱 응용 프로그램에서 Azure Storage를 활용할 수 있는 방법
* 어떤 종류의 데이터를 저장할 수 있습니다 hello Azure 저장소 서비스와: (object) 데이터, NoSQL 테이블 데이터, 메시지 큐, blob 및 파일 공유 합니다.
* Azure 저장소에 tooyour 데이터 액세스 관리 하는 방법
* 중복 및 복제를 통해 Azure Storage 데이터의 영속성을 유지하는 방법
* 여기서 toogo 다음 toobuild 첫 번째 Azure 저장소 응용 프로그램

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Azure Storage 작업을 위한 도구, 라이브러리 및 기타 리소스는 아래 [다음 단계](#next-steps)를 참조하세요.

## <a name="what-is-azure-storage"></a>Azure Storage란?
클라우드 컴퓨팅은 확장 가능하고 내구성이 우수한 고가용성 데이터 저장소가 필요한 응용 프로그램이 요구되는 새로운 시나리오를 지원합니다. Microsoft는 이러한 맥락에서 Azure Storage를 개발했습니다. 또한 toomaking에 해당 개발자 toobuild 대규모 응용 프로그램 toosupport 새로운 시나리오에 대 한 가능한 경우 Azure 저장소도 hello 저장소 기반 제공에 대 한 Azure 가상 컴퓨터를 더 이상 척도가 tooits 견고성.

Azure 저장소 이므로 확장성이 뛰어난, 저장 하 고 수백 테라바이트 과학, 재무 분석 및 미디어 응용 프로그램에 필요한 데이터 toosupport hello 빅 데이터 시나리오를 처리할 수 있습니다. 또는 hello 적은 양의 소규모 기업 웹 사이트에 필요한 데이터를 저장할 수 있습니다. 가 나중에 맞게 때마다 저장 하는 hello 데이터에 대해서만 지불 합니다. Azure Storage는 현재 수십조에 달하는 고유한 고객 개체를 저장하고 초당 평균 수백만 건의 요청을 처리합니다.

Azure 저장소는는 대규모 글로벌 고객에 대 한 응용 프로그램을 디자인 하 고 필요-hello 저장 된 데이터 양을 기준으로 둘 다에 따라 해당 응용 프로그램을 확장 하 고 hello에 대 한 요청 수 있으므로 유연 합니다. 사용량에 대해서만, 그리고 사용하는 경우에만 지불합니다.

Azure Storage는 트래픽을 기반으로 자동으로 데이터 부하를 분산하는 자동 분할 시스템을 사용합니다. 즉,는 hello 요구 사항에 응용 프로그램 성장에으로 Azure 저장소 자동으로 할당 hello 적절 한 리소스가 toomeet 해당 합니다.

Azure 저장소는 hello world 응용 프로그램의 모든 형식에서의 모든 위치에서 액세스할 수 있는 hello 데스크톱, 온-프레미스 서버 또는 모바일 hello 클라우드에서 실행 여부 또는 태블릿 장치입니다. Hello 응용 프로그램 hello 장치에서 데이터의 하위 집합을 저장 하 고 hello 클라우드에 저장 된 데이터의 전체 집합과 동기화 모바일 시나리오에서 Azure 저장소를 사용할 수 있습니다.

Azure Storage는 편리한 개발을 위해 다양한 운영 체제 집합(Windows 및 Linux 포함) 및 다양한 프로그래밍 언어( .NET, Java, Node.js, Python, Ruby, PHP 및 C++과 모바일 프로그래밍 언어 포함)를 사용하는 클라이언트를 지원합니다. Azure 저장소는 또한 사용할 수 있는 tooany 클라이언트 보내고 HTTP/HTTPS를 통해 데이터를 받을 수 있는 간단한 REST Api를 통해 데이터 리소스를 노출 합니다.

Azure Premium Storage는 Azure Virtual Machines에서 실행되는 I/O 사용량이 많은 작업을 지원하는 짧은 대기 시간의 고성능 디스크를 제공합니다. Azure 프리미엄 저장소를 여러 영구 데이터 디스크 tooa 가상 컴퓨터를 연결 하 고 사용할 수 toomeet 구성 성능 요구 사항입니다. 각 데이터 디스크는 Azure Premium Storage에서 SSD 디스크의 지원을 받으며 최대 I/O 성능을 제공합니다. 자세한 내용은 [Premium Storage: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](storage-premium-storage.md)를 참조하세요.

## <a name="introducing-hello-azure-storage-services"></a>Hello Azure 저장소 서비스를 소개합니다.
Azure 저장소는 다음 4 개의 서비스는 hello 제공: Blob 저장소, 테이블 저장소, 큐 저장소 및 파일 저장소.

* Blob Storage는 구조화되지 않은 개체 데이터를 저장합니다. Blob은 문서, 미디어 파일 또는 응용 프로그램 설치 프로그램 등 모든 종류의 텍스트 또는 이진 데이터일 수 있습니다. Blob 저장소 참조 tooas 개체 저장소 이기도합니다.
* Table Storage는 구조화된 데이터 집합을 저장합니다. 테이블 저장소는 신속 하 게 개발 및 데이터의 빠른 액세스 toolarge 수량을 허용 하는 NoSQL 키-특성 데이터 저장소.
* Queue Storage는 워크플로 처리 및 클라우드 서비스 구성 요소 사이의 통신을 위한 안정적인 메시지를 제공합니다.
* 파일 저장소 hello 표준 SMB 프로토콜을 사용 하 여 레거시 응용 프로그램에 대 한 공유 저장소를 제공 합니다. Azure 가상 컴퓨터 및 클라우드 서비스를 통해 탑재 된 공유 응용 프로그램 구성 요소에서 파일 데이터를 공유할 수 및 온-프레미스 응용 프로그램에는 파일 데이터 hello 파일 서비스 REST API를 통해 공유에 액세스할 수 있습니다.

Azure 저장소 계정은 tooservices Azure 저장소에서에 액세스할 수 있게 해 주는 보안 계정입니다. 저장소 계정의 저장소 리소스에 대 한 hello 고유한 네임 스페이스를 제공합니다. 아래 hello 이미지 hello hello Azure 저장소는 저장소 계정의 리소스에에서 관계를 보여 줍니다.

![Azure Storage 리소스](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Blob 저장소
많은 양의 구조화 되지 않은 개체 데이터 toostore hello 클라우드에서 사용자의 경우 Blob 저장소 비용 효율적이 고 확장 가능한 솔루션을 제공합니다. 와 같은 Blob 저장소 toostore 콘텐츠를 사용할 수 있습니다.

* 문서
* 사진, 비디오, 음악, 블로그 등의 소셜 데이터
* 파일, 컴퓨터, 데이터베이스 및 장치의 백업
* 웹 응용 프로그램의 이미지 및 텍스트
* 클라우드 응용 프로그램의 구성 데이터
* 로그 및 기타 대규모 데이터 집합과 같은 빅 데이터

모든 Blob은 컨테이너로 구성됩니다. 또한 컨테이너의 개체는 유용한 방법은 tooassign 보안 정책 toogroups를 제공합니다. 저장소 계정은 개수에 관계 없이 컨테이너를 포함할 수 있습니다 및 컨테이너에 blob hello 저장소 계정의 toohello 500TB 용량 한계를 개수에 관계 없이 포함 될 수 있습니다.

Blob 저장소에는 블록 Blob, 추가 Blob 및 페이지 Blob(디스크)의 세 가지 Blob 유형이 있습니다.

* 블록 Blob은 클라우드 개체 스트리밍 및 저장을 위해 최적화되며 문서, 미디어 파일, 백업 등을 저장하는 데 적합합니다.
* 추가 blob 비슷한 tooblock blob 하지만에 맞게 최적화 된 작업을 추가 합니다. 새 블록 toohello 끝을 추가 해야만 추가 blob은 업데이트할 수 있습니다. 추가 blob는 로깅에서 새 데이터 필요한 toobe hello blob의 toohello 끝만 작성 등의 시나리오에 적합 합니다.
* 페이지 blob는 IaaS 디스크를 나타내기 위해 최적화 되었으며 임의 지 원하는 쓰고 크기가 too1 TB up 될 수 있습니다. Azure 가상 컴퓨터 네트워크에 추가된 IaaS 디스크는 페이지 Blob으로 저장된 VHD입니다.

매우 큰 데이터 집합을 업로드 하거나 비현실적 hello 유선을 통해 데이터 tooBlob 저장소 다운로드 네트워크 제약 조건을 확인 하는 위치, 하드 드라이브 tooMicrosoft tooimport 제공 하거나 hello 데이터 센터에서 직접 데이터를 내보낼 수 있습니다. 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](storage-import-export-service.md)합니다.

## <a name="table-storage"></a>테이블 저장소

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

최신 응용 프로그램은 이전 세대 소프트웨어가 요구하는 것보다 확장성과 유연성이 더 높은 데이터 저장소를 요구하는 경우가 많습니다. 테이블 저장소는 응용 프로그램 toomeet 사용자 요구를 자동으로 확장할 수 있도록 고가용성, 확장성이 매우 뛰어난 저장소를 제공 합니다. Table Storage는 Microsoft의 NoSQL 키/특성 저장소로, 스키마 없이 디자인되어 전통적인 관계형 데이터베이스와 차이가 있습니다. Schemaless 데이터 저장소를 쉽게 tooadapt hello 데이터 응용 프로그램 evolve의 필요성을 해결 됩니다. 테이블 저장소 쉽게 toouse 이므로 개발자 응용 프로그램을 신속 하 게 만들 수 있습니다. 액세스 toodata 신속 하 고 모든 종류의 응용 프로그램에 대 한 비용 효율적인 됩니다.  비슷한 양의 데이터일 때 Table Storage는 일반적으로 전통적인 SQL에 비해 비용이 매우 낮습니다.

테이블 저장소는 키-특성 저장소입니다. 다시 말해서, 테이블의 모든 값이 입력된 속성 이름을 사용하여 저장됩니다. hello 속성 이름은 필터링 및 선택 기준 지정에 사용할 수 있습니다. 속성 모음과 해당 값은 함께 엔터티를 구성합니다. 테이블 저장소 schemaless 이기 때문에 두 개의 엔터티가 hello 동일 테이블의 속성을 다른 컬렉션을 포함할 수 있습니다 및 해당 속성은 여러 유형이 있을 수 있습니다.

테이블 저장소 toostore 유연한 데이터 집합, 웹 응용 프로그램, 주소록, 장치 정보 및 다른 유형의 서비스에 필요한 메타 데이터에 대 한 사용자 데이터와 같이 사용할 수 있습니다.  테이블의 모든 엔터티 수를 저장할 수 있습니다 및 저장소 계정은 임의 개수의 테이블 hello 저장소 계정의 toohello 용량 한계를 포함할 수 있습니다.

그러나 Blob 및 큐와 마찬가지로 개발자가 수 및 표준 REST 프로토콜을 사용 하 여 테이블 저장소에 액세스할를 테이블 저장소도 hello OData 프로토콜의 하위 집합에서는 고급 쿼리 기능 및 JSON과 AtomPub (XML 기반)를 모두 사용을 단순화 합니다. 서식을 지정 합니다.

오늘날의 인터넷 기반 응용 프로그램에 대 한 테이블 저장소와 같은 NoSQL 데이터베이스 관계형 데이터베이스 인기 있는 대체 tootraditional을 제공합니다.

## <a name="queue-storage"></a>큐 저장소
규모를 고려하여 응용 프로그램을 디자인할 때는 응용 프로그램 구성 요소를 개별적으로 확장할 수 있도록 각 구성 요소를 분리하는 경우가 많습니다. 큐 저장소 hello 클라우드 hello 데스크톱, 온-프레미스 서버 또는 모바일 장치에서에서 실행 되는 여부를 응용 프로그램 구성 요소 간의 비동기 통신을 위해 신뢰할 수 있는 메시징 솔루션을 제공 합니다. Queue storage는 또한 비동기 작업 관리와 프로세스 워크플로 작성을 지원합니다.

저장소 계정에 포함할 수 있는 큐의 수에는 제한이 없습니다. 큐는 메시지 hello 저장소 계정의 toohello 용량 한계를 개수에 관계 없이 포함 될 수 있습니다. 개별 메시지의 크기 (kb) too64 수 있습니다.

## <a name="file-storage"></a>File Storage
Azure 파일 서비스 hello hello 표준 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 액세스할 수 있는 항상 사용 가능한 네트워크 파일 공유를 tooset이 있습니다. 여러 Vm을 공유할 수 있다는 것을 의미 동일을 hello 읽기 및 쓰기 권한이 모두 있는 파일입니다. Hello REST 인터페이스 또는 hello 저장소 클라이언트 라이브러리를 사용 하 여 hello 파일을 읽을 수도 있습니다.

Azure 파일 저장소에서 회사 파일 공유에 파일을 구별 하는 한 가지는 어디에서 든 hello 파일을 액세스할 수 있도록 toohello 파일을 가리키는 공유 액세스 서명 (SAS) 토큰을 포함 하는 URL을 사용 하는 hello world에 있습니다. SAS 토큰을 생성할 수 있습니다. 특정 기간에 대 한 특정 액세스 tooa 개인 자산을 허용합니다.

파일 공유는 다음과 같은 여러 가지 일반적인 시나리오에 사용할 수 있습니다.

* 여러 온-프레미스 응용 프로그램에서 파일 공유를 사용합니다. 이 기능을 통해 보다 쉽게 toomigrate 데이터 tooAzure를 공유 하는 해당 응용 프로그램입니다. 탑재할 hello에 같은 드라이브 문자 hello 하는 파일 공유 toohello 온-프레미스 응용 프로그램 사용 하 여, 있는 경우에 최소한 변경 하 여 hello 파일 공유에 액세스 하는 응용 프로그램의 hello 부분 작동 해야 합니다.

* 구성 파일을 파일 공유에 저장하고 여러 VM에서 액세스할 수 있습니다. 도구 및 유틸리티를 그룹에 여러 개발자가 사용 되는 모든 사용자에 게 찾을 수 있도록, 확인 하는 파일 공유에 저장할 수 있으며를 사용 하는 hello 동일한 버전입니다.

* 진단 로그, 메트릭 및 크래시 덤프는 세 개의 예 tooa 파일 공유를 작성 및 처리 하거나 나중에 분석할 수 있는 데이터입니다.

이 시간, Active Directory 기반 인증 및 액세스 제어 목록 (Acl) 지원 되지 않으며, 없지만 이후 hello에 수 있습니다. hello 저장소 계정 자격 증명이 사용 되는 tooprovide 인증 액세스 toohello 파일 공유에 대 한 합니다. 즉, 탑재 hello 공유와 모든 사용자가 모든 읽기/쓰기 액세스 toohello 공유 해야 합니다.

## <a name="access-tooblob-table-queue-and-file-resources"></a>액세스 tooBlob, 테이블, 큐 및 파일 리소스
기본적으로 저장소 계정 소유자만 hello hello 저장소 계정의 리소스에에서 액세스할 수 있습니다. 데이터의 hello 보안을 위해에서 계정의 리소스에에서 대 한 모든 요청을 인증 합니다. 인증에는 공유 키 모델이 사용됩니다. Blob에 익명 인증이 구성 된 toosupport 될 수도 있습니다.

생성 시 저장소 계정에 인증을 위해 사용되는 2개의 개인 선택키가 할당됩니다. 두 키를 갖는 것 일반적인 보안 키 관리 방법으로 정기적으로 hello 키 다시 생성 하면 응용 프로그램 계속 사용할 수 있는지 확인 합니다.

Tooallow 제어 하는 사용자가 tooyour 저장소 리소스 액세스를 해야 하는 경우 공유 액세스 서명을 만들 수 있습니다. 공유 액세스 서명 (SAS)은 사용 tooa 저장소 리소스 액세스를 위임 하는 추가 된 tooa URL 일 수 있는 토큰입니다. Toowith hello 사용 권한을 지정 하는 것을 나타내는 hello 리소스에 액세스할 수 hello 토큰을 소유한 모든 사용자에 대 hello 기간 동안에 유효 합니다. 버전 2015-04-05부터 Azure Storage는 두 가지 공유 액세스 서명(서비스 SAS, 계정 SAS)을 지원합니다.

hello 서비스 SAS 대리자 tooa 리소스 hello 저장소 서비스 중 하나에 액세스: Blob, 큐, 테이블 또는 파일 서비스 hello 합니다.

SA 계정을 하나 이상 hello 저장소 서비스에 대 한 액세스 tooresources에 위임합니다. 서비스 SAS와 함께 사용할 수 없는 액세스 tooservice 수준 작업을 위임할 수 있습니다. 또한 액세스 tooread, 쓰기 및 삭제 작업을 blob 컨테이너, 테이블, 큐 및 서비스 SAS와 함께 사용할 수 없는 파일 공유를 위임할 수 있습니다.

마지막으로, 컨테이너 및 해당 Blob 또는 특정 Blob을 공개적으로 액세스할 수 있게 지정할 수 있습니다. 컨테이너 또는 Blob을 공개로 지정하면 모든 사용자가 이 컨테이너 또는 Blob를 익명으로 읽을 수 있으며 인증이 필요 없습니다.  공용 컨테이너 및 Blob은 웹 사이트에서 호스트되는 미디어 및 문서와 같은 리소스를 노출하는 데 유용합니다.  글로벌 고객에 대 한 네트워크 대기 시간 toodecrease hello Azure CDN로 웹 사이트에서 사용 되는 blob 데이터를 캐시할 수 있습니다.

공유 액세스 서명에 대한 자세한 내용은 [SAS(공유 액세스 서명) 사용](storage-dotnet-shared-access-signature-part-1.md)을 참조하세요. 참조 [익명 읽기 권한을 toocontainers 및 blob 관리](storage-manage-access-to-resources.md) 및 [hello Azure 저장소 서비스에 대 한 인증](https://msdn.microsoft.com/library/azure/dd179428.aspx) 보안 액세스 tooyour 저장소 계정에 대 한 자세한 내용은 합니다.

## <a name="replication-for-durability-and-high-availability"></a>내구성 및 고가용성을 위한 복제
저장소 계정은 항상 Microsoft Azure의 hello 데이터 tooensure 내 구성과 고가용성을 복제 합니다. 내 데이터를 동일한 데이터 센터 또는 tooa 보조 데이터 센터를 선택 하면 복제 옵션에 따라 hello 복제 복사 합니다. 복제는에서는 데이터를 보호 하 고 일시적인 하드웨어 오류의 hello 이벤트에서 응용 프로그램 실행 시간 프로그램을 유지 합니다. 데이터가 복제 된 tooa 두 번째 데이터 센터도 hello 기본 위치에서 치명적인 오류 로부터 데이터를 보호 하는 경우.

복제를 사용 하면 저장소 계정의 hello 맞는지 [서비스 수준 계약 (SLA) 저장소에 대 한](https://azure.microsoft.com/support/legal/sla/storage/) hello 얼굴 오류의 경우에 합니다. 지 속성 및 가용성에 대 한 Azure 저장소에 대 한 정보에 대 한 hello SLA 보장을 참조 하십시오.

저장소 계정을 만들 때 hello 다음 복제 옵션 중 하나를 선택할 수 있습니다.

* **LRS(로컬 중복 저장소)** 로컬 중복 저장소는 데이터의 복제본 3개를 유지 관리합니다. LRS는 단일 지역의 단일 데이터 센터 내에서 3번 복제됩니다. LRS는 단일 데이터 센터의 hello 오류 있지만 일반적인 하드웨어 장애 로부터 데이터를 보호합니다.

    LRS는 할인가로 제공됩니다. 최대의 영속성을 위해서는 아래에 설명된 대로 지역 중복 저장소를 사용하는 것이 좋습니다.
* **ZRS(영역 중복 저장소)** 영역 중복 저장소는 데이터의 복제본 3개를 유지 관리합니다. ZRS는 LRS 보다 높은 지 속성을 제공 하는 단일 지역 내에서 또는 두 영역 간 두 toothree 시설에 걸쳐 3 번 복제 됩니다. ZRS는 데이터가 단일 지역 내에서 영속되는지 확인합니다.

    ZRS는 LRS보다 높은 수준의 영속성을 제공하지만 최대의 영속성을 위해서는 아래에 설명된 대로 지역 중복 저장소를 사용하는 것이 좋습니다.

  > [!NOTE]
  > ZRS는 현재 블록 BLOB에만 사용할 수 있으며, 2014-02-14 이상 버전에서만 지원됩니다.
  >
  > 저장소 계정이 만들어진 하 고 ZRS를 선택한 후 변환할 수는 없습니다 것 toouse tooany 다른 복제의 경우, 또는 그 반대로 입력 합니다.
  >
  >
* **GRS(지역 중복 저장소)** GRS는 데이터의 복사본을 6개 유지 관리합니다. Grs를 사용할 경우 데이터는 hello 기본 지역 내에서 3 번 복제 됩니다 하 고 보조 지역 수백 킬로미터 떨어진 hello 기본 지역 내구성 hello 가장 높은 수준은 3 번 복제 됩니다. Hello 기본 지역에서 작업이 실패의 hello 이벤트에서 Azure 저장소에는 장애 조치 toohello 보조 지역이 됩니다. GRS는 데이터가 두 개의 별도 지역에서 영속되도록 합니다.

    지역별 기본 및 보조 쌍에 대한 정보는 [Azure 영역](https://azure.microsoft.com/regions/)을 참조하세요.
* **RA-GRS(읽기 액세스 지역 중복 저장소)** 읽기 액세스 지역 중복 저장소는 데이터 tooa 보조 지리적 위치를 복제 하 고 또한 hello 보조 위치에 대 한 읽기 액세스 tooyour 데이터를 제공 합니다. 읽기 액세스 지역 중복 저장소 사용 하면 기본 hello 또는 위치로 사용할 수 없게 되는 hello 이벤트에서 hello 보조 위치에서 데이터 tooaccess 있습니다. 읽기 액세스 지역 중복 저장소는 만들 때 기본적으로 저장소 계정에 대 한 hello 기본 옵션을입니다.

  > [!IMPORTANT]
  > 어떻게 데이터가 복제 되어 저장소 계정의 만든 후 hello 계정을 만들 때 ZRS를 지정 하지 않으면 변경할 수 있습니다. 그러나는 추가 일회성 데이터 전송 LRS tooGRS 또는 RA-GRS에서 전환 비용을 청구할 수 있습니다 note 합니다.
  >
  >

저장소 복제 옵션에 대한 자세한 내용은 [Azure Storage 복제](storage-redundancy.md)를 참조하세요.

저장소 계정 복제에 대한 가격 정보는 [Azure Storage 가격](https://azure.microsoft.com/pricing/details/storage/)을 참조하세요. 각 지역에서 어떤 서비스가 가능한지에 대한 자세한 정보는 [Azure 지역](https://azure.microsoft.com/regions/#services)을 참조하세요.

Azure Storage를 통한 지속성에 대한 구조적인 세부 사항은 [SOSP 문서 - Azure Storage: 일관성과 가용성이 뛰어난 클라우드 저장소 서비스](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)를 참조하세요.

## <a name="transferring-data-tooand-from-azure-storage"></a>Azure 저장소에서 데이터 tooand 전송
저장소 계정 내에서 또는 저장소 계정에서 hello AzCopy 명령줄 유틸리티 toocopy blob, 파일 및 테이블 데이터를 사용할 수 있습니다. 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md) 자세한 정보에 대 한 합니다.

AzCopy hello 위에 빌드됩니다. 따라서 [Azure 데이터 이동을 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), 미리 보기에서 현재 사용할 수 있습니다.

hello Azure 가져오기/내보내기 서비스 방식으로 tooimport blob 데이터를 제공 하거나 toohello Azure 데이터 센터를 메일로 보내도록 하드 드라이브 디스크를 통해 저장소 계정에서 blob 데이터를 내보냅니다. Hello 가져오기/내보내기 서비스에 대 한 자세한 내용은 참조 [hello Microsoft Azure 가져오기/내보내기 서비스 tooTransfer 데이터 tooBlob 저장소를 사용 하 여](storage-import-export-service.md)합니다.

## <a name="pricing"></a>가격
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>Storage API, 라이브러리 및 도구
Azure Storage 리소스는 HTTP/HTTPS 요청을 수행할 수 있는 모든 언어로 액세스할 수 있습니다. 또한 Azure Storage는 많이 사용되는 몇 가지 언어를 위한 프로그래밍 라이브러리를 제공합니다. 이 라이브러리는 동기/비동기 호출, 작업 일괄 처리, 예외 관리, 자동 재시도, 작업자 동작 등과 같은 세부 사항을 처리하여 Azure Storage 작업의 많은 측면을 간소화합니다. 다음 언어 hello에 대 한 현재 사용할 수 있는지 확인 하 고 플랫폼에서 다른 사용자와 hello 파이프라인:

### <a name="azure-storage-data-services"></a>Azure Storage 데이터 서비스
* [저장소 서비스 REST API](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [.NET, Windows Phone 및 Windows 런타임용 저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Java/Android용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/java/)
* [Node.js용 저장소 클라이언트 라이브러리](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [PHP용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/php/)
* [Ruby용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/ruby/)
* [Python용 저장소 클라이언트 라이브러리](https://azure.microsoft.com/develop/python/)
* [PowerShell 1.0용 Storage Cmdlet](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Azure Storage 관리 서비스
* [저장소 리소스 공급자 REST API 참조](/rest/api/storagerp/)
* [.NET용 저장소 리소스 공급자 클라이언트 라이브러리](/dotnet/api/microsoft.azure.management.storage)
* [PowerShell 1.0용 저장소 리소스 공급자 Cmdlet](/powershell/module/azure.storage)
* [저장소 서비스 관리 REST API(클래식)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Azure Storage 데이터 이동 서비스
* [Storage Import/Export Service REST API](storage-import-export-service.md)
* [.NET용 저장소 데이터 이동 클라이언트 라이브러리](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>도구 및 유틸리티
* [Microsoft Azure 저장소 탐색기](../vs-azure-tools-storage-manage-with-storage-explorer.md) toowork 시각적으로 Windows, macOS 등 및 Linux에서 Azure 저장소 데이터로 사용 하면 Microsoft에서 가능한 독립 실행형 앱입니다.
* [Azure Storage 클라이언트 도구](storage-explorers.md)
* [Azure SDK 및 도구](https://azure.microsoft.com/tools/)
* [Azure Storage 에뮬레이터](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy 명령줄 유틸리티](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>다음 단계
Azure 저장소에 대해 자세히 toolearn이 리소스를 살펴봅니다.

### <a name="documentation"></a>설명서
* [Azure Storage 설명서](https://azure.microsoft.com/documentation/services/storage/)
* [저장소 계정을 만드는](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>관리자용
* [Azure Storage와 함께 Azure PowerShell 사용](storage-powershell-guide-full.md)
* [Azure Storage에서 Azure CLI 사용](storage-azure-cli.md)

### <a name="for-net-developers"></a>.NET 개발자용
* [.NET을 사용하여 Azure Blob 저장소 시작](storage-dotnet-how-to-use-blobs.md)
* [.NET을 사용하여 Azure 테이블 저장소 시작](storage-dotnet-how-to-use-tables.md)
* [.NET을 사용하여 Azure 큐 저장소 시작](storage-dotnet-how-to-use-queues.md)
* [Windows에서 Azure 파일 저장소 시작](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Java/Android 개발자용
* [어떻게 toouse Java에서 Blob 저장소](storage-java-how-to-use-blob-storage.md)
* [어떻게 toouse Java에서 테이블 저장소](storage-java-how-to-use-table-storage.md)
* [어떻게 toouse Java에서 큐 저장소](storage-java-how-to-use-queue-storage.md)
* [어떻게 toouse Java에서 파일 저장소](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Node.js 개발자용
* [어떻게 toouse Node.js에서 Blob 저장소](storage-nodejs-how-to-use-blob-storage.md)
* [어떻게 toouse Node.js에서 테이블 저장소](storage-nodejs-how-to-use-table-storage.md)
* [어떻게 toouse Node.js에서 큐 저장소](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>PHP 개발자용
* [어떻게 toouse PHP에서 Blob 저장소](storage-php-how-to-use-blobs.md)
* [어떻게 toouse PHP에서 테이블 저장소](storage-php-how-to-use-table-storage.md)
* [어떻게 toouse PHP에서 큐 저장소](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Ruby 개발자용
* [어떻게 toouse Ruby에서 Blob 저장소](storage-ruby-how-to-use-blob-storage.md)
* [어떻게 toouse Ruby에서 테이블 저장소](storage-ruby-how-to-use-table-storage.md)
* [어떻게 toouse Ruby에서 큐 저장소](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Python 개발자용
* [어떻게 toouse Python에서 Blob 저장소](storage-python-how-to-use-blob-storage.md)
* [어떻게 toouse Python에서 테이블 저장소](storage-python-how-to-use-table-storage.md)
* [어떻게 toouse Python에서 큐 저장소](storage-python-how-to-use-queue-storage.md)
* [어떻게 toouse Python에서 파일 저장소](storage-python-how-to-use-file-storage.md)
