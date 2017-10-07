---
title: "aaaDNS 영역 및 개요-Azure DNS 기록 | Microsoft Docs"
description: "Microsoft Azure DNS에서 DNS 영역 및 레코드 호스팅에 대한 지원 개요."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: be4580d7-aa1b-4b6b-89a3-0991c0cda897
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: jonatul
ms.openlocfilehash: f214c3e2e810a80a000281820acd35f0aaf5a7e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-dns-zones-and-records"></a>DNS 영역 및 레코드 개요

이 페이지에서는 도메인, DNS 영역 및 DNS 레코드 및 레코드 집합 및 Azure DNS에서 지원 되는 방식의 hello 주요 개념을 설명 합니다.

## <a name="domain-names"></a>도메인 이름

Domain Name System hello 도메인의 계층입니다. hello 계층 구조 이름이 단순히 hello '루트' 도메인에서 시작 '**.**'.  그 아래에 'com', 'net', 'org', 'uk' 또는 'jp'와 같은 최상위 도메인이 있습니다.  그 아래에 'org.uk' 또는 'co.jp'와 같은 두 번째 수준의 도메인이 있는 hello 도메인 hello DNS 계층 구조에 전체적으로 배포 됩니다 hello 전 세계 DNS 이름 서버에서 호스트.

도메인 이름 등록 기관 toopurchase 만든 'contoso.com' 등의 도메인 이름을 사용 하면 하는 조직입니다.  도메인 이름을 제공 오른쪽 toocontrol hello DNS에서 계층 구조에서 해당 이름의 예를 들어 toodirect hello 이름 'www.contoso.com' tooyour 회사 웹 사이트를 허용 hello 구입 합니다. hello 등록 기관에서 자동으로 자체 이름 서버 hello 도메인을 호스팅할 수도 toospecify 대체 이름 서버를 사용 하면 있습니다.

Azure DNS 수 있는 전 세계적으로 분산, 고가용성 이름 서버 인프라를 제공 toohost 사용자 도메인을 사용 합니다. Azure dns에서 도메인 호스팅하여 hello로 DNS 레코드를 관리할 수 있습니다 동일한 자격 증명, Api, 도구, 청구 및 기타 Azure 서비스를 지원 합니다.

Azure DNS는 현재 도메인 이름 구입을 지원하지 않습니다. Toopurchase 도메인 이름, 원하는 경우 제 3 자 도메인 이름 등록 기관 toouse를 해야 합니다. hello 등록 기관에는 일반적으로 작은 연간 요금 요금. hello 도메인의 DNS 레코드 관리용 Azure DNS에서 호스팅할 수 있습니다. 참조 [도메인 tooAzure DNS 위임](dns-domain-delegation.md) 대 한 자세한 내용은 합니다.

## <a name="dns-zones"></a>DNS 영역 

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="dns-records"></a>DNS 레코드

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

### <a name="time-to-live"></a>Time-to-Live

hello 시간 toolive, 또는 TTL, 다시 쿼리 중인 하기 전에 클라이언트에서 각 레코드 캐시 되는 기간을 지정 합니다. 위 예제는 hello, hello TTL은 3600 초 또는 1 시간입니다.

Azure DNS TTL은 각 레코드에 대 한 하지 hello 레코드 집합에 대 한 지정 된 hello에에서 있으므로 해당 레코드 내의 모든 레코드에 대해 동일한 값이 사용 하는 hello 설정 합니다.  1 ~ 2,147,483,647초 사이의 TTL 값을 지정할 수 있습니다.

### <a name="wildcard-records"></a>와일드카드 레코드

Azure DNS는 [와일드카드 레코드](https://en.wikipedia.org/wiki/Wildcard_DNS_record)를 지원합니다. 와일드 카드 레코드 (비 와일드 카드 레코드 집합에서 더 알맞은 아니면) 이름이 일치 하는 응답 tooany 쿼리에서 반환 됩니다. Azure DNS는 NS 및 SOA를 제외한 모든 레코드 종류에 대해 와일드카드 레코드 집합을 지원합니다.

와일드 카드 레코드 toocreate 설정 hello 레코드 집합 이름을 사용 합니다. '\*'. 또는 맨 왼쪽의 레이블로 '\*'가 포함된 이름을 사용할 수 있습니다(예: '\*.foo').

### <a name="cname-records"></a>CNAME 레코드

CNAME 레코드 집합 공존할 수 없으며 hello로 다른 레코드 집합에서 같은 이름입니다. 예를 들어 hello 상대 이름이 'w w w'를 사용 하 여 설정 하는 CNAME 레코드를 만들 수 없습니다 및 동일한 hello 상대 이름이 'w w w'에 hello 사용 하 여 A 기록 시간입니다.

때문에 hello 영역 루트 (이름 = ' @') hello NS 및 SOA 레코드를 포함 하는 항상 hello 영역을 만들 때 생성 된 집합을 hello 영역 루트에서 설정 하는 CNAME 레코드를 만들 수 없습니다.

이러한 제약 조건은 hello DNS 표준에서 발생 하 고 Azure DNS의 제한 없는 합니다.

### <a name="ns-records"></a>NS 레코드

hello NS 레코드 hello 영역 루트에서 설정 (name ' @')은 자동으로 각 DNS 영역과 만들어지며 hello 영역 삭제 될 때 자동으로 삭제 됩니다 (삭제할 수 없습니다 별도로).

이 레코드 집합에는 hello Azure DNS 이름 서버 할당된 toohello 영역의 hello 이름이 포함 됩니다. 추가 이름 서버 toothis NS 레코드 집합을 공동 도메인 DNS 공급자를 둘 이상의 호스팅 toosupport를 추가할 수 있습니다. 또한 TTL hello 및이 레코드 집합에 대 한 메타 데이터를 수정할 수 있습니다. 그러나 제거 하거나 hello 미리 채워진된 Azure DNS 이름 서버를 수정할 수 없습니다. 

Note이 적용 hello 영역 루트에서 레코드 집합 toohello NS만 됩니다. (사용 되는 toodelegate 하위 영역)으로 시간대에서 다른 NS 레코드 집합 작성, 수정 및 제약 조건 없이 삭제 합니다.

### <a name="soa-records"></a>SOA 레코드

각 영역의 hello 루트에 SOA 레코드 집합을 자동으로 생성 됩니다 (이름 = ' @'), hello 영역 삭제 될 때 자동으로 삭제 됩니다.  SOA 레코드는 별도로 생성 또는 삭제할 수 없습니다.

Azure DNS에서 제공 하는 미리 구성 된 toorefer toohello 주 이름 서버 이름을 hello 'host' 속성을 제외 하 고 hello SOA 레코드의 모든 속성을 수정할 수 있습니다.

### <a name="spf-records"></a>SPF 레코드

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="srv-records"></a>SRV 레코드

[SRV 레코드](https://en.wikipedia.org/wiki/SRV_record) 다양 한 서비스 toospecify 서버 위치에서 사용 됩니다. Azure DNS에서 SRV 레코드를 지정할 경우

* hello *서비스* 및 *프로토콜* hello 레코드 집합 이름의 일부로 지정 된, 밑줄 접두사로 추가 해야 합니다.  예를 들어 '\_sip.\_tcp.name'입니다.  Hello 영역 루트에서 레코드에 대 한이 없는 필요 toospecify ' @' hello 레코드 이름 하기만 하면 사용 하 여 hello 서비스 및 프로토콜, 예를 들어 '\_sip.\_ tcp'.
* hello *우선 순위*, *가중치*, *포트*, 및 *대상* hello 레코드 집합의 각 레코드의 매개 변수로 지정 됩니다.

### <a name="txt-records"></a>TXT 레코드

TXT 레코드는 사용 되는 toomap 도메인 이름을 tooarbitrary 텍스트 문자열입니다. 여러 응용 프로그램에서는 hello 등 특히 관련된 tooemail 구성 사용 하는 [보낸 사람 정책 프레임 워크 (SPF)](https://en.wikipedia.org/wiki/Sender_Policy_Framework) 및 [DomainKeys 식별 된 메일 (DKIM)](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail)합니다.

hello DNS 표준은 단일 TXT 레코드 toocontain too254 자 하거나 나타낼 수 있으며 각 하는 여러 문자열을 허용 합니다. 여러 문자열이 사용되는 경우 이러한 문자열은 클라이언트에 의해 연결되고 단일 문자열로 처리됩니다.

Hello Azure DNS REST API를 호출할 때 필요한 toospecify 각 TXT 문자열 별도로 합니다.  Hello Azure 포털을 사용할 때 PowerShell 또는 CLI 인터페이스 지정 해야 자동으로 구분 되어 254 자 세그먼트로 필요한 경우 레코드당 단일 문자열입니다.

TXT 레코드 집합의 여러 TXT 레코드 hello 하는 hello DNS 레코드의 여러 문자열와 일치 하지 않습니다.  TXT 레코드 집합은 여러 레코드를 포함할 수 있으며 *각각의 레코드*는 여러 문자열을 포함할 수 있습니다.  Azure DNS 세트 (모든 레코드를 결합) 각 TXT 레코드의 총 문자열 길이는 too1024 문자를 지원 합니다.

## <a name="tags-and-metadata"></a>태그 및 메타데이터

### <a name="tags"></a>태그들

태그 이름-값 쌍의 목록이 되며 Azure 리소스 관리자 toolabel 리소스에서 사용 됩니다.  Azure 리소스 관리자, Azure 청구서의 태그 필터링 tooenable 뷰를 사용 하 여을 통해 있습니다 tooset 정책 태그에는 필요 합니다. 태그에 대 한 자세한 내용은 참조 [를 사용 하 여 Azure 리소스를 tooorganize 태그](../azure-resource-manager/resource-group-using-tags.md)합니다.

Azure DNS에서는 DNS 영역 리소스에 Azure Resource Manager 태그를 사용할 수 있으며  아래 설명된 대로 대체 ‘메타데이터’가 DNS 레코드 집합에서 지원되기는 하지만 DNS 레코드 집합의 태그는 지원하지 않습니다.

### <a name="metadata"></a>Metadata

대체 toorecord 태그 설정, Azure DNS 'metadata'를 사용 하 여 레코드 집합을 주석 처리를 지원 합니다.  비슷한 tootags 있습니다 tooassociate 이름-값 쌍으로 각 레코드 집합 메타 데이터를 사용 합니다.  이 유용할 수 있습니다, 그리고 예를 들어 각 레코드의 toorecord hello 목적은 설정 합니다.  태그와는 달리 메타 데이터 사용된 tooprovide, Azure 청구서의 필터링 된 뷰일 수 없습니다 및 Azure 리소스 관리자 정책에서 지정할 수 없습니다.

## <a name="etags"></a>Etag

두 사람이 나 두 프로세스 시도 toomodify 가정 DNS에서 레코드를 hello 동일한 시간입니다. 어느 쪽이 성공할까요? 및 hello 승자 알고 있는지 다른 사용자가 만든 변경 내용을 덮어은?

Azure DNS toohandle 동시 변경 toohello Etag를 사용 하 여 동일한 리소스 안전 하 게 합니다. Etags는 [Azure Resource Manager '태그'](#tags)와 구분됩니다. 각 DNS 리소스(영역 또는 레코드 집합)에는 Etag가 연결되어 있습니다. 리소스를 검색할 때마다 해당 Etag도 검색됩니다. 리소스를 업데이트할 때 다시 toopass hello Etag Azure DNS hello 서버 일치 해당 hello Etag를 확인할 수 있도록 선택할 수 있습니다. 각 업데이트 tooa 리소스 Etag 다시 생성 되 고 hello에 결과가 이후 Etag 불일치 동시 변경 발생 했음을 나타냅니다. Hello 리소스가 이미 존재 하지 않는 새 리소스 tooensure를 만들 때 Etag은 사용할 수도 있습니다.

기본적으로 Azure DNS PowerShell Etag tooblock 동시 변경 toozones 및 레코드 집합을 사용합니다. 선택적 hello *-덮어쓰기* 스위치 사용된 toosuppress Etag 검사를 수 있으며,이 경우 모든 동시에 발생 한 변경 내용을 덮어씁니다.

Hello Azure DNS REST API의 hello 수준 Etag는 HTTP 헤더를 사용 하 여 지정 됩니다.  해당 명령의 동작은 다음 표에 hello에 제공 됩니다.

| 헤더 | 동작 |
| --- | --- |
| 없음 |PUT 항상 성공(Etag 검사 안 함) |
| If-match <etag> |리소스가 있고 Etag가 일치하는 경우에만 PUT 성공 |
| If-match * |리소스가 있는 경우에만 PUT 성공 |
| If-none-match * |리소스가 없는 경우에만 PUT 성공 |


## <a name="limits"></a>제한

기본 제한 값을 다음 hello Azure DNS를 사용 하는 경우에 적용 됩니다.

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

## <a name="next-steps"></a>다음 단계

* Azure DNS를 사용 하 여 toostart 너무 방법을 알아봅니다[DNS 영역을 만드는](dns-getstarted-create-dnszone-portal.md) 및 [DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md)합니다.
* toomigrate 기존 DNS 영역을 알아보려면 어떻게 너무[DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md)합니다.
