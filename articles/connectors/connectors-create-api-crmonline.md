---
title: "Azure 논리 앱에서 aaaConnect tooDynamics 365 (온라인) | Microsoft Docs"
description: "논리 hello hello Dynamics 365 커넥터에서 제공 하는 API 통해 Dynamics 365 (온라인) 엔터티를 관리 하는 응용 프로그램 워크플로 만들기"
services: logic-apps
cloud: Azure Stack
author: Mattp123
manager: anneta
documentationcenter: 
tags: connectors
ms.assetid: 0dc2abef-7d2c-4a2d-87ca-fad21367d135
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: matp; LADocs
ms.openlocfilehash: 183d7a6b8e5d2c0eecc70da0da3806e06c382df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toodynamics-365-from-logic-app-workflows"></a>논리 앱 워크플로에서 tooDynamics 365 연결

논리 앱 tooDynamics 365 (온라인)에 연결 하 고 레코드를 만들거나, 항목을 업데이트 하거나 레코드의 목록을 반환 하는 경우 유용한 비즈니스 흐름을 만들 수 있습니다. Hello Dynamics 365 커넥터와 함께 다음 작업을 수행할 수 있습니다.

* Dynamics 365 (온라인)에서 가져올 hello 데이터를 기반으로 비즈니스 흐름을 작성 합니다.
* 응답 한 다음 다른 작업에 사용할 수 있는 hello 출력을 확인 하는 작업을 사용 합니다. 예를 들어 Dynamics 365(온라인)에서 항목이 업데이트되면 Office 365를 사용하여 메일을 보낼 수 있습니다.

이 항목에서는 방법을 toocreate 논리 앱을 만드는 작업 Dynamics 365 Dynamics 365 새 잠재 고객 때마다 만들어집니다.

## <a name="prerequisites"></a>필수 조건
* Azure 계정.
* Dynamics 365(온라인) 계정.

## <a name="create-a-task-when-a-new-lead-is-created-in-dynamics-365"></a>Dynamics 365에서 새 리드가 생성될 작업 만들기

1.  [TooAzure 로그인](https://portal.azure.com)합니다.

2.  Hello Azure 검색 상자에 입력 `Logic apps`, ENTER 키를 누릅니다.

      ![논리 앱 찾기](./media/connectors-create-api-crmonline/find-logic-apps.png)

3.  **논리 앱** 아래에서 **추가**를 클릭합니다.

      ![LogicApp 추가](./media/connectors-create-api-crmonline/add-logic-app.png)

4.  toocreate hello 논리 앱 전체 hello **이름**, **구독**, **리소스 그룹**, 및 **위치** 필드를 선택한 다음 클릭 **만들**합니다.

5.  Hello 새 논리 앱을 선택 합니다. Hello를 받는 경우 **배포 성공** 알림을 클릭 **새로 고침**합니다.

6.  **배포 도구** 아래에서 **논리 앱 디자이너**를 클릭합니다. Hello 템플릿 목록에서 클릭 **빈 논리 앱**합니다.

7.  Hello 검색 상자에 입력 `Dynamics 365`합니다. Hello Dynamics 365 트리거합니다 목록, 선택 **Dynamics 365-레코드를 만들 때**합니다.

8.  TooDynamics 365에서에서 증명된 toosign 인 경우 않으면 지금 연결 합니다.

9.  다음 정보는 hello hello 트리거 세부 정보를 입력 합니다.

  * **조직 이름**. Hello 논리 앱 toolisten를 원하는 hello Dynamics 365 인스턴스를 선택 합니다.

  * **엔터티 이름**. Toolisten를 원하는 hello 엔터티를 선택 합니다. 이 이벤트는 트리거 toostart hello 논리 앱 역할을 합니다. 
  이 연습에서는 **리드**를 선택합니다.

  * **얼마나 자주 시겠습니까 toocheck 항목에 대 한?** 이러한 값은 얼마나 자주 설정 hello 논리 앱 업데이트 관련된 toohello 트리거를 확인 합니다. hello 기본 설정은 3 분 마다 업데이트에 대 한 toocheck입니다.

    * **빈도**. 초, 분, 시간 또는 일을 선택합니다.

    * **간격**. Hello 초, 분, 시간 또는 toopass hello 다음 검사 하기 전에 원하는 날짜 수를 입력 합니다.

      ![논리 앱 트리거 세부 정보](./media/connectors-create-api-crmonline/trigger-details.png)

10. **새 단계**를 클릭한 다음 **작업 추가**를 클릭합니다.

11. Hello 검색 상자에 입력 `Dynamics 365`합니다. Hello 작업 목록에서 선택 **Dynamics 365 – 새 레코드를 만들어**합니다.

12. Hello 다음 정보를 입력 합니다.

    * **조직 이름**. Hello 흐름 toocreate hello 레코드 저장할 hello Dynamics 365 인스턴스를 선택 합니다. 
    이 인스턴스가 동일한 hello toobe에 되어 있지 않습니다 공지에서 hello 이벤트가 트리거되면 여기서 인스턴스.

    * **엔터티 이름**. Hello 이벤트가 트리거될 때 않겠다고 toocreate 레코드 hello 엔터티를 선택 합니다. 
    이 연습에서는 **작업**을 선택합니다.

13. Hello에 클릭 **주체** 나타나는 상자. Hello 동적 콘텐츠 나타나는 목록에서 이러한 필드 중 하나를 선택할 수 있습니다.

    * **성**. Hello 작업 레코드를 만들 때 hello 잠재 고객에 대 한 hello 성을 hello 작업에 대 한 hello 제목 필드에 삽입이 필드를 선택 합니다.
    * **토픽**. Hello 작업에 대 한 hello 제목 필드에 hello 리드에이 필드 삽입 hello 항목 필드를 선택 때 hello 작업 레코드가 만들어집니다. 
    클릭 **항목** tooadd 해당 toohello **주체** 상자입니다.

      ![논리 앱 새 레코드 만들기 세부 정보](./media/connectors-create-api-crmonline/create-record-details.png)

14. Hello 논리가 응용 프로그램 디자이너 도구 모음에서 **저장**합니다.

    ![논리 앱 디자이너 도구 모음 저장](./media/connectors-create-api-crmonline/designer-toolbar-save.png)

15. 논리 앱 toostart hello 클릭 **실행**합니다.

    ![논리 앱 디자이너 도구 모음 저장](./media/connectors-create-api-crmonline/designer-toolbar-run.png)

16. 이제 Dynamics 365 for Sales에서 리드 레코드를 만들고 흐름이 어떻게 진행되는지 확인하세요!

## <a name="set-advanced-options-for-a-logic-app-step"></a>논리 앱 단계에 대한 고급 옵션 설정

논리 앱 단계에서 toofilter 데이터 클릭 방법을 toospecify **고급 옵션 표시** 해당 단계에서 다음 필터 또는 추가 순서 쿼리에서 합니다.

예를 들어 필터의 쿼리 tooget 유일한 활성 계정을 사용할 수 있으며 hello 계정 이름을 기준으로 정렬. tooperform이 작업을 hello OData 필터 쿼리 입력 `statuscode eq 1`를 선택 하 고 **계정 이름** hello 동적 콘텐츠 목록에서 합니다. 자세한 정보: [MSDN: $filter](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_1) 및 [$orderby](https://msdn.microsoft.com/library/gg309461.aspx#Anchor_2)

![논리 앱 고급 옵션](./media/connectors-create-api-crmonline/advanced-options.png)

### <a name="best-practices-when-using-advanced-options"></a>고급 옵션을 사용하는 경우 모범 사례

값 tooa 필드를 추가한 경우 값을 입력 하거나 hello 동적 콘텐츠 목록에서 값을 선택 하는지 여부를 hello 필드 형식이 같아야 합니다.

필드 형식  |어떻게 toouse  |여기서 toofind  |이름  |데이터 형식  
---------|---------|---------|---------|---------
텍스트 필드|텍스트 필드에는 한 줄의 텍스트 또는 텍스트 형식 필드인 동적 콘텐츠가 필요합니다. Hello 범주 및 하위 범주 필드를 포함 하는 예입니다.|설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 작업 > 필드 |카테고리 |한 줄의 텍스트        
정수 필드 | 일부 필드에는 정수 또는 정수 형식 필드인 동적 콘텐츠가 필요합니다. 이러한 예로 완료율, 기간이 있습니다. |설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 작업 > 필드 |percentcomplete |정수         
날짜 필드 | 일부 필드에 mm/dd/yyyy 형식 또는 날짜 형식 필드인 동적 콘텐츠가 필요합니다. 이러한 예로 만든 날짜, 시작 날짜, 실제 시작, 마지막 보류 시간, 실제 종료, 기한 날짜가 있습니다. | 설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 작업 > 필드 |createdon |날짜 및 시간
레코드 ID와 조회 유형이 모두 필요한 필드입니다. |다른 엔터티 레코드를 참조 하는 일부 필드는 hello 레코드 ID와 hello 조회 유형을 모두 필요 합니다. |설정 > 사용자 지정 > 사용자 지정 hello 시스템 > 엔터티 > 계정 > 필드  | accountid  | 기본 키

### <a name="more-examples-of-fields-that-require-both-a-record-id-and-lookup-type"></a>레코드 ID와 조회 유형이 모두 필요한 필드의 추가 예
Hello 이전 테이블에 확장을 추가 예제 hello 동적 콘텐츠 목록에서 선택 된 값을 사용 하지 않는 필드는 다음과 같습니다. 대신, 이러한 필드 두 레코드 ID와 조회 종류 중 하나로 PowerApps의 hello 필드에 입력 해야 합니다.  
* 소유자 및 소유자 유형. hello 소유자 필드는 유효한 사용자 또는 팀 레코드 ID 여야 합니다. hello 소유자 유형 중 하나 여야 합니다 **systemusers** 또는 **팀**합니다.
* 고객 및 고객 유형. hello 고객 필드 유효한 계정 이거나 문의 레코드 id입니다. hello 소유자 유형 중 하나 여야 합니다 **계정** 또는 **연락처**합니다.
* 관련 항목 및 관련 유형. 필드에 대 한 hello 계정 등, 올바른 레코드 ID 이거나 문의 레코드 id입니다. hello에 대 한 형식은 형식 이어야 합니다 hello 조회 hello 레코드에 대 한 같은 **계정** 또는 **연락처**합니다.

hello 다음 작업 만들기 작업 추가 예제 toohello hello 작업의 필드에 대 한 추가 toohello 레코드 ID를 해당 하는 계정 레코드입니다.

![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid-type-account.png)

이 예제에서는 또한 hello 작업 tooa 특정 사용자를 할당 hello 사용자 레코드 ID를 기반

![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid-type-user.png)

toofind 레코드의 ID를 hello 다음 단원을 참조 하십시오: *hello 레코드 ID 찾기*

## <a name="find-hello-record-id"></a>Hello 레코드 ID 찾기

1. 계정 레코드 등의 레코드를 엽니다.

2. Hello 작업 도구 모음에서 클릭 **팝아웃** ![팝아웃 레코드](./media/connectors-create-api-crmonline/popout-record.png)합니다.
또는 기본 전자 메일 프로그램에 toocopy hello 전체 URL hello 작업 도구 모음에서 클릭 **전자 메일 링크**합니다.

   hello 레코드 ID hello %7b 및 %7 d hello URL의 문자를 인코딩할 사이 표시 됩니다.

   ![흐름 recordId 및 계정 유형](./media/connectors-create-api-crmonline/recordid.png)

## <a name="troubleshooting"></a>문제 해결
tootroubleshoot 논리 앱 hello 이벤트의 hello 상태 세부 정보 보기에서에서 실패 한 단계입니다.

1. **논리 앱** 아래에서 논리 앱을 선택한 다음 **개요**를 클릭합니다. 

   hello 요약 영역에 표시 되 고 hello 논리 앱에 대 한 hello 실행 상태를 제공 합니다. 

   ![논리 앱 실행 상태](./media/connectors-create-api-crmonline/tshoot1.png)

2. tooview 모든 실패 한 실행에 대 한 자세한 내용을 보려면 클릭 hello 실패 이벤트입니다. 실패 한 단계로 tooexpand 해당 단계를 클릭 합니다.

   ![실패한 단계 확장](./media/connectors-create-api-crmonline/tshoot2.png)

   hello 단계의 세부 사항을 표시 되며 hello hello 오류 원인을 해결할 수 있습니다.

   ![실패한 단계 세부 정보](./media/connectors-create-api-crmonline/tshoot3.png)

논리 앱 문제 해결에 대한 자세한 내용은 [논리 앱 오류 진단](../logic-apps/logic-apps-diagnosing-failures.md)을 참조하세요.

## <a name="connector-specific-details"></a>커넥터 관련 세부 정보

모든 트리거 및 hello swagger에 정의 된 작업을 확인 하 고 hello에 어떠한 제한도 볼 [connector 세부 정보](/connectors/crm/)합니다. 

## <a name="next-steps"></a>다음 단계
탐색에서 논리 앱에서 사용할 수 있는 다른 커넥터 hello 우리의 [Api 목록](apis-list.md)합니다.
