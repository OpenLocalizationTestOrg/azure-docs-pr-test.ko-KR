---
title: "Azure 로그 분석에서 분석 솔루션 aaaDNS | Microsoft Docs"
description: "설정 및 보안, 성능 및 작업에 대 한 DNS 인프라에 대 한 로그 분석 toogather 정보에서 hello DNS 분석 솔루션을 사용 합니다."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>DNS 분석 미리 보기 솔루션 hello로 DNS 인프라에 대 한 정보를 수집 합니다.

![DNS 분석 기호](./media/log-analytics-dns/dns-analytics-symbol.png)

이 문서에서는 tooset를 사용 하 여 보안, 성능 및 작업에 대 한 DNS 인프라에 대 한 Azure 로그 분석 toogather 정보에서 Azure DNS 분석 솔루션 hello 방법을 설명 합니다.

DNS 분석은 다음을 수행하는 데 도움을 줍니다.

- tooresolve 악의적인 도메인 이름을 클라이언트를 식별 합니다.
- 부실 리소스 레코드 식별
- 자주 쿼리되는 도메인 이름 및 talkative DNS 클라이언트 식별
- DNS 서버에서 요청 부하 보기
- 동적 DNS 등록 오류 보기

hello 솔루션 수집, 분석, 및 Windows DNS 분석 및 감사 로그와 DNS 서버에서 기타 관련된 데이터를 상호 연결 합니다.

## <a name="connected-sources"></a>연결된 소스

다음 표에서 hello이이 솔루션에서 지원 되는 연결 된 hello 소스를 설명 합니다.

| **연결된 원본** | **지원** | **설명** |
| --- | --- | --- |
| [Windows 에이전트](log-analytics-windows-agents.md) | 예 | hello 솔루션은 Windows 에이전트 로부터 DNS 정보를 수집합니다. |
| [Linux 에이전트](log-analytics-linux-agents.md) | 아니요 | hello 솔루션 직접 Linux 에이전트에서 DNS 정보를 수집 하지 않습니다. |
| [System Center Operations Manager 관리 그룹](log-analytics-om-agents.md) | 예 | hello 솔루션 연결 된 Operations Manager 관리 그룹의 에이전트에서 DNS 정보를 수집합니다. Hello Operations Manager 에이전트 toohello Operations Management Suite에서에서 직접 연결 필요 하지 않습니다. Hello 관리 그룹 toohello Operations Management Suite 리포지토리에서 데이터가 전달 됩니다. |
| [Azure 저장소 계정](log-analytics-azure-storage.md) | 아니요 | Azure 저장소는 hello 솔루션에서 사용 되지 않습니다. |

### <a name="data-collection-details"></a>데이터 수집 세부 정보

hello 솔루션은 수집 DNS 인벤토리 및 이벤트 관련 데이터를 DNS hello DNS 서버에서 로그 분석 에이전트를 설치한 합니다. 이 데이터 다음 tooLog 분석 업로드 및 hello 솔루션 대시보드에 나타납니다. DNS 서버, 영역 및 리소스 레코드의 hello 수와 같은 인벤토리와 관련 된 데이터는 hello DNS PowerShell cmdlet을 실행 하 여 수집 됩니다. hello 데이터 2 일 마다 한 번 업데이트 됩니다. hello에서 실시간에 가까운 hello 이벤트 관련 데이터를 수집 [분석 및 로그 감사](https://technet.microsoft.com/library/dn800669.aspx#enhanc) 향상 된 DNS 로깅 및 진단에 Windows Server 2012 r 2에서 제공 합니다.

## <a name="configuration"></a>구성

다음 정보 tooconfigure hello 솔루션 hello를 사용 합니다.

- 있어야는 [Windows](log-analytics-windows-agents.md) 또는 [Operations Manager](log-analytics-om-agents.md) toomonitor 되도록 각 DNS 서버에 에이전트입니다.
- Hello에서 hello DNS 분석 솔루션 tooyour Operations Management Suite 작업 영역을 추가할 수 있습니다 [Azure 마켓플레이스](https://aka.ms/dnsanalyticsazuremarketplace)합니다. 에 설명 된 hello 프로세스를 사용할 수도 있습니다 [hello 솔루션 갤러리에서에서 추가할 로그 분석 솔루션](log-analytics-add-solutions.md)합니다.

hello 솔루션 hello 추가 구성은 필요 하지 않고 데이터 수집을 시작 합니다. 그러나 구성 toocustomize 데이터 수집을 수행 하는 hello를 사용할 수 있습니다.

### <a name="configure-hello-solution"></a>Hello 솔루션 구성

Hello 솔루션 대시보드에서 **구성** tooopen hello DNS 분석 구성 페이지입니다. 다음과 같은 2가지 유형의 구성 변경을 수행할 수 있습니다.

- **허용 목록에 포함된 도메인 이름**. hello 솔루션에서 모든 hello 조회 쿼리를 처리 하지 않습니다. 도메인 이름 접미사의 허용 목록이 유지됩니다. 이 허용 목록에 도메인 이름 접미사와 일치 하는 toohello 도메인 이름을 확인 하는 hello 조회 쿼리가 hello 솔루션에 의해 처리 되지 않습니다. 허용 목록 도메인 이름을 처리 하 고 있지 tooLog 분석을 전송 toooptimize hello 데이터는 데 도움이 됩니다. hello 기본 화이트 리스트 www.google.com 및 www.facebook.com 같은 인기 있는 공용 도메인 이름이 포함 되어 있습니다. Hello 전체 기본 목록을 스크롤하여 볼 수 있습니다.

 Hello 목록 tooadd 도메인 이름 접미사에 대 한 조회 insights tooview를 수정할 수 있습니다. 에 대 한 조회 insights tooview 의도 하지 않은 모든 도메인 이름 접미사를 제거할 수 있습니다.

- **Talkative 클라이언트 임계값** Hello 조회 요청 수는 hello로 강조 표시에 대 한 hello 임계값을 초과 하는 DNS 클라이언트 **DNS 클라이언트** 블레이드입니다. hello 기본 임계값은 1, 000입니다. Hello 임계값을 편집할 수 있습니다.

    ![허용 목록에 포함된 도메인 이름](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>관리 팩

Hello Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite 작업 영역을 사용 하는 경우 hello 다음 관리 팩이 설치 되어 있습니다.

- Microsoft DNS 데이터 수집기 인텔리전스 팩(Microsft.IntelligencePacks.Dns)

Operations Manager 관리 그룹에 연결 된 tooyour Operations Management Suite 작업 영역 이면 hello 다음 관리 팩에에서 설치 됩니다 Operations Manager이이 솔루션을 추가 합니다. 이 관리 팩에 대한 구성 또는 유지 관리는 필요 없습니다.

- Microsoft DNS 데이터 수집기 인텔리전스 팩(Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS 분석 구성(Microsoft.IntelligencePack.Dns.Configuration)

솔루션 관리 팩 업데이트 되는 방식에 대 한 자세한 내용은 참조 하십시오. [Operations Manager 연결 tooLog 분석](log-analytics-om-agents.md)합니다.

## <a name="use-hello-dns-analytics-solution"></a>Hello DNS 분석 솔루션을 사용 하 여

이 섹션에서는 모든 hello 대시보드 기능을 설명 및 방법을 toouse 해당 합니다.

Hello 솔루션 tooyour 작업 영역을 추가한 후 hello 솔루션 타일 hello Operations Management Suite 개요 페이지에서 간단히 요약 한 DNS 인프라를 제공 합니다. Hello hello 데이터 수집 되 고 DNS 서버 수가 포함 됩니다. 지난 24 시간 동안 클라이언트 tooresolve 악의적인 도메인 hello에 의해 만들어진 요청 hello 수가 포함 됩니다. Hello 타일을 클릭 하면 hello 솔루션 대시보드가 열립니다.

![DNS 분석 타일](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>솔루션 대시보드

hello 솔루션 대시보드 hello 솔루션의 다양 한 기능 hello에 대 한 요약된 정보를 표시합니다. 링크가 포함 되어 toohello 법정 분석 및 진단에 대 한 보기를 자세히 설명 합니다. 기본적으로 hello 데이터가 지난 7 일 hello에 대 한 표시 됩니다. Hello를 사용 하 여 hello 날짜 및 시간 범위를 변경할 수 있습니다 **날짜 및 시간 선택 컨트롤**hello 다음 이미지에에서 나타난 것 처럼:

![시간 선택 컨트롤](./media/log-analytics-dns/dns-time.png)

hello 솔루션 대시보드 블레이드 다음 hello를 보여 줍니다.

**DNS 보안**. 보고서에 악의적인 도메인과 toocommunicate를 시도 하는 DNS 클라이언트 hello 합니다. Microsoft 위협 인텔리전스 피드를 사용 하 여 DNS 분석 클라이언트 tooaccess 악의적인 도메인을 시도 하 고 있는 Ip를 검색할 수 있습니다. 대부분의 경우에서 맬웨어 감염 된 장치 "전화" toohello "명령 및 제어" 센터를 확인 하 여 hello 악의적인 도메인의 도메인 이름 맬웨어 hello 합니다.

![DNS 보안 블레이드](./media/log-analytics-dns/dns-security-blade.png)

Hello 목록에 클라이언트 IP를 클릭 하면 로그 검색 열리고 hello 해당 쿼리의 hello 조회 세부 정보를 표시 합니다. 다음 예제는 hello, DNS 분석 감지 hello 통신으로 수행 했던는 [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![ircbot을 표시하는 로그 검색 결과](./media/log-analytics-dns/ircbot.png)

hello 정보를 사용 하면 tooidentify에서:

- 클라이언트 hello 통신을 시작한 IP입니다.
- Toohello 악성 IP 확인 되는 도메인 이름입니다.
- Hello 도메인 이름을 IP 주소를 확인 합니다.
- 악의적인 IP 주소
- Hello 문제의 심각도입니다.
- Hello 악성 IP 차단 목록에 대 한 설명입니다.
- 검색 시간

**도메인 쿼리함**. 사용자 환경에서 hello DNS 클라이언트가 쿼리 중인 hello 빈도가 가장 높은 도메인 이름을 제공 합니다. Hello 목록을 쿼리 하는 모든 hello 도메인 이름 볼 수 있습니다. 또한 로그 검색에서 특정 도메인 이름의 hello 조회 요청 세부 정보로 다운 드릴 수 있습니다.

![도메인 쿼리함 블레이드](./media/log-analytics-dns/domains-queried-blade.png)

**DNS 클라이언트**. 보고서에는 클라이언트 hello *hello 임계값 졌는 지* hello 선택한 기간에에서는 쿼리 수입니다. Hello 목록이 모든 hello DNS 클라이언트 및 로그 검색에에 의해 만들어진 hello 쿼리의 hello 세부 정보를 볼 수 있습니다.

![DNS 클라이언트 블레이드](./media/log-analytics-dns/dns-clients-blade.png)

**동적 DNS 등록**. 이름 등록 오류를 보고합니다. 주소에 대 한 모든 등록 실패 [리소스 레코드](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (형식 A 및 AAAA) hello 클라이언트 hello 등록 요청을 수행한 Ip와 함께 강조 표시 됩니다. 그런 다음 이러한 단계를 수행 하 여 hello 등록 실패의이 정보 toofind hello 근본 원인을 사용할 수 있습니다.

1. 클라이언트 hello hello 이름에 대 한 권한이 있는 hello 영역 tooupdate 시도 찾습니다.

2. 해당 영역의 hello 솔루션 toocheck hello 인벤토리 정보를 사용 합니다.

3. Hello 영역에 대 한 해당 hello 동적 업데이트를 확인 합니다.

4. 보안 동적 업데이트에 대 한 hello 영역이 구성 되어 있는지 여부를 확인 합니다.

    ![동적 DNS 등록 블레이드](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**이름 등록 요청**. hello 위 타일에는 DNS 동적 업데이트 요청 성공 및 실패 한 추세선을 표시합니다. hello 낮은 타일 hello 상위 10 개의 클라이언트가 전송 하는 실패 한 DNS 업데이트 요청 오류의 hello 수로 정렬 toohello DNS 서버를 나열 합니다.

![이름 등록 요청 블레이드 ](./media/log-analytics-dns/name-reg-req-blade.png)

**샘플 DDI 분석 쿼리** 직접 원시 분석 데이터를 인출 하는 hello 가장 일반적인 검색 쿼리 목록이 포함 됩니다.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![샘플 쿼리](./media/log-analytics-dns/queries.png)

이러한 쿼리를 시작점으로 사용하여 사용자 지정 보고를 위한 쿼리를 만들 수 있습니다. hello 쿼리 연결할 toohello DNS 분석 로그 검색 페이지 결과가 표시 됩니다.

- **DNS 서버 목록**. 연결된 FQDN, 도메인 이름, 포리스트 이름 및 서버 IP와 함께 모든 DNS 서버 목록을 표시합니다.
- **DNS 영역 목록**. DNSSEC 서명 상태 hello 연결된 영역 이름, 동적 업데이트 상태, 이름 서버와 모든 DNS 영역 목록이 표시 됩니다.
- **사용되지 않은 리소스 레코드**. 모든 hello 부실/사용 되지 않는 리소스 레코드의 목록을 표시합니다. 이 목록에는 hello 리소스 레코드 이름, 리소스 레코드 종류, DNS 서버에 연결 하는 hello, 레코드 생성 시간 및 영역 이름을 포함합니다. 이 목록 tooidentify hello DNS 리소스 레코드를 사용 하에서는 더 이상 사용할 수 없습니다. 이 정보에 따라 hello DNS 서버에서 이러한 항목을 다음 제거할 수 있습니다.
- **DNS 서버 쿼리 로드**. DNS 서버에 DNS를 로드 하는 hello의 관점을 얻을 수 있도록 정보가 표시 됩니다. 이 정보는 hello 서버에 대 한 hello 용량을 계획 하는 데 유용 합니다. Toohello 이동할 수 있습니다 **메트릭** toochange hello 보기 tooa 그래픽 시각화를 탭 합니다. 이 보기는 DNS 서버에서 DNS를 로드 하는 hello은 분산 하는 방법을 이해 하도록 도와 줍니다. 각 서버에 대한 DNS 쿼리 속도 추세가 표시됩니다.

    ![DNS 서버 쿼리 로그 검색 결과](./media/log-analytics-dns/dns-servers-query-load.png)

- **DNS 영역 쿼리 로드**. Hello 솔루션에서 관리 되는 hello DNS 서버에서 DNS 초당 영역 쿼리 통계는 모든 hello 영역 hello를 표시 합니다. Hello 클릭 **메트릭** hello 결과의 세부 레코드 tooa 그래픽 시각화에서 toochange hello 보기를 탭 합니다.
- **구성 이벤트**. 모든 hello DNS 구성 변경 이벤트와 연결 된 메시지를 표시합니다. Hello 이벤트, 이벤트 ID, DNS 서버 시간에 따라 이러한 이벤트를 필터링 할 수 있습니다 또는 작업 범주입니다. hello 데이터는 특정 시간에 변경 내용을 toospecific DNS 서버를 감사 하는 데 도움이 됩니다.
- **DNS 분석 로그**. Hello 솔루션에서 관리 하는 모든 hello DNS 서버에서 모든 hello 분석 이벤트를 표시 합니다. 그런 다음 hello 이벤트, 이벤트 ID, DNS 서버, 클라이언트 IP 조회 쿼리 hello 및 유형 작업 범주를 쿼리 하는 시간에 따라 이러한 이벤트를 필터링 할 수 있습니다. DNS 서버에 대 한 분석 이벤트 활동 hello DNS 서버에서 추적을 사용 하도록 설정 합니다. 분석 이벤트가 hello 서버 보내거나 DNS 정보를 받을 때마다 기록 됩니다.

### <a name="search-by-using-dns-analytics-log-search"></a>DNS 분석 로그 검색을 사용하여 검색

Hello 로그 검색 페이지에서 쿼리를 만들 수 있습니다. 패싯 컨트롤을 사용하여 검색 결과를 필터링할 수 있습니다. 또한 결과 tootransform 고급 쿼리, 필터 및 보고서를 만들 수 있습니다. 다음 쿼리는 hello를 사용 하 여 시작 합니다.

1. Hello에 **검색 쿼리 상자**, 형식 `Type=DnsEvents` tooview 모든 hello hello 솔루션에서 관리 하는 hello DNS 서버에 의해 생성 된 DNS 이벤트입니다. hello 결과 모든 이벤트 관련된 toolookup 쿼리, 동적 등록 및 구성 변경에 대 한 hello 로그 데이터를 나열합니다.

    ![DnsEvents 로그 검색](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. tooview hello 로그 데이터 조회 쿼리를 선택 **LookUpQuery** hello로 **하위** hello 왼쪽에 패싯 컨트롤 hello에서에서 필터입니다. 선택한 기간 hello에 대 한 모든 hello 조회 쿼리 이벤트를 나열 하는 테이블 표시 됩니다.

    b. 동적 등록에 대 한 tooview hello 로그 데이터 선택 **DynamicRegistration** hello로 **하위** hello 왼쪽에 패싯 컨트롤 hello에서에서 필터입니다. 선택한 기간 hello에 대 한 모든 hello 동적 등록 이벤트를 나열 하는 테이블 표시 됩니다.

    c. tooview hello 로그 데이터의 구성 변경 내용 선택 **ConfigurationChange** hello로 **하위** hello 왼쪽에 패싯 컨트롤 hello에서에서 필터입니다. 특정 기간 hello에 대 한 모든 hello 구성 변경 이벤트를 나열 하는 테이블 표시 됩니다.

2. Hello에 **검색 쿼리 상자**, 형식 `Type=DnsInventory` tooview 모든 hello hello 솔루션에서 관리 하는 hello DNS 서버에 대 한 DNS 인벤토리와 관련 된 데이터입니다. hello 결과 hello 로그 데이터에 대 한 DNS 서버, DNS 영역 리소스 레코드를 나열합니다.

    ![DnsInventory 로그 검색](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>사용자 의견

두 가지 방법으로 사용자 의견을 제공할 수 있습니다.

- **UserVoice**. DNS 분석 기능 toowork에 대 한 아이디어를 게시 합니다. Hello 방문 [Operations Management Suite UserVoice 페이지](https://aka.ms/dnsanalyticsuservoice)합니다.
- **코호트 가입**. 항상 조인 우리의 패 거리 들은 tooget 초기 액세스 toonew 기능 및 DNS 분석을 개선할 수 있도록 새로운 고객의 관심이 합니다. 코호트 가입에 관심이 있는 경우 [빠른 설문 조사](https://aka.ms/dnsanalyticssurvey)에 참여하세요.

## <a name="next-steps"></a>다음 단계

[로그 검색](log-analytics-log-searches.md) tooview DNS 로그 레코드를 자세히 설명 합니다.
