---
title: "B2B 엔터프라이즈 통합-Azure 논리 앱에 대 한 aaaX12 메시지 | Microsoft Docs"
description: "EDI 형식인 B2B 엔터프라이즈 통합용 X12 메시지를 Azure Logic Apps과 교환"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 7422d2d5-b1c7-4a11-8c9b-0d8cfa463164
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 20a077b299875a16ada66a500d5f1c8f9972d309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-x12-messages-for-enterprise-integration-with-logic-apps"></a>엔터프라이즈 통합용 X12 메시지를 논리 앱과 교환

Azure Logic Apps의 X12 메시지를 교환하기 전에 X12 규약을 만들고 통합 계정에 해당 규약을 저장해야 합니다. 다음 단계에 대해 hello은 toocreate x12 계약입니다.

> [!NOTE]
> 이 페이지는 Azure 논리 앱에 대 한 hello X12 기능을 포함합니다. 자세한 내용은 [EDIFACT](logic-apps-enterprise-integration-edifact.md)를 참조하세요.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* 이미 정의되고 Azure 구독과 연결된 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)
* 두 개 이상의 [파트너](../logic-apps/logic-apps-enterprise-integration-partners.md) 통합 계정에 정의 되 고 아래에서 X12 hello 식별자를 사용 하 여 구성 **비즈니스 Id**    
* 필수 [스키마](../logic-apps/logic-apps-enterprise-integration-schemas.md) tooyour 업로드 하기 위한 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)

후 [통합 계정 만들기](../logic-apps/logic-apps-enterprise-integration-accounts.md), [파트너 추가](logic-apps-enterprise-integration-partners.md), 있고는 [스키마](../logic-apps/logic-apps-enterprise-integration-schemas.md) toouse 원하는, X12를 만들 수 있습니다 이러한 단계를 수행 하 여 계약입니다.

## <a name="create-an-x12-agreement"></a>X12 규약 만들기

1.  Toohello 로그인 [Azure 포털](http://portal.azure.com "Azure 포털")합니다. Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다. 

    > [!TIP]
    > 표시 되지 않으면 **더 많은 서비스**, 먼저 tooexpand hello 메뉴를 할 수 있습니다. 축소 된 hello 메뉴의 hello 위쪽 선택 **표시 메뉴**합니다.

    ![왼쪽 메뉴에서 "추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-x12/account-1.png)

2.  Hello 검색 상자에 필터로 "통합"을 입력 합니다. Hello 결과 목록에서 선택 **통합 계정**합니다.  

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-x12/account-2.png)

3. Hello에 **통합 계정** 블레이드 열리면 tooadd hello 계약 원하는 선택 hello 통합 계정입니다.
통합 계정이 표시되지 않으면 [먼저 만듭니다](../logic-apps/logic-apps-enterprise-integration-accounts.md "통합 계정에 대한 모든 정보") 를.

    ![여기서 toocreate hello 계약 통합 계정 선택](./media/logic-apps-enterprise-integration-x12/account-3.png)

4. 선택 **개요**을 선택한 후 hello **계약** 바둑판식으로 배열입니다. 계약 타일 없다면 먼저 hello 타일을 추가 합니다. 

    !["규약" 타일 선택](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. 열리면 hello 계약 블레이드에서 선택 **추가**합니다.

    !["추가" 선택](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)     

6. **추가** 아래에서 규약의 **이름**을 입력합니다. Hello 계약 유형 선택 **X12**합니다. 선택 hello **호스트 파트너**, **호스트 Id**, **게스트 파트너**, 및 **게스트 Identity** 의 계약에 대 한 합니다. 더 많은 속성 세부 정보에 대 한이 단계에서는 hello 표를 참조 합니다.

    ![규약 세부 정보 제공](./media/logic-apps-enterprise-integration-x12/x12-1.png)  

    | 속성 | 설명 |
    | --- | --- |
    | 이름 |Hello 계약의 이름 |
    | 규약 유형 | X12여야 합니다. |
    | 호스트 파트너 |규약에는 호스트 및 게스트 파트너가 필요합니다. hello 호스트 파트너에는 hello 규약을 구성 하는 hello 조직을 나타냅니다. |
    | 호스트 ID |Hello 호스트 파트너에 대 한 식별자 |
    | 게스트 파트너 |규약에는 호스트 및 게스트 파트너가 필요합니다. hello 게스트 파트너에는 hello 호스트 파트너와 비즈니스를 수행 하는 hello 조직을 나타냅니다. |
    | 게스트 ID |Hello 게스트 파트너에 대 한 식별자 |
    | 수신 설정 |이러한 속성에는 계약에 의해 수신 된 tooall 메시지 적용 됩니다. |
    | 송신 설정 |이러한 속성에는 규약을 전송한 tooall 메시지 적용 됩니다. |  

  > [!NOTE]
  > 해결 X12 계약 hello 보낸 사람 한정자 및 식별자 및 hello 받는 사람 한정자 및 식별자 hello 파트너와 들어오는 메시지에 정의 된 일치 여부에 따라 달라 집니다. 파트너에 대 한 이러한 값이 변경 하는 경우 너무 hello 계약을 업데이트 합니다.

## <a name="configure-how-your-agreement-handles-received-messages"></a>규약에서 수신된 메시지를 처리하는 방법 구성

Hello 규약 속성을 설정한 했으므로 본이 계약 식별 하 고 본이 계약을 통해 파트너 로부터 받은 들어오는 메시지를 처리 하는 방법을 구성할 수 있습니다.

1.  **추가** 아래에서 **수신 설정**을 선택합니다.
와 함께 메시지를 교환 하는 hello 파트너 계약에 따라 이러한 속성을 구성 합니다. 속성 설명에 대 한이 섹션의 hello 테이블을 참조 합니다.

    **수신 설정**은 식별자, 승인, 스키마, 봉투, 제어 번호, 유효성 검사 및 내부 설정이라는 섹션으로 구성됩니다.

2. 을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.

계약에는 들어오는 준비 toohandle tooyour 따르는 메시지만 선택한 설정 합니다.

### <a name="identifiers"></a>식별자

![식별자 속성 설정](./media/logic-apps-enterprise-integration-x12/x12-2.png)  

| 속성 | 설명 |
| --- | --- |
| ISA1(인증 한정자) |Hello 드롭 다운 목록에서 hello 권한 부여 한정자 값을 선택 합니다. |
| ISA2 |선택 사항입니다. 권한 부여 정보 값을 입력합니다. ISA1에 입력 한 hello 값 00이 아닌 경우 영숫자 문자가 한 개를 10 개 사이로 입력 합니다. |
| ISA3(보안 한정자) |Hello 드롭 다운 목록에서 hello 보안 한정자 값을 선택 합니다. |
| ISA4 |선택 사항입니다. Hello 보안 정보 값을 입력 합니다. ISA3에 입력 한 hello 값 00이 아닌 경우 영숫자 문자가 한 개를 10 개 사이로 입력 합니다. |

### <a name="acknowledgment"></a>승인

![승인 속성 설정](./media/logic-apps-enterprise-integration-x12/x12-3.png) 

| 속성 | 설명 |
| --- | --- |
| TA1이 예상됨 |기술 승인 toohello 교환 보낸 사람을 반환합니다. |
| FA가 예상됨 |기능 승인 toohello 교환 보낸 사람을 반환합니다. 그런 다음 hello 997 또는 999 승인 여부에 따라 hello 스키마 버전 |
| AK2/IK2 루프 포함 |수락된 트랜잭션 집합에 대한 기능 확인에서 AK2 루프를 생성할 수 있습니다. |

### <a name="schemas"></a>스키마

각 트랜잭션 유형(ST1) 및 발신자 응용 프로그램(GS2)에 대한 스키마를 선택합니다. hello 수신 파이프라인 ST1에 대 한 hello 값을 비교 하 여 들어오는 hello 메시지를 디스어셈블 및 여기에서 집합과 여기에서 설정 하는 hello 스키마와 함께 hello 들어오는 메시지의 스키마를 hello hello hello로 들어오는 메시지의 GS2 값 있습니다.

![스키마 선택](./media/logic-apps-enterprise-integration-x12/x12-33.png) 

| 속성 | 설명 |
| --- | --- |
| 버전 |Hello X12 버전 선택 |
| 트랜잭션 유형(ST01) |Hello 트랜잭션 유형 선택 |
| 발신자 응용 프로그램(GS02) |Hello 보낸 사람 응용 프로그램을 선택 합니다. |
| 스키마 |원하는 toouse hello 스키마 파일을 선택 합니다. 스키마는 tooyour 통합 계정에 추가 됩니다. |

> [!NOTE]
> 필요한 hello 구성 [스키마](../logic-apps/logic-apps-enterprise-integration-schemas.md) 업로드 tooyour 즉 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.

### <a name="envelopes"></a>봉투

![트랜잭션 집합의 hello 구분 기호를 지정 합니다: 표준 식별자 또는 반복 구분 기호를 선택 합니다.](./media/logic-apps-enterprise-integration-x12/x12-34.png)

| 속성 | 설명 |
| --- | --- |
| ISA11 사용 |트랜잭션 집합의 구분 기호 toouse를 hello를 지정합니다. <p>선택 **표준 식별자** toouse 마침표 (.) hello hello EDI에에서 hello 들어오는 문서의 소수 표기법 대신 십진수 표기법에 대 한 수신 파이프라인입니다. <p>선택 **반복 구분 기호** 반복적된으로 발생 하는 단순 데이터 요소 또는 반복 되는 데이터 구조에 대 한 toospecify hello 구분 기호입니다. 예를 들어 일반적으로 hello 캐럿 (^)으로 사용 됩니다 hello 반복 구분 기호. HIPAA 스키마에 대 한 hello 캐럿만 사용할 수 있습니다. |

### <a name="control-numbers"></a>컨트롤 번호

![Toohandle 번호 중복을 제어 하는 방법 선택](./media/logic-apps-enterprise-integration-x12/x12-35.png) 

| 속성 | 설명 |
| --- | --- |
| 교환 컨트롤 번호 중복 허용 안 함 |중복 교환을 차단합니다. Hello 받은 교환 컨트롤 번호에 대 한 hello 교환 컨트롤 번호 (ISA13) 확인합니다. 일치 하는 항목이 발견 되 면 hello 수신 파이프라인 hello 교환을 처리 하지 않습니다. Hello에 대 한 값을 제공 하 여 hello 검사를 수행 하기 위한 일 수를 지정할 수 있습니다 *(일) 마다 중복 isa13 확인*합니다. |
| 그룹 컨트롤 번호 중복 허용 안 함 |중복된 그룹 컨트롤 번호가 있는 교환을 차단합니다. |
| 트랜잭션 집합 컨트롤 번호 중복 허용 안 함 |중복된 트랜잭션 집합 컨트롤 번호가 있는 교환을 차단합니다. |

### <a name="validations"></a>유효성 검사

![받은 메시지의 유효성 검사 속성 설정](./media/logic-apps-enterprise-integration-x12/x12-36.png) 

각 유효성 검사 행을 완료하면 다른 행이 자동으로 추가됩니다. 모든 규칙을 지정 하지 않으면 유효성 검사 hello "기본" 행을 사용 합니다.

| 속성 | 설명 |
| --- | --- |
| 메시지 유형 |Hello EDI 메시지 유형을 선택 합니다. |
| EDI 유효성 검사 |Hello 스키마의 EDI 속성, 길이 제한, 빈 데이터 요소 및 후행 구분 기호에 정의 된 대로 데이터 형식에 대해 EDI 유효성 검사를 수행 합니다. |
| 확장 유효성 검사 |Hello 데이터 형식이 없는 경우 EDI 유효성 검사에 hello 데이터 요소 요구 사항 및 반복, 열거 및 데이터 길이 유효성 검사 (최소값/최대값)를 허용 합니다. |
| 선행/후행 0 허용 |추가 선행 또는 후행 0 및 공백 문자를 보존합니다. 이러한 문자를 제거하지 마십시오. |
| 선행/후행 0 자르기 |선행 또는 후행 0 및 공백 문자를 제거합니다. |
| 후행 구분 기호 정책 |후행 구분 기호를 생성합니다. <p>선택 **허용 되지 않습니다** tooprohibit 후행 구분 기호를 반드시 hello에서 받은 교환 합니다. Hello 교환에 후행 구분 기호를 있으면, hello 교환이 잘못 선언 되었습니다. <p>선택 **Optional** tooaccept 여부에 관계 없이 후행 구분 기호를 교환 합니다. <p>선택 **필수** hello 교환 때 후행 구분 기호를 반드시 있어야 합니다. |

### <a name="internal-settings"></a>내부 설정

![내부 설정 선택](./media/logic-apps-enterprise-integration-x12/x12-37.png) 

| 속성 | 설명 |
| --- | --- |
| 10 진수 형식 "Nn" tooa 기본 10 숫자 값 |밑수 10 숫자 값으로 "Nn" hello 형식으로 지정 된 EDI 번호를 변환 합니다. |
| 후행 구분 기호가 허용되는 경우 빈 XML 태그 만들기 |빈 후행 구분 기호에 대 한 XML 태그를 포함 하는이 확인란 toohave hello 교환 보낸 사람을 선택 합니다. |
| 교환을 트랜잭션 집합으로 분할 - 오류 발생 시 트랜잭션 집합 일시 중단|각 트랜잭션 집합을 개별 XML 문서로 교환의 hello 적절 한 봉투 (envelope) toohello 트랜잭션 집합을 적용 하 여 구문 분석 합니다. Hello 유효성 검사가 실패 hello 트랜잭션만 일시 중단 합니다. |
| 교환을 트랜잭션 집합으로 분할 - 오류 발생 시 교환 일시 중단|각 트랜잭션 집합을 개별 XML 문서로 교환의 hello 적절 한 봉투를 적용 하 여 구문 분석 합니다. Hello 교환에 있는 하나 이상의 트랜잭션 집합이 유효성 검사에 실패 하는 경우 전체 교환이 일시 중단 합니다. | 
| 교환 유지 - 오류 발생 시 트랜잭션 집합 일시 중단 |Hello 교환을 그대로 유지, hello 전체 일괄 처리 된 교환에 대해 XML 문서를 만듭니다. Tooprocess 줄이면서 유효성 검사에 실패 하는 hello 트랜잭션 집합만 일시 중단 다른 모든 트랜잭션 집합입니다. |
| 교환 유지 - 오류 발생 시 교환 일시 중단 |Hello 교환을 그대로 유지, hello 전체 일괄 처리 된 교환에 대해 XML 문서를 만듭니다. Hello 교환에 있는 하나 이상의 트랜잭션 집합이 유효성 검사에 실패 하는 경우 hello 전체 교환이 일시 중단 합니다. |

## <a name="configure-how-your-agreement-sends-messages"></a>규약에서 메시지를 보내는 방법 구성

본이 계약 식별 하 고 본이 계약을 통해 tooyour 파트너를 전송 하는 보내는 메시지를 처리 하는 방법을 구성할 수 있습니다.

1.  **추가** 아래에서 **송신 설정**을 선택합니다.
사용자와 메시지를 교환하는 파트너와의 규약에 따라 이러한 속성을 구성합니다. 속성 설명에 대 한이 섹션의 hello 테이블을 참조 합니다.

    **송신 설정**은 식별자, 승인, 스키마, 봉투, 문자 집합 및 구분 기호, 컨트롤 번호, 유효성 검사라는 섹션으로 구성됩니다.

2. 을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.

이제 규약 준비 toohandle 보내는 tooyour 선택 설정을 준수 하는 메시지입니다.

### <a name="identifiers"></a>식별자

![식별자 속성 설정](./media/logic-apps-enterprise-integration-x12/x12-4.png)  

| 속성 | 설명 |
| --- | --- |
| 권한 부여 한정자(ISA1) |Hello 드롭 다운 목록에서 hello 권한 부여 한정자 값을 선택 합니다. |
| ISA2 |권한 부여 정보 값을 입력합니다. 이 값이 00이 아니면 영숫자 문자를 1~10개 사이로 입력합니다. |
| 보안 한정자(ISA3) |Hello 드롭 다운 목록에서 hello 보안 한정자 값을 선택 합니다. |
| ISA4 |Hello 보안 정보 값을 입력 합니다. 이 값은 hello 값 (ISA4) 텍스트 상자에 대 한 00이 아닌 경우에 영숫자 값 최소 사이의 10 개 사이로 입력 합니다. |

### <a name="acknowledgment"></a>승인

![승인 속성 설정](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| 속성 | 설명 |
| --- | --- |
| TA1이 예상됨 |toohello 기술 (TA1) 승인을 교환 보낸 사람을 반환 합니다. 이 설정은 hello 메시지 요청 hello 계약에 hello 게스트 파트너 로부터 승인을 보내는 hello 호스트 파트너를 지정 합니다. Hello hello 규약의 수신 설정에 따라 hello 호스트 파트너에서 게 이러한 승인이 필요 합니다. |
| FA가 예상됨 |toohello 기능 (FA) 승인을 교환 보낸 사람을 반환 합니다. Hello 997 또는 999 승인에 사용 하는 hello 스키마 버전에 따라 할지 여부를 선택 합니다. Hello hello 규약의 수신 설정에 따라 hello 호스트 파트너에서 게 이러한 승인이 필요 합니다. |
| FA 버전 |Hello FA 버전 선택 |

### <a name="schemas"></a>스키마

![스키마 toouse 선택](./media/logic-apps-enterprise-integration-x12/x12-5.png)  

| 속성 | 설명 |
| --- | --- |
| 버전 |Hello X12 버전 선택 |
| 트랜잭션 유형(ST01) |Hello 트랜잭션 유형 선택 |
| 스키마 |Hello 스키마 toouse를 선택 합니다. 스키마는 통합 계정에 있습니다. 스키마를 먼저 선택하면 버전 및 트랜잭션 유형이 자동으로 구성됩니다.  |

> [!NOTE]
> 필요한 hello 구성 [스키마](../logic-apps/logic-apps-enterprise-integration-schemas.md) 업로드 tooyour 즉 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)합니다.

### <a name="envelopes"></a>봉투

![트랜잭션 집합의 hello 구분 기호를 지정 합니다: 표준 식별자 또는 반복 구분 기호를 선택 합니다.](./media/logic-apps-enterprise-integration-x12/x12-6.png) 

| 속성 | 설명 |
| --- | --- |
| ISA11 사용 |트랜잭션 집합의 구분 기호 toouse를 hello를 지정합니다. <p>선택 **표준 식별자** toouse 마침표 (.) hello hello EDI에에서 hello 들어오는 문서의 소수 표기법 대신 십진수 표기법에 대 한 수신 파이프라인입니다. <p>선택 **반복 구분 기호** 반복적된으로 발생 하는 단순 데이터 요소 또는 반복 되는 데이터 구조에 대 한 toospecify hello 구분 기호입니다. 예를 들어 일반적으로 hello 캐럿 (^)으로 사용 됩니다 hello 반복 구분 기호. HIPAA 스키마에 대 한 hello 캐럿만 사용할 수 있습니다. |

### <a name="control-numbers"></a>컨트롤 번호

![컨트롤 번호 속성 지정](./media/logic-apps-enterprise-integration-x12/x12-8.png) 

| 속성 | 설명 |
| --- | --- |
| 컨트롤 버전 번호(ISA12) |Hello X12 표준의 hello 버전 선택 |
| 사용 표시기(ISA15) |교환의 hello 컨텍스트를 선택 합니다.  hello 값은 정보, 프로덕션 데이터 또는 테스트 데이터 |
| 스키마 |Hello GS 및 ST 세그먼트는 toohello 송신 파이프라인이 보내는 X12 인코딩 교환에 대 한 생성 |
| GS1 |이 단계는 선택적 hello 드롭 다운 목록에서 기능 코드 hello에 대 한 값 선택 |
| GS2 |(선택) 응용 프로그램 보낸 사람입니다. |
| GS3 |(선택) 응용 프로그램 받는 사람입니다. |
| GS4 |(선택) CCYYMMDD 또는 YYMMDD를 선택합니다. |
| GS5 |(선택) HHMM, HHMMSS 또는 HHMMSSdd를 선택합니다. |
| GS7 |이 단계는 선택적 hello 드롭 다운 목록에서 담당 에이전시 hello에 대 한 값 선택 |
| GS8 |(옵션), 버전의 hello 문서 |
| 교환 컨트롤 번호(ISA13) |필요한 경우 hello 교환 컨트롤 번호에 대 한 값의 범위를 입력 합니다. 1~999999999 사이의 숫자 값을 입력합니다. |
| 그룹 컨트롤 번호(GS06) |필요한 경우 hello 그룹 컨트롤 번호에 대 한 숫자 범위를 입력 합니다. 1~999999999 사이의 숫자 값을 입력합니다. |
| 트랜잭션 집합 컨트롤 번호(ST02) |필요한 경우 hello 트랜잭션 집합 컨트롤 번호에 대 한 숫자 범위를 입력 합니다. 1~999999999 사이의 숫자 값 범위를 입력합니다. |
| 접두사 |옵션, 승인에 사용 된 트랜잭션 집합 컨트롤 번호의 hello 범위에 대 한 지정 합니다. 가운데 두 필드 hello에 대 한 숫자 값 및 입력 영숫자 값 (필요한 경우) hello 접두사 및 접미사 필드에 대 한 합니다. 이 필요 하 고 hello 최소값 및 최대값 hello 컨트롤 번호를 포함 하는 hello 가운데 필드 |
| 접미사 |옵션, 승인에 사용 되는 트랜잭션 집합 컨트롤 번호의 hello 범위에 대 한 지정 합니다. 가운데 두 필드 hello에 대 한 숫자 값 및 입력 영숫자 값 (필요한 경우) hello 접두사 및 접미사 필드에 대 한 합니다. 이 필요 하 고 hello 최소값 및 최대값 hello 컨트롤 번호를 포함 하는 hello 가운데 필드 |

### <a name="character-sets-and-separators"></a>문자 집합 및 구분 기호

Hello 문자 집합이 아닌 다른 각 메시지 유형에 대해 다른 구분 기호 집합을 입력할 수 있습니다. 문자 집합 주어진된 메시지 스키마를 지정 하지 않으면 hello 기본 문자 집합이 사용 됩니다.

![메시지 유형의 구분 기호 지정](./media/logic-apps-enterprise-integration-x12/x12-9.png) 

| 속성 | 설명 |
| --- | --- |
| 사용 되는 문자 집합 toobe |선택 hello X12 문자 집합 toovalidate hello 속성입니다. hello 옵션은 Basic, 확장 및 u t f 8입니다. |
| 스키마 |Hello 드롭 다운 목록에서 스키마를 선택 합니다. 각 행을 완료한 후에 새 행이 자동으로 추가됩니다. Hello 선택한 스키마에 대 한 선택 hello 구분 기호는 hello 다음 구분 기호 설명에 따라 toouse 되도록 설정 합니다. |
| 입력 형식 |입력된 형식을 hello 드롭 다운 목록에서 선택 합니다. |
| Component Separator |tooseparate 복합 데이터 요소는 단일 문자를 입력 합니다. |
| Data Element Separator |복합 데이터 요소 내의 단순 데이터 요소 tooseparate 단일 문자를 입력 합니다. |
| Replacement Character |Hello 아웃 바운드 X12 메시지를 생성할 때 hello 페이로드 데이터의 모든 구분 기호 문자를 대체 하기 위해 사용 되는 대체 문자를 입력 합니다. |
| Segment Terminator |EDI 세그먼트의 tooindicate hello 끝 단일 문자를 입력 합니다. |
| 접미사 |Hello 세그먼트 식별자와 함께 사용 되는 hello 문자를 선택 합니다. Hello 다음 접미사를 지정 하면 세그먼트 마침 표시 데이터 요소는 비어 있을 수 있습니다. Hello 세그먼트 마침 표시를 비워 두는 경우 접미사를 지정 해야 합니다. |

> [!TIP]
> tooprovide 특수 문자 값을 JSON으로 hello 계약 편집 하 고 hello 특수 문자에 대 한 hello ASCII 값을 제공 합니다.

### <a name="validation"></a>유효성 검사

![보낸 메시지의 유효성 검사 속성 설정](./media/logic-apps-enterprise-integration-x12/x12-10.png) 

각 유효성 검사 행을 완료하면 다른 행이 자동으로 추가됩니다. 모든 규칙을 지정 하지 않으면 유효성 검사 hello "기본" 행을 사용 합니다.

| 속성 | 설명 |
| --- | --- |
| 메시지 유형 |Hello EDI 메시지 유형을 선택 합니다. |
| EDI 유효성 검사 |Hello 스키마의 EDI 속성, 길이 제한, 빈 데이터 요소 및 후행 구분 기호에 정의 된 대로 데이터 형식에 대해 EDI 유효성 검사를 수행 합니다. |
| 확장 유효성 검사 |Hello 데이터 형식이 없는 경우 EDI 유효성 검사에 hello 데이터 요소 요구 사항 및 반복, 열거 및 데이터 길이 유효성 검사 (최소값/최대값)를 허용 합니다. |
| 선행/후행 0 허용 |추가 선행 또는 후행 0 및 공백 문자를 보존합니다. 이러한 문자를 제거하지 마십시오. |
| 선행/후행 0 자르기 |선행 또는 후행 0 문자를 제거합니다. |
| 후행 구분 기호 정책 |후행 구분 기호를 생성합니다. <p>선택 **허용 되지 않습니다** tooprohibit 후행 구분 기호를 반드시 hello에 교환을 보낸 합니다. Hello 교환에 후행 구분 기호를 있으면, hello 교환이 잘못 선언 되었습니다. <p>선택 **Optional** toosend 여부에 관계 없이 후행 구분 기호를 교환 합니다. <p>선택 **필수** 후행 구분 기호를 전송 하는 hello 교환 해야 합니다. |

## <a name="find-your-created-agreement"></a>생성된 규약 찾기

1.  Hello에서 모든 규약 속성을 설정 하는 것이 마친 후 **추가** 블레이드에서 선택 **확인** toofinish 계약 및 반환 tooyour 통합 계정 블레이드 만들기.

    이제 새로 추가된 규약이 **규약** 목록에 표시됩니다.

2.  또한 통합 계정 개요에서 규약을 볼 수도 있습니다. 통합 계정 블레이드를 사용 하 여 선택 **개요**을 선택한 후 hello **계약** 바둑판식으로 배열입니다.

    ![모든 동의 "계약" 타일 tooview 선택](./media/logic-apps-enterprise-integration-x12/x12-1-5.png)   

## <a name="view-hello-swagger"></a>Hello swagger 보기
Hello 참조 [세부 정보를 swagger](/connectors/x12/)합니다. 

## <a name="learn-more"></a>자세한 정보
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](../logic-apps/logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  

