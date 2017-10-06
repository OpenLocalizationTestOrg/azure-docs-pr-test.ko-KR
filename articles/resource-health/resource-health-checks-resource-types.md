---
title: "Azure 리소스 상태를 통해 리소스 종류 aaaSupported | Microsoft Docs"
description: "Azure Resource Health를 통해 지원되는 리소스 유형"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 03/19/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: a37d5c33f6ef6fdfbce0daf392bc7fa57853c7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-types-and-health-checks-in-azure-resource-health"></a>Azure Resource Health에서 리소스 유형 및 상태 검사
리소스 종류에서 리소스 상태를 통해 실행 되는 모든 hello 검사의 전체 목록은 다음과 같습니다.

## <a name="microsoftcacheredisredis"></a>Microsoft.CacheRedis/Redis
|실행된 검사|
|---|
|<ul><li>모든 hello 캐시 노드가 고 실행?</li><li>Hello 캐시 hello 데이터 센터 내에서 연결할 수 있습니까?</li><li>캐시 hello 최대 연결 수에 도달 하는 hello 했습니까?</li><li> Hello 캐시의 사용 가능한 메모리를 소진 했습니다. </li><li>많은 수의 페이지 폴트 발생 캐시 hello?</li><li>부하가 캐시 hello?</li></ul>|

## <a name="microsoftcdnprofile"></a>Microsoft.CDN/profile
|실행된 검사|
|---|
|<ul> <li>Hello 끝점이 중지 되었습니다, 제거 또는 잘못 구성 된?</li><li>Hello 보조 포털 CDN 구성 작업에 액세스할 수 있는?</li><li>사항이 hello로 지속적인 배달 문제 CDN 끝점 있습니까?</li><li>사용자가 CDN 리소스의 hello 구성을 변경할 수 있습니까?</li><li>예상 hello 속도로 구성 변경 내용을 전파 하 시겠습니까?</li><li>사용자가 hello Azure 포털, PowerShell 또는 hello API 사용 하 여 hello CDN 구성을 관리할 수 있습니까?</li> </ul>|

## <a name="microsoftclassiccomputevirtualmachines"></a>Microsoft.classiccompute/virtualmachines
|실행된 검사|
|---|
|<ul><li>호스트 서버 hello 작동 중 이며 실행?</li><li>완료 hello 호스트 운영 체제 부팅는?</li><li>Hello 가상 컴퓨터 컨테이너 프로 비전 및 전원을?</li><li>이 hello 호스트와 hello 저장소 계정 간에 네트워크 연결이 있습니까?</li><li>완료 hello hello 게스트 OS의 부팅는?</li><li>진행 중인 계획된 유지 관리가 있는가?</li></ul>|

## <a name="microsoftcognitiveservicesaccounts"></a>Microsoft.cognitiveservices/accounts
|실행된 검사|
|---|
|<ul><li>Hello 계정 hello 데이터 센터 내에서 연결할 수 있습니까?</li><li>사용 가능한 Cognitive 서비스 리소스 공급자 hello?</li><li>hello 적절 한 지역에서 사용할 수 있는 Cognitive 서비스 hello?</li><li>읽을 수 hello 리소스 메타 데이터를 보유 하는 hello 저장소 계정에서 작업을 수행할 수 있습니까?</li><li>Hello API 호출 할당량에 도달 했습니다.</li><li>Hello API 호출 읽기 제한에 도달 했습니다.</li></ul>|

## <a name="microsoftcomputevirtualmachines"></a>Microsoft.compute/virtualmachines
|실행된 검사|
|---|
|<ul><li>Hello 서버를이 가상 컴퓨터를 호스트 및 실행?</li><li>완료 hello 호스트 운영 체제 부팅는?</li><li>Hello 가상 컴퓨터 컨테이너 프로 비전 및 전원을?</li><li>이 hello 호스트와 hello 저장소 계정 간에 네트워크 연결이 있습니까?</li><li>완료 hello hello 게스트 OS의 부팅는?</li><li>진행 중인 계획된 유지 관리가 있는가?</li></ul>|

## <a name="microsoftdatalakeanalyticsaccounts"></a>Microsoft.datalakeanalytics/accounts
|실행된 검사|
|---|
|<ul><li>전송 작업에서 tooData Lake 분석 하는 사용자 수 영역을 hello?</li><li>기본 작업에 성공적으로 완료 및 실행 hello 지역 합니까?</li><li>사용자가 hello 지역에서 카탈로그 항목을 나열할 수 있습니까?</li>|


## <a name="microsoftdatalakestoreaccounts"></a>Microsoft.datalakestore/accounts
|실행된 검사|
|---|
|<ul><li>사용자가 hello 지역에서 데이터 tooData 레이크 저장소에 업로드할 수 있습니까?</li><li>사용자가 hello 지역에 데이터 레이크 저장소에서 데이터를 다운로드할 수 있습니까?</li></ul>|

## <a name="microsoftdocumentdbdatabaseaccounts"></a>Microsoft.documentdb/databaseAccounts
|실행된 검사|
|---|
|<ul><li>Tooa DocumentDB 서비스 사용 불가 인해 제공 되지 않는 데이터베이스 또는 컬렉션 요청 있었는지가?</li><li>Tooa DocumentDB 서비스 사용 불가 인해 제공 되지 않는 모든 문서 요청 있었는지가?</li></ul>|

## <a name="microsoftnetworkconnections"></a>Microsoft.network/connections
|실행된 검사|
|---|
|<ul><li>Hello VPN 터널 연결 되어 있습니까?</li><li>Hello 연결에서 구성 충돌 사항이 있습니까?</li><li>Hello 사전 공유 키 제대로 구성 되어 있습니까?</li><li>Hello VPN 온-프레미스 장치를 연결할 수 있는?</li><li>Hello IPSec/IKE 보안 정책에 불일치 사항이 있습니까?</li><li>제대로 프로 비전 되거나 실패 한 상태로 hello S2S VPN 연결을 이란?</li><li>제대로 프로 비전 되거나 실패 한 상태로 hello VNET 대 VNET 연결 이란?</li></ul>|

## <a name="microsoftnetworkvirtualnetworkgateways"></a>Microsoft.network/virtualNetworkGateways
|실행된 검사|
|---|
|<ul><li>hello VPN 게이트웨이에서 연결할 수 있는 인터넷 hello?</li><li>이 대기 모드에서 VPN 게이트웨이 hello?</li><li>Hello VPN 서비스가 hello 게이트웨이에서 실행 중 입니까?</li></ul>|

## <a name="microsoftnotificationhubsnamespace"></a>Microsoft.NotificationHubs/namespace
|실행된 검사|
|---|
|<ul><li> 등록, 설치 또는 송신과 같은 런타임 작업 hello 네임 스페이스에서 수행할 수 있습니다.</li></ul>|

## <a name="microsoftpowerbiworkspacecollections"></a>Microsoft.PowerBI/workspaceCollections
|실행된 검사|
|---|
|<ul><li>hello 호스트 운영 체제를 실행 한?</li><li>Hello workspaceCollection hello 데이터 센터 외부에서 연결할 수 있는?</li><li>hello PowerBI 리소스 공급자를 사용할 수 있습니까?</li><li>hello 적절 한 지역에서 사용할 수 있는 PowerBI 서비스 hello?</li></ul>|

## <a name="microsoftsearchsearchservices"></a>Microsoft.search/searchServices
|실행된 검사|
|---|
|<ul><li>Hello 클러스터에서 진단 작업을 수행할 수 있습니까?</li></ul>|

## <a name="microsoftsqlserverdatabase"></a>Microsoft.SQL/Server/database
|실행된 검사|
|---|
|<ul><li> 로그인 toohello 데이터베이스 있었는지가?</li></ul>|

## <a name="microsoftstreamanalyticsstreamingjobs"></a>Microsoft.StreamAnalytics/streamingjobs
|실행된 검사|
|---|
|<ul><li>Hello 작업은를 실행 하 고 실행 중인 모든 hello 호스트?</li><li>Hello 작업이 없습니다 toostart 되었습니까?</li><li>진행 중인 런타임 업데이트가 있는가?</li><li>(예: 실행 중 또는 고객에 의해 중지) 예상 되는 상태에서 hello 작업은?</li><li>Hello 작업이 발생 했습니다 아웃 메모리 예외의?</li><li>진행 중인 예약된 계산 업데이트가 있는가?</li><li>사용할 수 있는 실행 관리자 (제어 계획) hello?</li></ul>|

## <a name="microsoftwebserverfarms"></a>Microsoft.web/serverFarms
|실행된 검사|
|---|
|<ul><li>호스트 서버 hello 작동 중 이며 실행?</li><li>인터넷 정보 서비스를 실행 중인가?</li><li>부하 분산 장치 hello 실행 중 입니까?</li><li>웹 서비스를 계획 하는 hello hello 데이터 센터 내에서 연결할 수 있습니까?</li><li>서버 팜 hello에 대 한 hello 저장소 계정 호스팅 hello 사이트 콘텐츠를 사용할 수??</li></ul>|

## <a name="microsoftwebsites"></a>Microsoft.web/sites
|실행된 검사|
|---|
|<ul><li>호스트 서버 hello 작동 중 이며 실행?</li><li>인터넷 정보 서버를 실행 중인가?</li><li>부하 분산 장치 hello 실행 중 입니까?</li><li>Hello 웹 응용 프로그램 hello 데이터 센터 내에서 연결할 수 있습니까?</li><li>Hello 저장소 계정 hello 사용 가능한 사이트 콘텐츠를 호스팅하는?</li></ul>|

이러한 리소스 toolearn 리소스 상태에 대 한 자세한 참조:
-  [소개 tooAzure 리소스 상태](Resource-health-overview.md)
-  [Azure Resource Health에 대한 질문과 대답](Resource-health-faq.md)

