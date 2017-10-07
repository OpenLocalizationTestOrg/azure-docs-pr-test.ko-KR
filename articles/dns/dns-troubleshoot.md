---
title: "aaaAzure DNS 문제 해결 가이드 | Microsoft Docs"
description: "Azure dns tootroubleshoot 공통 발급 하는 방법"
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
editor: 
ms.assetid: 95b01dc3-ee69-4575-a259-4227131e4f9c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/20/2017
ms.author: jonatul
ms.openlocfilehash: 944aa1811c980063f739268cd2c79b647b2754a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-troubleshooting-guide"></a>Azure DNS 문제 해결 가이드

이 페이지에서는 일반적인 Azure DNS 질문에 대한 문제 해결 정보를 제공합니다.

이 단계에서 문제를 해결하지 못하는 경우 [MSDN의 커뮤니티 지원 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WAVirtualMachinesVirtualNetwork)에서 검색하거나 문제를 게시할 수 있습니다. 또는 Azure 지원 요청을 방문하세요.


## <a name="i-cant-create-a-dns-zone"></a>DNS 영역을 만들 수 없습니다.

tooresolve 일반적인 문제는 hello 다음 단계 중 하나 이상을 시도해 보십시오.

1.  Azure DNS 감사 검토 hello toodetermine hello 실패 이유를 기록 합니다.
2.  각 DNS 영역 이름은 해당 리소스 그룹 내에서 고유해야 합니다. 즉, 두 개의 DNS 영역의 hello로 동일한 이름은 리소스 그룹을 공유할 수 없습니다. 다른 영역 이름을 사용하거나 다른 리소스 그룹을 사용해 보세요.
3.  "에 도달 했거나 hello {구독 id}를 구독에서 영역의 최대 수를 초과 했습니다." 오류가 표시 될 수 있습니다. 다른 Azure 구독을 사용, 일부 영역을 삭제 또는 구독 제한 tooraise Azure 지원에 문의 하십시오.
4.  오류가 표시 될 수 있습니다 "hello 영역 '{영역 name}'를 사용할 수 없습니다." 이 오류는 Azure DNS이 DNS 영역에 대 한 이름 서버 수 없습니다 tooallocate 했음을 의미 합니다. 다른 영역 이름을 사용해 보세요. 또는 hello 도메인 이름 소유자 인 사용자에 대 한 이름 서버를 할당할 수 있는 Azure 지원에 문의 합니다.


### <a name="recommended-documents"></a>**권장되는 문서**

[DNS 영역 및 레코드](dns-zones-records.md)
<br>
[DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md)

## <a name="i-cant-create-a-dns-record"></a>DNS 레코드를 만들 수 없습니다.

tooresolve 일반적인 문제는 hello 다음 단계 중 하나 이상을 시도해 보십시오.

1.  Azure DNS 감사 검토 hello toodetermine hello 실패 이유를 기록 합니다.
2.  레코드 집합 hello가 이미 존재 합니까?  Azure DNS 레코드를 사용 하 여 레코드를 관리 합니다. *설정*, 레코드의 이름을 지정 하 고 동일한 hello 동일 hello hello 컬렉션은 형식입니다. 경우에 동일한 이름을 지정 하 고 이미 입력 hello로 레코드가 없는 tooadd hello 기존 레코드를 편집 해야 하는 이러한 다른 레코드로 설정 합니다.
3.  발생 하는 것 toocreate hello DNS 영역 루트 (hello '루트' hello 영역)에 있는 레코드? 따라서 DNS 규칙 hello는 toouse hello 경우 ' @' 문자 hello 레코드 이름으로 합니다. 또한 hello DNS 표준 hello 영역 루트에서 CNAME 레코드를 허용 하지 않는 note 합니다.
4.  CNAME 충돌이 있나요?  hello DNS 표준 이름과 같은 다른 종류의 레코드로 이름을 hello로 CNAME 레코드를 허용 하지 않습니다. 다른 종류의 이름과 동일한 이름을 실패 hello로 레코드를 만들어 기존는 CNAME을 사용할 경우 합니다.  마찬가지로, CNAME를 만들면 실패 hello 이름이 다른 종류의 기존 레코드와 일치 합니다. 다른 레코드 또는 다른 레코드 이름 선택 hello를 제거 하 여 hello 충돌을 제거 합니다.
5.  DNS 영역에 사용할 수 있는 레코드 집합의 hello 수 hello 제한에 도달 했습니다. hello 현재 레코드 집합 수 고 hello 레코드 집합의 최대 수에에서 표시 됩니다 hello hello '속성' hello 영역에 대 한 Azure 포털입니다. 이 제한에 도달 했으므로, 다음 일부 레코드 집합을 삭제 하거나이 영역에 대 한 레코드 집합 제한 tooraise Azure 지원에 문의 하는 경우 다음 다시 시도 하십시오. 


### <a name="recommended-documents"></a>**권장되는 문서**

[DNS 영역 및 레코드](dns-zones-records.md)
<br>
[DNS 영역 만들기](dns-getstarted-create-dnszone-portal.md)



## <a name="i-cant-resolve-my-dns-record"></a>DNS 레코드를 확인할 수 없음

DNS 이름 확인은 여러 가지 이유로 실패할 수 있는 다단계 프로세스입니다. hello 다음 단계 쉽게 Azure DNS에 호스트 되는 영역에서 DNS 레코드에 대 한 DNS 확인이 실패 하는 이유를 조사할 수 있습니다.

1.  Hello DNS 레코드가 Azure DNS에서 올바르게 구성 되었는지 확인 합니다. Hello hello 영역 이름, 레코드 이름 및 레코드 종류 정확한 지 확인 하는 Azure 포털의에서 hello DNS 레코드를 검토 합니다.
2.  Hello Azure DNS 이름 서버 hello DNS 레코드가 올바르게 해결 확인 합니다.
    - 로컬 PC에서 DNS 쿼리를 만들면 hello hello 이름 서버의 현재 상태를 반영 하지 않는 캐시 된 결과 표시 될 수 있습니다.  회사 네트워크 DNS 프록시 서버를 자주 사용 되는 또한 toospecific 이름 서버 연결에서 DNS 쿼리를 방지 하는 합니다.  tooavoid 이러한 문제를 사용 하 여 웹 기반 이름 확인 서비스와 같은 [digwebinterface](http://digwebinterface.com)합니다.
    - Hello Azure 포털에에서 표시 된 대로 있는지 toospecify 프로그램 DNS 영역에 대 한 올바른 이름 서버 hello를 수 있습니다.
    - Hello DNS가 (toospecify hello 정규화 된 이름, hello 영역 이름을 포함 하 여 있어야) 정확한 hello 레코드 종류 올바른지 확인
3.  Hello DNS 도메인 이름을 올바르게 되었으면 확인 [toohello Azure DNS 이름 서버 위임](dns-domain-delegation.md)합니다. [DNS 위임 유효성 검사를 제공하는 여러 타사 웹 사이트](https://www.bing.com/search?q=dns+check+tool)가 있습니다. 이 테스트 되는 *영역* 위임 테스트 hello DNS 영역 이름 및 hello 정규화 레코드 이름이 아니라만 입력 해야 합니다.
4.  위의 hello 마치면 DNS 레코드 이제 해결 해야 올바르게 합니다. tooverify, 다시 사용할 수 있습니다 [digwebinterface](http://digwebinterface.com),이 이번에 hello 기본 이름 서버 설정을 사용 합니다.


### <a name="recommended-documents"></a>**권장되는 문서**

[도메인 tooAzure DNS 위임](dns-domain-delegation.md)



## <a name="how-do-i-specify-hello-service-and-protocol-for-an-srv-record"></a>Hello 'service' 및 ' p' SRV 레코드를 지정 하는 방법

Azure DNS 레코드 집합으로 DNS 레코드를 관리 합니다.-동일한 이름을 지정 하 고 동일한 hello hello로 레코드의 컬렉션을 hello 유형입니다. SRV 레코드 집합에 대 한 hello 'service' 및 'p' toobe hello 레코드 집합 이름의 일부로 지정 해야 합니다. hello 다른 SRV 매개 변수 (예: 'priority', 'weight', 'port' 및 'target')은 별도로 지정 되며 hello 레코드 집합의 각 레코드에 대 한 합니다.

SRV 레코드 이름(서비스 이름 'sip', 프로토콜 'tcp') 예제:

- \_sip 합니다. \_tcp (hello 영역 루트에서 설정 하는 레코드를 만듭니다)
- \_sip.\_tcp.sipservice ('sipservice'라는 이름의 레코드 생성)

### <a name="recommended-documents"></a>**권장되는 문서**

[DNS 영역 및 레코드](dns-zones-records.md)
<br>
[Hello Azure 포털을 사용 하 여 DNS 레코드 집합 및 레코드를 만들으십시오](dns-getstarted-create-recordset-portal.md)
<br>
[SRV 레코드 유형(Wikipedia)](https://en.wikipedia.org/wiki/SRV_record)


## <a name="next-steps"></a>다음 단계

* [Azure DNS 영역 및 레코드](dns-zones-records.md) 알아보기
* Azure DNS를 사용 하 여 toostart 너무 방법을 알아봅니다[DNS 영역을 만드는](dns-getstarted-create-dnszone-portal.md) 및 [DNS 레코드 만들기](dns-getstarted-create-recordset-portal.md)합니다.
* toomigrate 기존 DNS 영역을 알아보려면 어떻게 너무[DNS 영역 파일 가져오기 및 내보내기](dns-import-export.md)합니다.

