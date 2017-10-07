---
title: "논리 앱 커넥터의 aaaOverview | Microsoft Docs"
description: "논리 앱에서 사용할 수 있는 커넥터의 개요"
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: dc4cac4c0dfaa2f9fd218ffc04414fa8e52a91d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-in-a-logic-app"></a>논리 앱에서 커넥터 사용
커넥터는 서비스, 프로토콜 및 플랫폼 간에 빠르게 액세스 tooevents, 데이터 및 작업을 제공합니다.  커넥터를 지 원하는 논리 앱의 전체 목록은 hello 수 [´ ֿ ´](apis-list.md)합니다.  커넥터는 트리거 또는 논리 앱에서 작업으로 사용할 수 있습니다 및 구성 해야 할 수 있습니다 *연결* toouse (예: tooaccess 계정 또는 사용자 대신 post는 Twitter 권한 부여) 합니다.

## <a name="basics"></a>기본 사항
Dynamics, Azure, Salesforce와 같은 다른 서비스와 논리 앱 toointegrate의 일환으로 액세스할 수는 호스팅된 서비스에 따르면 커넥터는 [많은](apis-list.md)합니다.  이러한 커넥터는 Microsoft에서 배포 및 관리하므로, 규모, 처리량 및 보안이 관리되는 통합 워크플로를 작성할 수 있습니다.  검색 및 커넥터 작업을 선택 하 여 커넥터 tooa 논리 앱을 추가 하거나 아래에서 트리거할 수 있습니다 **표시 Microsoft 관리 되는 Api**합니다.

![트리거를 선택하기 위한 작업 메뉴][1]

각 커넥터 동작이 나 트리거 속성 tooconfigure 집합이 있어야 합니다.  작업에 대 한 hello 정보 단추 toolearn에서을 클릭 하거나 해당 설명서를 참조할 수 있습니다 [자세한 toolearn](apis-list.md)합니다.

서비스 또는 하지 않은 API 아직 커넥터와 toointegrate 원하는 논리 앱을 통해 확장할 수도 있습니다는 [사용자 지정 커넥터](../logic-apps/logic-apps-create-api-app.md) 또는 HTTP와 같은 프로토콜을 통해 toohello 서비스 직접 호출 합니다.

## <a name="triggers"></a>트리거
일부 연결선은 트리거, 즉 해당 커넥터에서 이벤트는 논리 앱을 실행 하 고 hello 트리거의 일부로 모든 데이터를 전달 합니다.  트리거는 항상 hello 논리 앱의 첫 번째 단계입니다.  인기 있는 트리거에는 다음과 같은 작업이 포함됩니다.

* 되풀이 - 1시간마다 실행
* HTTP 요청을 받은 경우
* Tooa 큐는 항목을 추가 하는 경우
* 전자 메일이 수신될 때

일부 트리거는 이벤트 알림 toohello 논리 앱을 통해 수행 되며 얼마나 자주 hello 논리 앱 확인 합니다 (위쪽 tooevery 15 초) 이벤트에 대 한 hello 서비스에 구성 된 되풀이 간격 할 다른 인스턴트 hello를 실행 됩니다.  

이벤트가 수신 되 면 hello 논리 앱을 실행 하면 발생 하 고 hello 워크플로에서 hello 작업 시작 됩니다.  Hello에서 모든 데이터가 hello 워크플로 전체에서 트리거할 수 tooaccess 수도 있습니다 ('에서 새 윗' 예제 hello에 대 한 트리거는 hello 트 윗에 전달할 hello 실행).

## <a name="actions"></a>작업
대부분의 커넥터에는 hello 워크플로의 일부로 실행 될 수 있는 하나 이상의 작업이 있습니다.  작업은 hello 실행 한 후 발생 하는 단계는 트리거에서 발생 합니다.  동작 tooadd 클릭 hello **새 단계** 단추와 검색에 대 한 hello toouse 원하는 연결선입니다.  선택 하면 (및 모든를 구성한 후 [연결](#connections) 필요할 수 있습니다) 구성할 수 있습니다 hello 동작 카드 표시 됩니다.  출력에 대 한 hello 토큰 중 하나를 클릭 하 여 이전 단계에서 데이터를 선택 하거나 필요에 따라 다른 구성에 입력할 수 있습니다.

![커넥터 작업 구성][2]

## <a name="connections"></a>연결
대부분의 커넥터 필요 tooconfigure는 *연결* hello 커넥터를 사용할 수 있습니다.  A *연결* 모든 로그인 또는 연결 구성이 tooaccess hello 커넥터 필요 합니다.  OAuth를 사용 하 여, 연결 하는 커넥터에 대 한 (예: Office 365, Salesforce, 또는 GitHub) 액세스 토큰 암호화 끌어다 비밀 Azure 저장소에 안전 하 게 저장할 수 있는 hello 서비스에 로그인을 의미 합니다.  다른 커넥터(예: FTP 및 SQL)에는 서버 주소, 사용자 이름 및 암호와 같은 구성을 포함하는 연결이 필요합니다.  이러한 연결 구성 세부 정보 또한 암호화된 후 안전하게 저장됩니다.  연결이 허용 됩니다 수 tooaccess hello 서비스에 대 한 상태로 hello 서비스를 허용 합니다.  Azure Active Directory OAuth 연결 (예: Office 365, Dynamics)에 대 한 toorefresh hello 액세스 토큰을 무기한 계속 수 하겠습니다.  다른 서비스는 토큰을 새로 고치지 않고 사용할 수 있는 기간이 한정되어 있을 수 있습니다.  일반적으로 암호 변경과 같은 특정 작업을 수행하면 모든 액세스 토큰이 무효화됩니다.  

Azure에서 **찾아보기**를 클릭하고 **API 연결**을 선택하여 연결을 보고 관리할 수 있습니다.  Hello API 연결 리소스에서에서 있습니다 수 보기, 편집, 업데이트 또는 다시 만든 모든 연결을 인증 합니다.

## <a name="next-steps"></a>다음 단계
* [첫 번째 논리 앱 만들기](../logic-apps/logic-apps-create-a-logic-app.md)
* [논리 앱의 일반 용도 및 예제에 대해 자세히 알아보기](../logic-apps/logic-apps-examples-and-scenarios.md)
* [엔터프라이즈 통합 트리거 및 작업 시작](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
