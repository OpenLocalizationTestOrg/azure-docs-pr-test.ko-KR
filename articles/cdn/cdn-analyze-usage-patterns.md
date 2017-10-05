---
title: "Azure CDN 사용 패턴 분석 | Microsoft Docs"
description: "다음과 같은 보고서를 사용하여 CDN 사용 패턴을 볼 수 있습니다. 대역폭, 전송되는 데이터, 적중 횟수, 캐시 상태, 캐시 적중률, 전송되는 IPv4/IPv6 데이터"
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 5a0d9018-8bdb-48ff-84df-23648ebcf763
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: aadbe872dd3384c8d337b432fb3be69422ca322b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-azure-cdn-usage-patterns"></a>Azure CDN 사용 패턴 분석

[!INCLUDE[cdn-verizon-only](../../includes/cdn-verizon-only.md)]

아래 가이드에서는 Verizon 프로필에 대한 관리 포털을 통해 핵심 보고서를 확인하는 단계를 진행합니다. 또한 Verizon 및 Akamai 프로필에 대한 핵심 분석 데이터를 [Azure Portal을 통해](cdn-log-analysis.md) 저장소, 이벤트 허브 또는 Log Analytics(OMS)로 내보낼 수도 있습니다.

다음과 같은 보고서를 사용하여 CDN 사용 패턴을 볼 수 있습니다.

* 대역폭
* 전송되는 데이터
* 적중 횟수
* 캐시 상태
* 캐시 적중률
* 전송되는 IPv4/IPv6 데이터

## <a name="accessing-core-reports"></a>핵심 보고서 액세스
1. CDN 프로필 블레이드에서 **관리** 단추를 클릭합니다.
   
    ![CDN 프로필 블레이드 관리 단추](./media/cdn-reports/cdn-manage-btn.png)
   
    CDN 관리 포털이 열립니다.
2. **분석** 탭을 마우스로 가리킨 후 **핵심 보고서** 플라이아웃을 마우스로 가리킵니다.  메뉴에서 원하는 보고서를 클릭합니다.
   
    ![CDN 관리 포털 - 핵심 보고서 메뉴](./media/cdn-reports/cdn-core-reports.png)

## <a name="bandwidth"></a>대역폭
대역폭 보고서는 특정 기간의 HTTP 및 HTTPS 대역폭 사용량을 나타내는 그래프와 데이터 테이블로 구성됩니다. 모든 CDN POP 또는 특정 POP의 대역폭 사용량을 볼 수 있습니다. 이렇게 하면 CDN POP 간에 트래픽 급증 및 분산을 Mbps 단위로 볼 수 있습니다.

* 모든 에지 노드를 선택하여 모든 노드의 트래픽을 보거나 드롭다운 목록에서 특정 지역/노드를 선택합니다.
* 날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.
* "이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.

보고서는 5분마다 업데이트됩니다.

![대역폭 보고서](./media/cdn-reports/cdn-bandwidth.png)

## <a name="data-transferred"></a>전송되는 데이터
이 보고서는 특정 기간의 HTTP 및 HTTPS 트래픽 사용량을 나타내는 그래프와 데이터 테이블로 구성됩니다. 모든 CDN POP 또는 특정 POP의 트래픽 사용량을 볼 수 있습니다. 이렇게 하면 CDN POP 간에 트래픽 급증 및 분산을 GB 단위로 볼 수 있습니다.

* 모든 에지 노드를 선택하여 모든 노드의 트래픽을 보거나 드롭다운 목록에서 특정 지역/노드를 선택합니다.
* 날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.
* "이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.

보고서는 5분마다 업데이트됩니다.

![전송되는 데이터 보고서](./media/cdn-reports/cdn-data-transferred.png)

## <a name="hits-status-codes"></a>적중 횟수(상태 코드)
이 보고서는 콘텐츠에 대한 요청 상태 코드의 분포를 설명합니다. 각 콘텐츠 요청에서 HTTP 상태 코드가 생성됩니다. 상태 코드는 에지 POP가 요청을 처리한 방식을 설명합니다. 예를 들어 2xx 상태 코드는 요청이 클라이언트로 성공적으로 처리되었음을 나타내는 반면, 4xx 상태 코드는 오류가 발생했음을 나타냅니다. HTTP 상태 코드에 대한 자세한 내용은 [상태 코드](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)를 참조하세요.

* 날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.
* "이동" 옆에 있는 Excel 시트를 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.

![적중 횟수 보고서](./media/cdn-reports/cdn-hits.png)

## <a name="cache-statuses"></a>캐시 상태
이 보고서는 클라이언트 요청에 대한 캐시 적중 횟수 및 캐시 누락 수 분포를 설명합니다. 캐시 적중 횟수에서 가장 빠른 성능이 제공되므로 캐시 누락 수를 최소화하여 데이터 전달 속도를 최적화할 수 있습니다. "no-cache" 응답 헤더를 방지하도록 원본 서버를 구성하고, 엄격하게 필요한 경우를 제외하고 쿼리 문자열 캐싱을 방지하고, 캐시할 수 없는 응답 코드를 방지하여 캐시 누락 수를 줄일 수 있습니다. 자산의 max-age를 최대한 길게 설정하여 원본 서버에 대한 요청 수를 최소화하면 만료된 캐시 적중 횟수를 방지할 수 있습니다.

![캐시 상태 보고서](./media/cdn-reports/cdn-cache-statuses.png)

### <a name="main-cache-statuses-include"></a>기본 캐시 상태는 다음과 같습니다.
* TCP_HIT: 에지에서 처리됩니다. 개체가 캐시에 있었으며 max-age를 초과하지 않았습니다.
* TCP_MISS: 원본에서 처리됩니다. 개체가 캐시에 없었으며 응답이 다시 원본으로 전송되었습니다.
* TCP_EXPIRED _MISS: 원본을 사용하여 유효성을 재검사한 후 원본에서 처리됩니다. 개체가 캐시에 있었지만 max-age를 초과했습니다. 원본을 사용하여 유효성을 재검사한 후 캐시 개체가 원본의 새 응답으로 대체되었습니다.
* TCP_EXPIRED _HIT: 원본을 사용하여 유효성을 재검사한 후 에지에서 처리됩니다. 개체가 캐시에 있었지만 max-age를 초과했습니다. 원본 서버를 사용하여 유효성을 재검사한 후 캐시 개체가 수정되지 않았습니다.
* 날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.
* "이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.

### <a name="full-list-of-cache-statuses"></a>캐시 상태 전체 목록
* TCP_HIT - 요청이 POP에서 클라이언트로 직접 처리된 경우 이 상태가 보고됩니다. 클라이언트에 가장 가까운 POP에 캐시되고 활성 시간이 만료된 유효한 TTL이 있는 경우 POP에서 즉시 자산이 제공됩니다. TTL은 다음 응답 헤더에 의해 결정됩니다.
  
  * Cache-Control: s-maxage
  * Cache-Control: max-age
  * 만료
* TCP_MISS - 이 상태는 클라이언트에 가장 가까운 POP에서 요청된 자산의 캐시된 버전을 찾을 수 없음을 나타냅니다. 원본 서버 또는 원본 보호 서버의 자산이 요청됩니다. 원본 서버 또는 원본 보호 서버가 자산을 반환하면 클라이언트에 제공되고 클라이언트와 에지 서버 둘 다에 캐시됩니다. 그렇지 않으면 200 이외의 상태 코드(예: 403 사용할 수 없음, 404 찾을 수 없음 등)가 반환됩니다.
* TCP_EXPIRED _HIT - 자산의 max-age가 만료된 경우 등 TTL이 만료된 자산을 대상으로 하는 요청이 POP에서 클라이언트로 직접 처리된 경우 이 상태가 보고됩니다.
  
    요청이 만료된 경우 일반적으로 원본 서버에 대한 유효성 재검사 요청이 발생합니다. TCP_EXPIRED _HIT가 발생하려면 원본 서버에서 자산의 최신 버전이 없음을 표시해야 합니다. 이러한 상황에서는 일반적으로 해당 자산의 Cache-Control 및 Expires 헤더가 업데이트됩니다.
* TCP_EXPIRED _MISS - 만료된 캐시된 자산의 최신 버전이 POP에서 클라이언트에 제공된 경우 이 상태가 보고됩니다. 이러한 상황은 캐시된 자산의 TTL이 만료되었으며(예: 만료된 max-age) 원본 서버가 해당 자산의 최신 버전을 반환하는 경우에 발생합니다. 캐시된 버전 대신 이 새로운 버전의 자산이 클라이언트에 제공됩니다. 또한 에지 서버와 클라이언트에 캐시됩니다.
* CONFIG_NOCACHE - 이 상태는 에지 POP의 고객별 구성에서 자산이 캐시되지 않도록 차단했음을 나타냅니다.
* NONE - 이 상태는 캐시 콘텐츠 새로 고침 검사가 수행되지 않았음을 나타냅니다.
* TCP_ CLIENT_REFRESH _MISS - HTTP 클라이언트(예: 브라우저)에서 에지 POP가 원본 서버에서 부실 자산의 새 버전을 검색하도록 강제하는 경우 이 상태가 보고됩니다.
  
    기본적으로 서버는 HTTP 클라이언트에서 에지 서버가 원본 서버에서 자산의 새 버전을 검색하도록 강제할 수 없게 합니다.
* TCP_ PARTIAL_HIT - 바이트 범위 요청에 의해 부분적으로 캐시된 자산이 적중되는 경우 이 상태가 보고됩니다. 요청된 바이트 범위는 POP에서 클라이언트에 즉시 제공됩니다.
* UNCACHEABLE - 자산의 Cache-Control 및 Expires 헤더에서 POP 또는 HTTP 클라이언트에 캐시되지 않도록 표시하는 경우 이 상태가 보고됩니다. 이러한 유형의 요청은 원본 서버에서 처리됩니다.

## <a name="cache-hit-ratio"></a>캐시 적중률
이 보고서는 캐시에서 직접 처리된 캐시된 요청 비율을 나타냅니다.

보고서는 다음과 같은 세부 정보를 제공합니다.

* 요청한 콘텐츠가 요청자에게 가장 가까운 POP에 캐시되었습니다.
* 네트워크 에지에서 직접 요청이 처리되었습니다.
* 요청에 원본 서버를 사용한 유효성 재검사가 필요하지 않았습니다.

보고서에 포함되지 않는 정보는 다음과 같습니다.

* 국가 필터링 옵션으로 인해 거부된 요청
* 헤더에 캐시하지 않도록 표시된 자산에 대한 요청 예를 들어 Cache-Control: private, Cache-Control: no-cache 또는 Pragma: no-cache 헤더는 자산이 캐시되지 않도록 합니다.
* 부분적으로 캐시된 콘텐츠에 대한 바이트 범위 요청.

수식은 (TCP_ HIT/(TCP_ HIT+TCP_MISS))*100입니다.

* 날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음 "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.
* "이동" 옆에 있는 Excel 시트 아이콘을 클릭하여 데이터를 내보내고 다운로드할 수 있습니다.

![캐시 적중률 보고서](./media/cdn-reports/cdn-cache-hit-ratio.png)

## <a name="ipv4ipv6-data-transferred"></a>전송되는 IPv4/IPv6 데이터
이 보고서는 IPv4 및 IPv6의 트래픽 사용량 분포를 보여 줍니다.

![전송되는 IPv4/IPv6 데이터](./media/cdn-reports/cdn-ipv4-ipv6.png)

* 날짜 범위를 선택하여 오늘/이번 주/이번 달 등의 데이터를 보거나 사용자 지정 날짜를 입력한 다음
* "이동"을 클릭하여 선택 항목이 업데이트되었는지 확인합니다.

## <a name="considerations"></a>고려 사항
보고서는 최근 18개월 내에서만 생성할 수 있습니다.

