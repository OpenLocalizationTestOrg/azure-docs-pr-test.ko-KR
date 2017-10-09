---
title: "로그 분석에 aaaIIS 기록 | Microsoft Docs"
description: "IIS(인터넷 정보 서비스)는 Log Analytics에서 수집할 수 있는 로그 파일에 사용자 활동을 저장합니다.  이 문서는 hello 레코드의 세부 정보 및 IIS 로그 컬렉션 tooconfigure 작성 방법과 hello OMS 리포지토리에 대해 설명 합니다."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a>Log Analytics의 IIS 로그
IIS(인터넷 정보 서비스)는 Log Analytics에서 수집할 수 있는 로그 파일에 사용자 활동을 저장합니다.  

![IIS 로그](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a>IIS 로그 구성
Log Analytics는 IIS에서 생성된 로그 파일의 항목을 수집하므로 [로깅에 대해 IIS를 구성](https://technet.microsoft.com/library/hh831775.aspx)해야 합니다.

Log Analytics는 W3C 형식으로 저장된 IIS 로그 파일만 지원하며 사용자 지정 필드 또는 IIS 고급 로깅을 지원하지 않습니다.  
Log Analytics는 NCSA 또는 IIS 네이티브 형식의 로그를 수집하지 않습니다.

로그 분석에서 hello에서 IIS 로그를 구성 [로그 분석 설정의 데이터 메뉴](log-analytics-data-sources.md#configuring-data-sources)합니다.  **W3C 형식 IIS 로그 파일 수집**을 선택하는 것 외에 다른 구성은 필요 없습니다.

IIS 로그 컬렉션을 사용 하도록 설정 하면 각 서버에서 hello IIS 로그 롤오버 설정을 구성 해야 하는 것이 좋습니다.

## <a name="data-collection"></a>데이터 수집
Log Analytics는 연결된 각 원본에서 대략 15분마다 IIS 로그 항목을 수집합니다.  hello 에이전트를 수집 하는 각 이벤트 로그에 해당 위치를 기록 합니다.  Hello 에이전트 오프 라인인 경우 다음 로그 분석에서 이벤트를 수집 마지막 중단, 이러한 이벤트는 hello 에이전트 오프 라인 상태인 동안 생성 된 경우에 합니다.

## <a name="iis-log-record-properties"></a>IIS 로그 레코드 속성
IIS 로그 레코드에는 형식이 **W3CIISLog** 한 hello 속성의 다음 표에 hello:

| 속성 | 설명 |
|:--- |:--- |
| 컴퓨터 |이벤트 hello hello 컴퓨터의 이름에서 수집 되었습니다. |
| cIP |Hello 클라이언트의 IP 주소입니다. |
| csMethod |GET 또는 POST 등 hello 요청의 메서드. |
| csReferer |해당 hello 사이트 toohello 현재 사이트에서 사용자가 링크를 팔 로우. |
| csUserAgent |Hello 클라이언트의 브라우저 종류입니다. |
| csUserName |Hello 서버에 액세스 하는 사용자를 인증 하는 hello의 이름입니다. 익명 사용자는 하이픈으로 표시됩니다. |
| csUriStem |Hello 요청 웹 페이지 등의 대상입니다. |
| csUriQuery |쿼리를 있는 경우 해당 hello 클라이언트 tooperform을 시도 되었습니다. |
| ManagementGroupName |Operations Manager 에이전트에 대 한 hello 관리 그룹의 이름입니다.  다른 에이전트의 경우 AOI-\<작업 영역 ID\>입니다. |
| RemoteIPCountry |Hello 클라이언트의 IP 주소 hello의 국가입니다. |
| RemoteIPLatitude |위도 hello 클라이언트 IP 주소입니다. |
| RemoteIPLongitude |경도 hello 클라이언트 IP 주소입니다. |
| scStatus |HTTP 상태 코드입니다. |
| scSubStatus |하위 상태 오류 코드입니다. |
| scWin32Status |Windows 상태 코드입니다. |
| sIP |Hello 웹 서버의 IP 주소입니다. |
| SourceSystem |OpsMgr |
| sPort |Hello 서버 hello 클라이언트에 연결 된 포트입니다. |
| sSiteName |Hello IIS 사이트의 이름입니다. |
| TimeGenerated |날짜 및 시간 hello 항목 기록 되었습니다. |
| TimeTaken |시간 tooprocess hello의 길이 (밀리초)에 요청 합니다. |

## <a name="log-searches-with-iis-logs"></a>IIS 로그로 로그 검색
hello 다음 표에서 다른 로그 있는 쿼리 예의 IIS 로그 레코드를 검색 합니다.

| 쿼리 | 설명 |
|:--- |:--- |
| Type=W3CIISLog |모든 IIS 로그 레코드 |
| Type=W3CIISLog scStatus=500 |반환 상태가 500인 모든 IIS 로그 레코드입니다. |
| Type=W3CIISLog &#124; Measure count() by cIP |클라이언트 IP 주소별 IIS 로그 항목 수 |
| Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem |Count의 IIS 로그 hello 호스트 www.contoso.com에 대 한 url 항목입니다. |
| Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000 |각 IIS 컴퓨터에서 받은 총 바이트 수 |

>[!NOTE]
> 작업 영역에는 업그레이드 된 toohello 되었으면 [새 로그 분석 쿼리 언어](log-analytics-log-search-upgrade.md), 쿼리 위에 hello toohello 다음 변경 합니다.

> | 쿼리 | 설명 |
|:--- |:--- |
| W3CIISLog |모든 IIS 로그 레코드 |
| W3CIISLog &#124; where scStatus==500 |반환 상태가 500인 모든 IIS 로그 레코드입니다. |
| W3CIISLog &#124; summarize count() by cIP |클라이언트 IP 주소별 IIS 로그 항목 수 |
| W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem |Count의 IIS 로그 hello 호스트 www.contoso.com에 대 한 url 항목입니다. |
| W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000 |각 IIS 컴퓨터에서 받은 총 바이트 수 |

## <a name="next-steps"></a>다음 단계
* 로그 분석 toocollect 다른 구성 [데이터 원본](log-analytics-data-sources.md) 분석 합니다.
* 에 대 한 자세한 내용은 [검색 로그](log-analytics-log-searches.md) tooanalyze hello 데이터가 데이터 원본 및 솔루션에서 수집 합니다.
* 로그 분석 tooproactively 알려 IIS 로그에서 발견 되는 중요 한 조건을에서 경고를 구성 합니다.
