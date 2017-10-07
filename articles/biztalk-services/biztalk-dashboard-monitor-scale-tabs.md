---
title: "aaaDashboard, 모니터, 배율, 구성, 및에서 BizTalk 서비스 하이브리드 연결 | Microsoft Docs"
description: "Hello 컨트롤에 대해 알아보고 hello 클래식 포털 탭에서 BizTalk 서비스에 대 한 성능을 모니터링할: 대시보드, 모니터, 크기 조정, 구성 및 하이브리드 연결 합니다. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Hello 대시보드, 모니터, 크기 조정, 구성 및 하이브리드 연결 탭 검토

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

BizTalk 서비스를 만들고 응용 프로그램을 배포 후 hello BizTalk 서비스 설정 중 일부를 변경할 수 있으며 hello 응용 프로그램 성능을 모니터링 합니다. 

Hello Azure 클래식 포털을 열 때 자동으로 hello에 배치 됩니다 **모든 항목이** 탭 tooview hello에서 BizTalk 서비스를 선택 하는 BizTalk 서비스를 **모든 항목** 탭 이나 선택 hello **BIZTALK 서비스** ; 탭 한 다음 BizTalk 서비스 이름을 선택 합니다.

다음 탭 hello로 새 창이 열립니다. 이 항목에서는 이러한 탭에 대해 설명합니다.

## <a name="quickstart-quickstartquickstart"></a>빠른 시작(![빠른 시작][Quickstart])
Hello BizTalk 서비스 버전에 따라 나열 된 모든 옵션을 사용 하지 못할 수 있습니다. 

<table border="1">
    <tr>
        <td><strong>Hello 도구 가져오기</strong></td>
        <td>Hello BizTalk 서비스 SDK tooinstall hello Visual Studio 프로젝트 템플릿 온-프레미스 개발 컴퓨터에 다운로드 합니다. 이러한 서식 파일 만들기 hello <strong>BizTalk 서비스</strong> (브리지) 및 hello <strong>BizTalk 서비스 아티팩트</strong> 배포 tooyour BizTalk 서비스 (변환) Visual Studio 프로젝트입니다.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Azure BizTalk Services SDK 어떻게 hello 사용 하 여 시작 합니까 </a> 및 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Azure BizTalk Services SDK 설치 hello</a> 목록 hello 단계 tooget 시작 합니다.
        </td>
    </tr>
    <tr>
        <td><strong>파트너 규약 만들기</strong></td>
        <td>열립니다는 파트너를 추가 하 고 X12, AS2, 만들 Azure에서 호스팅되는 Azure BizTalk 서비스 포털 hello 및 EDIFACT EDI 규약입니다.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services 포털에서 EDI 메시징에 대 한 구성 요소 구성</a> 목록 hello 단계 tooget 시작 합니다.
        </td>
    </tr>

<tr>
        <td><strong>BizTalk Services에 대한 자세한 정보</strong></td>
        <td>Toohello 이동 <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">학습 센터</a> toolearn Azure BizTalk 서비스에 대 한 자세한 합니다.</td>
</tr>
</table>


Hello 맨 아래에 hello 작업 표시줄에서 다음을 수행할 수 있습니다.

<table border="1">

<tr>
<td>응용 프로그램 배포 <strong>관리</strong></td>
<td>Hello Azure BizTalk 서비스 포털도를 열립니다. BizTalk 서비스 포털 hello는 파트너를 추가 하 고 X12, AS2, 만드는 포함 하 여 hello 입구 tooEDI 구성 및 EDIFACT 계약입니다.
<br/><br/>
와 동일 hello은이 <strong>파트너 규약을 만들</strong> hello에 <strong>빠른 시작</strong> 탭 합니다.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services 포털에서 EDI 메시징에 대 한 구성 요소 구성</a> hello BizTalk 서비스 포털에 더 많은 정보를 제공 합니다.</td>
</tr>

<tr>
<td><strong>연결 정보</strong> 의 액세스 제어 Namespace hello</td>
<td>연결 정보를 선택 하면 다음 액세스 제어 Namespace, 기본 발급자 hello 하 고 기본 키 표시 됩니다. 이러한 값은 복사할 수 있습니다.
<br/><br/>
Hello 액세스 제어 포털을 열 수도 있습니다. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">액세스 제어 Namespace를 만들</a> hello 액세스 제어 포털에 더 많은 정보를 제공 합니다.</td>
</tr>

<tr>
<td><strong>키를 동기화</strong> hello 저장소 계정에</td>
<td>저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다. 이러한 암호화 키 저장소 계정 액세스 tooyour를 제어합니다. BizTalk 서비스는 hello 기본 키를 자동으로 사용 합니다. <strong>키를 동기화</strong> hello BizTalk 서비스를 중단시 키 지 않고 사용자가 tooswitch hello 기본 키 및 보조 키 hello 사이 사용 하도록 설정 합니다.
<br/><br/>
예를 들어 hello BizTalk 서비스 toouse hello 저장소 계정에 대 한 새 기본 키를 원하는합니다. toodo이:
<br/><br/>
<ol>
<li>BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다. Hello 보조 키를 선택 합니다. 이렇게 하면 BizTalk 서비스 hello hello 보조 키를 사용 하 여 시작 합니다.</li>
<li>Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 기본 키를 다시 생성 합니다. BizTalk 서비스는 hello 보조 키를 사용 하 여 기억 하십시오.</li>
<li>BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다. 이제 hello 기본 키를 선택 합니다. 이 hello 새로운 재생성 하는 기본 키입니다.</li>
<li>Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 보조 키 다시 생성 합니다.</li>
</ol>
<br/>
이 프로세스를 "키 롤오버"라고 합니다. hello 목적은 hello BizTalk 서비스를 중단시 키 지 않고 tooenable 사용자 tooswitch hello 기본 키 및 보조 키 hello 사이입니다.</td>
</tr>

<tr>
<td>응용 프로그램 <strong>삭제</strong></td>
<td>선택 하면 BizTalk 서비스를 삭제 하 고 모든 배포 항목 tooit 제거 됩니다.</td>
</tr>
</table>


## <a name="dashboard"></a>대시보드
Hello BizTalk 서비스 버전에 따라 나열 된 모든 옵션을 사용 하지 못할 수 있습니다. 

BizTalk 서비스 이름을 선택 하면 hello 대시보드 탭이 표시 됩니다. 대시보드에서 다음을 수행할 수 있습니다.

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>사용 개요: hello 사용 되는 하이브리드 연결 수를 보여 줍니다.
또한 gb에서 hello 데이터 사용을 표시합니다. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>메트릭 그래프: 성능 메트릭의 고정 목록을 표시합니다.
이러한 메트릭은 hello BizTalk 서비스의 hello 상태에 대 한 실시간 값을 제공 합니다. Hello를 선택할 수도 있습니다 **상대** 또는 **절대** 시간 범위 값과 hello **간격** hello 그래프에 표시 되는 hello 메트릭. 

이러한 성능 메트릭에 대 한 이동 너무[사용 가능한 메트릭](#Metrics) 이 항목의 합니다.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>간략 상태: BizTalk 서비스 속성을 나열합니다.
<table border="1">

<tr>
<td><strong>추적 데이터베이스 자격 증명 업데이트</strong></td>
<td>변경 내용을 hello 사용자 이름 및 암호 toolog hello 추적 데이터베이스에 사용 되는 합니다.</td>
</tr>
<tr>
<td><strong>SSL 인증서 업데이트</strong></td>
<td>Hello BizTalk 서비스 toouse 서로 다른 SSL 인증서를 업데이트할 수 있습니다. 자체 서명 된 SSL 인증서를 자동으로 생성 됩니다 있습니다 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">hello BizTalk 서비스 만들기</a>합니다.</td>
</tr>
<tr>
<td><strong>인증서 다운로드</strong></td>
<td>BizTalk 서비스 tooa 로컬 컴퓨터에서 사용 하는 hello SSL 인증서를 다운로드할 수 있습니다.</td>
</tr>
<tr>
<td><strong>상태</strong></td>
<td>Hello BizTalk 서비스의 현재 상태를 표시합니다. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: 서비스 상태 차트</a>를 참조합니다. </td>
</tr>
<tr>
<td><strong>서비스 URL</strong></td>
<td>BizTalk 서비스에 대 한 hello URL입니다. Hello로 동일 hello은이 <strong>도메인 URL</strong> BizTalk 서비스를 만들 때 입력 합니다.</td>
</tr>
<tr>
<td><strong>공용 VIP(가상 IP) 주소</strong></td>
<td>hello IP 주소가 tooyour BizTalk 서비스를 지정 합니다. 모든 입력된 끝점에 사용 되 고 아웃 바운드 트래픽에 대 한 hello 원본 주소입니다. 이 IP 주소 생성 될 때 BizTalk 서비스 tooyour를 속해 있습니다. Hello BizTalk 서비스를 삭제 하면 BizTalk 서비스 tooanother hello IP 주소에 할당 됩니다.</td>
</tr>
<tr>
<td><strong>ACS 네임스페이스</strong></td>
<td>BizTalk 서비스 hello로 인증합니다.</td>
</tr>
<tr>
<td><strong>에디션</strong></td>
<td>Hello Edition hello BizTalk 서비스를 만들 때 입력 나열 합니다.</td>
</tr>
<tr>
<td><strong>위치</strong></td>
<td>표시 hello BizTalk 서비스를 호스팅하는 지역.</td>
</tr>
<tr>
<td><strong>생성일</strong></td>
<td>Hello 날짜 및 시간 hello는 표시 합니다. BizTalk 서비스를 만들었습니다.</td>
</tr>
<tr>
<td><strong>추적 데이터베이스</strong></td>
<td>BizTalk 서비스에 사용 되는 테이블을 추적 하는 hello를 저장 하는 hello Azure SQL 데이터베이스 이름입니다. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">요구 사항 Explained</a> hello 추적 데이터베이스에 자세히 설명 합니다.</td>
</tr>
<tr>
<td><strong>모니터링/보관 저장소</strong></td>
<td>BizTalk 서비스의 출력을 모니터링 하는 hello를 저장 하는 hello Azure 저장소 계정 이름입니다.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">요구 사항 Explained</a> hello 저장소 계정에 자세히 설명 합니다.</td>
</tr>
<tr>
<td><strong>구독 이름</strong></td>
<td>BizTalk 서비스를 호스트 하는 hello 구독을 나열 합니다. hello 구독 액세스 toohello Azure 클래식 포털을 통해 제어합니다.</td>
</tr>
<tr>
<td><strong>구독 ID</strong></td>
<td>구독을 만들 때 구독 ID가 자동으로 생성됩니다. REST Api를 사용 하는 경우 구독 id. tooenter hello 할 수 있습니다.</td>
</tr>
</table>

[BizTalk 서비스:를 사용 하 여 Azure 클래식 포털을 프로 비전](http://go.microsoft.com/fwlink/p/?LinkID=302280) 목록 hello 단계 toocreate BizTalk 서비스입니다.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>연결 정보를 동기화 키를 관리 하 고 hello 작업 표시줄에서 삭제 합니다.
<table border="1">

<tr>
<td>응용 프로그램 배포 <strong>관리</strong></td>
<td>Hello Azure BizTalk 서비스 포털을 엽니다. BizTalk 서비스 포털 hello는 파트너를 추가 하 고 X12, AS2, 만드는 포함 하 여 hello 입구 tooEDI 구성 및 EDIFACT 계약입니다.
<br/><br/>
와 동일 hello은이 <strong>파트너 규약을 만들</strong> hello에 <strong>빠른 시작</strong> 탭 합니다.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">BizTalk Services 포털에서 EDI 메시징에 대 한 구성 요소 구성</a> hello BizTalk 서비스 포털에 더 많은 정보를 제공 합니다.</td>
</tr>
<tr>
<td><strong>연결 정보</strong> 의 액세스 제어 Namespace hello</td>
<td>표시 hello 액세스 제어 Namespace, 기본 발급자 및 기본 키 값이 있습니다. 복사할 수 있습니다.
<br/><br/>
Hello 액세스 제어 포털을 열 수도 있습니다. 이 액세스 제어 포털 hello Active Directory 옵션을 사용 하 여 hello 왼쪽된 탐색 창에서 같은 hello 됩니다.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Your ACS Namespace 관리</a> hello 액세스 제어 포털에 더 많은 정보를 제공 합니다.</td>
</tr>
<tr>
<td><strong>키를 동기화</strong> hello 저장소 계정에</td>
<td>저장소 계정을 만들면 기본 키와 보조 키가 자동으로 만들어집니다. 이러한 암호화 키 저장소 계정 액세스 tooyour를 제어합니다. BizTalk 서비스는 hello 기본 키를 자동으로 사용 합니다. <strong>키를 동기화</strong> hello BizTalk 서비스를 중단시 키 지 않고 사용자가 tooswitch hello 기본 키 및 보조 키 hello 사이 사용 하도록 설정 합니다.
<br/><br/>
예를 들어 hello BizTalk 서비스 toouse hello 저장소 계정에 대 한 새 기본 키를 원하는합니다. toodo이:
<br/><br/>
<ol>
<li>BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다. Hello 보조 키를 선택 합니다. 이렇게 하면 BizTalk 서비스 hello hello 보조 키를 사용 하 여 시작 합니다.</li>
<li>Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 기본 키를 다시 생성 합니다. BizTalk 서비스는 hello 보조 키를 사용 하 여 기억 하십시오.</li>
<li>BizTalk Service를 선택하고 <strong>동기화 키</strong>를 선택합니다. 이제 hello 기본 키를 선택 합니다. 이 hello 새로운 재생성 하는 기본 키입니다.</li>
<li>Hello Azure 클래식 포털에서에서 저장소 계정을 선택 하 고 hello 보조 키 다시 생성 합니다.</li>
</ol>
<br/>
이 프로세스를 "키 롤오버"라고 합니다. hello 목적은 hello BizTalk 서비스를 중단시 키 지 않고 tooenable 사용자 tooswitch hello 기본 키 및 보조 키 hello 사이입니다.</td>
</tr>

<tr>
<td>응용 프로그램 <strong>삭제</strong></td>
<td>BizTalk 서비스와 모든 배포 항목 tooit 제거 됩니다.</td>
</tr>
</table>


## <a name="monitor"></a>모니터
Toohello 적용 되지 않습니다 무료 버전입니다.

BizTalk 서비스 이름을 선택 하면 hello 모니터 탭 ´ ï ´ 하 고 hello 다음을 표시 합니다.

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>메트릭 그래프: 표시 hello 선택한 성능 메트릭
이러한 메트릭은 hello BizTalk 서비스의 hello 상태에 대 한 실시간 값을 제공 합니다. 표시할 성능 메트릭을 선택합니다. 최대 6개의 성능 메트릭을 동시에 표시할 수 있습니다. 

Hello를 선택할 수도 있습니다 **상대** 또는 **절대** 시간 범위 값과 hello **간격** 표시 되는 hello 메트릭. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>hello 그래프에 메트릭 tooremove 또는 표시:
1. 선택 hello **모니터** 탭 합니다.
2. 선택 **메트릭 추가** hello 작업 표시줄에서:  
   ![메트릭 추가 선택][AddMetrics]
3. 원하는 toodisplay hello 성능 메트릭을 확인 합니다.
4. Hello 확인 표시 tooreturn toohello 선택 **모니터** 탭 합니다.
5. Hello 그래프에 hello 원 다음 toohello 메트릭 toodisplay 해당 메트릭이 값을 선택 합니다.  
   
    예를 들어 hello **CPU 사용량** 메트릭을 회색; 출력 hello 그래프에 표시 되지 않습니다.  
   ![CPU 사용량 메트릭이 회색으로 표시됨][GrayedMetric]  
   
    Select hello 원 tooenable hello 회색 **CPU 사용량** 메트릭 toodisplay hello 그래프에서 해당 출력:  
   ![CPU 사용량 메트릭 사용][EnabledMetric]
6. tooremove hello 디스플레이 그래프 및 hello 목록에서 메트릭을 선택 **메트릭을 삭제** hello 작업 표시줄에서 합니다. tooadd hello 백 toohello 메트릭 목록에서 **메트릭 추가** hello 작업 표시줄에서 hello 메트릭을 그리고 선택 hello 확인 표시 tooreturn toohello 확인 **모니터** 탭 합니다. Select hello 원 tooenable hello 메트릭을 회색으로 표시 합니다.

## <a name="Metrics"></a>사용 가능한 메트릭
hello 다음 성능 카운터/메트릭을 사용할 수 있습니다.

<table border="1">

<tr>
<td><strong>왕복 대기 시간</strong></td>
<td>데 걸린 시간 (밀리초) (ms) tooprocess 모든 브리지에서 BizTalk 서비스 hello hello 메시지를 완전히 처리 될 때까지 hello 시간 hello 메시지에서 메시지를 수신 하는 hello 평균 시간을 표시 합니다. 성공적으로 처리된 메시지만 계산됩니다.<br/><br/>
이벤트를 수행 하는 hello 발생 하는 경우 타임 스탬프를 만듭니다.
<ul>
<li>메시지가 전달 hello 게이트웨이</li>
<li>메시지는 라우트된 toohello 대상</li>
<li>대상 응답을 받은 경우</li>
<li>대상 승인 보낸 응답 toohello 게이트웨이</li>
</ul>
<br/>
이 메트릭은 계산을 수행 하는 hello의 hello 결과를 보여 줍니다.
<br/><br/>
[대상 승인 보낸 응답 toohello 게이트웨이]-[메시지가 hello 게이트웨이 전달 하는 데 사용]</td>
</tr>
<tr>
<td><strong>원본에서 실패</strong></td>
<td>Hello에 실패 한 메시지의 총 수를 표시 하 여 hello hello 원본 끝점에서 메시지를 끌어오는 경우 BizTalk 서비스입니다.</td>
</tr>
<tr>
<td><strong>CPU 사용량</strong></td>
<td>모든 역할 인스턴스의 hello 평균 % 프로세서 시간을 나열합니다.</td>
</tr>
<tr>
<td><strong>처리 대기 시간</strong></td>
<td>Hello hello 시간을 제외한 모든 브리지에서 hello BizTalk 서비스에서 메시지 대상에 소요 된 시간 (밀리초) (ms) tooprocess에서 수행 되는 평균 시간을 표시 합니다. 성공적으로 처리된 메시지만 계산됩니다.<br/><br/>
각 이벤트 뒤 hello 발생 하는 경우 타임 스탬프를 만듭니다.

<ul>
<li>메시지가 전달 hello 게이트웨이</li>
<li>메시지는 라우트된 toohello 대상</li>
<li>대상 응답을 받은 경우</li>
<li>대상 승인 보낸 응답 toohello 게이트웨이</li>
</ul>
<br/>이 메트릭은 계산을 수행 하는 hello의 hello 결과를 보여 줍니다.<br/><br/>
[대상 승인 보낸 응답 toohello 게이트웨이]-[메시지가 전달 게이트웨이 hello]-[대상 응답을 받을] + [메시지 라우팅된 toohello 대상]</td>
</tr>
<tr>
<td><strong>처리 중 실패</strong></td>
<td>Hello 총 시간 간격 내에서 모든 hello 브리지에서 hello BizTalk 서비스에서 처리 하는 동안 실패 한 메시지 수를 표시 합니다.</td>
</tr>
<tr>
<td><strong>전송된 메시지</strong></td>
<td>시간 간격 내에서 모든 브리지 hello BizTalk 서비스에서 보낸 메시지의 표시 hello의 총 수입니다. 이 메트릭은 파이프라인에서 보낸 메시지 hello 경로 대상에 도달 하는 경우에 증가 됩니다. 이 메트릭이 메시지가 성공적으로 처리되었음을 나타내지는 않습니다.<br/><br/>
요청-회신 시나리오에서 hello 메트릭은 hello 경로 대상에서 수신 승인을 백 toohello 파이프라인을 보낼 때 증가 됩니다.</td>
</tr>
<tr>
<td><strong>수신된 메시지</strong></td>
<td>시간 간격 내에서 모든 브리지 hello BizTalk 서비스에서 받은 메시지의 표시 hello의 총 수입니다. 이 메트릭은 hello 파이프라인에서 새 메시지를 받으면 증가 됩니다.</td>
</tr>
<tr>
<td><strong>진행 중 메시지</strong></td>
<td>표시 hello 메시지에서 현재 처리 중인 BizTalk 서비스 hello 시간 간격 내에서 총 수입니다.</td>
</tr>
<tr>
<td><strong>처리된 메시지</strong></td>
<td>표시 hello 시간 간격 내에서 모든 브리지 hello BizTalk 서비스에서 성공적으로 처리 하는 메시지의 총 수입니다. 이 메트릭은 hello 파이프라인과 toohello 성공적으로 라우팅된 대상으로 메시지를 성공적으로 수신 되 면 증가 합니다.</td>
</tr>
</table>


## <a name="scale"></a>확장
Hello 크기 조정 탭에서 추가 하거나 BizTalk 서비스에 사용 되는 단위 수가 hello 뺄 수 있습니다. 기본적으로 한 개의 단위가 구성되어 있습니다. 추가 단위가 tooscale를 추가할 수 있습니다 BizTalk 서비스입니다. Hello 눈금을 늘리면 처리량이 증가 합니다. hello 리소스의도 늘어나면 처리 능력 및 배포 된 브리지, 계약, LOB 연결을 포함 하 여 합니다. 예를 들어 hello 범위 1 단위 too2 단위에서 증가 합니다. 이 경우 이중 hello 수가 브리지, double hello 계약, double hello LOB 연결 및 이중 hello 처리 능력을 배포할 수 있습니다.

일부 BizTalk 버전에서는 크기 조정 옵션을 제공하지 않습니다. 이 경우 1 단위가 허용됩니다. toodetermine 버전을 확장할 수 있습니다, 단위의 수 참조 너무[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md)합니다.

Hello 단위 수를 늘리면 가격 떨어질 수 있습니다. Hello 단위를 늘릴 경우을 선택 하면 **저장** 청구 영향을 받는지 여부를 알려 주는 메시지가 표시 됩니다. Toocontinue을 선택합니다. Hello 단위 수를 늘리면 활성 tooUpdating에서 hello BizTalk 서비스 상태를 변경 합니다. Hello 업데이트 상태, BizTalk 서비스 toorun를 계속합니다.

[BizTalk 서비스: 버전 차트](biztalk-editions-feature-chart.md) 에 “단위"가 정의되어 있습니다.

## <a name="configure"></a>구성
TooHybrid 연결 적용 되지 않습니다.

백업 상태 tooNone hello 또는 자동 설정합니다. TooNone, 설정 된 경우 백업이 자동으로 생성 됩니다. TooAutomatic, 설정 된 경우 hello 백업 위치, hello 백업과 기간 tookeep hello 백업 파일의 hello 빈도 구성 합니다. 

[BizTalk 서비스: 백업 및 복원](biztalk-backup-restore.md) hello 세부 정보를 제공 합니다. 

## <a name="HybridConnections"></a>하이브리드 연결
하이브리드 연결은 Azure 앱 서비스, SQL Server, MySQL, HTTP 웹 Api 가장 사용자 지정 웹 서비스와 같은 정적 TCP 포트를 사용 하 여 tooan 온-프레미스 리소스에서에서 모바일 앱 또는 웹 앱과 같은 Azure 응용 프로그램을 연결 합니다. 하이브리드 연결은 BizTalk 서비스의 hello Azure 클래식 포털에서에서 관리 됩니다.

Azure 앱 서비스에 하이브리드 연결이 toocreate 참조 [액세스 온-프레미스 하이브리드 연결을 사용 하 여 Azure 앱 서비스의 리소스](../app-service-web/web-sites-hybrid-connection-get-started.md)합니다.

toocreate Azure BizTalk 서비스에서 하이브리드 연결을 관리, 참조 또는 [하이브리드 연결](integration-hybrid-connection-overview.md)합니다.

## <a name="next"></a>다음
Hello 다른 탭에 익숙하다면 했으므로 hello Azure BizTalk 서비스 기능에 대 한 더 알아볼 수 있습니다.

* [BizTalk 서비스: 제한](biztalk-throttling-thresholds.md)  
* [BizTalk 서비스: 발급자 이름 및 발급자 키](biztalk-issuer-name-issuer-key.md)  
* [BizTalk 서비스: 백업 및 복원](biztalk-backup-restore.md)

## <a name="see-also"></a>참고 항목
* [하이브리드 연결](integration-hybrid-connection-overview.md)  
* [BizTalk 서비스: Developer, Basic, Standard 및 Premium Editions 차트](biztalk-editions-feature-chart.md)  
* [BizTalk 서비스: Azure 클래식 포털을 사용하여 프로비전](biztalk-provision-services.md)  
* [BizTalk 서비스: BizTalk 서비스 상태 차트](biztalk-service-state-chart.md)  
* [Azure BizTalk 서비스 SDK를 hello 어떻게 사용 하 여 시작 합니까](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

