---
title: "B2B 엔터프라이즈 통합-Azure 논리 앱에 대 한 aaaEDIFACT 메시지 | Microsoft Docs"
description: "EDI 형식인 B2B 엔터프라이즈 통합용 EDIFACT 메시지를 Azure Logic Apps과 교환"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 2257d2c8-1929-4390-b22c-f96ca8b291bc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/26/2016
ms.author: LADocs; jonfan
ms.openlocfilehash: 496fadcda58de2d36459202b839b0a63c9e5857c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-edifact-messages-for-enterprise-integration-with-logic-apps"></a>엔터프라이즈 통합에 대한 EDIFACT 메시지를 Logic Apps과 교환

Azure Logic Apps의 EDIFACT 메시지를 교환하기 전에 EDIFACT 규약을 만들고 통합 계정에 해당 규약을 저장해야 합니다. 다음은 방법에 대 한 hello 단계 toocreate EDIFACT 규약입니다.

> [!NOTE]
> 이 페이지는 Azure 논리 앱에 대 한 hello EDIFACT 기능을 포함합니다. 자세한 내용은 [X12](logic-apps-enterprise-integration-x12.md)를 참조하세요.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* 이미 정의되고 Azure 구독과 연결된 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)  
* 통합 계정에 이미 정의된 둘 이상의 [파트너](logic-apps-enterprise-integration-partners.md)

> [!NOTE]
> 만들 때 규약, hello 콘텐츠 hello 메시지를 보내거나 받은 hello 파트너 로부터 tooand hello 계약 형식과 일치 해야 합니다.

[통합 계정을 만들고](../logic-apps/logic-apps-enterprise-integration-accounts.md) [파트너를 추가](logic-apps-enterprise-integration-partners.md)한 후에 다음과 같은 단계에 따라 EDIFACT 규약을 만들 수 있습니다.

## <a name="create-an-edifact-agreement"></a>EDIFACT 규약 만들기 

1.  Toohello 로그인 [Azure 포털](http://portal.azure.com "Azure 포털")합니다. Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다.

    > [!TIP]
    > 표시 되지 않으면 **더 많은 서비스**, 먼저 tooexpand hello 메뉴를 할 수 있습니다. 축소 된 hello 메뉴의 hello 위쪽 선택 **표시 메뉴**합니다.

    ![왼쪽 메뉴에서 "추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-edifact/edifact-0.png)

2. Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다. Hello 결과 목록에서 선택 **통합 계정**합니다.

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-edifact/edifact-1-3.png)

3. Hello에 **통합 계정** 블레이드 열리면 toocreate hello 계약 원하는 선택 hello 통합 계정입니다.
통합 계정이 표시되지 않으면 [먼저 만듭니다](../logic-apps/logic-apps-enterprise-integration-accounts.md "통합 계정에 대한 모든 정보") 를.  

    ![여기서 toocreate hello 계약 통합 계정 선택](./media/logic-apps-enterprise-integration-edifact/edifact-1-4.png)

4. Hello 선택 **계약** 바둑판식으로 배열입니다. 계약 타일 없다면 먼저 hello 타일을 추가 합니다.   

    !["규약" 타일 선택](./media/logic-apps-enterprise-integration-edifact/edifact-1-5.png)

5. 열리면 hello 계약 블레이드에서 선택 **추가**합니다.

    !["추가" 선택](./media/logic-apps-enterprise-integration-edifact/edifact-agreement-2.png)

6. **추가** 아래에서 규약의 **이름**을 입력합니다. **규약 유형**에 **EDIFACT**를 선택합니다. 선택 hello **호스트 파트너**, **호스트 Id**, **게스트 파트너**, 및 **게스트 Identity** 의 계약에 대 한 합니다.

    ![규약 세부 정보 제공](./media/logic-apps-enterprise-integration-edifact/edifact-1.png)

    | 속성 | 설명 |
    | --- | --- |
    | 이름 |Hello 계약의 이름 |
    | 규약 유형 | EDIFACT여야 함 |
    | 호스트 파트너 |규약에는 호스트 및 게스트 파트너가 필요합니다. hello 호스트 파트너에는 hello 규약을 구성 하는 hello 조직을 나타냅니다. |
    | 호스트 ID |Hello 호스트 파트너에 대 한 식별자 |
    | 게스트 파트너 |규약에는 호스트 및 게스트 파트너가 필요합니다. hello 게스트 파트너에는 hello 호스트 파트너와 비즈니스를 수행 하는 hello 조직을 나타냅니다. |
    | 게스트 ID |Hello 게스트 파트너에 대 한 식별자 |
    | 수신 설정 |이러한 속성에는 계약에 의해 수신 된 tooall 메시지 적용 됩니다. |
    | 송신 설정 |이러한 속성에는 규약을 전송한 tooall 메시지 적용 됩니다. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>규약에서 수신된 메시지를 처리하는 방법 구성

Hello 규약 속성을 설정한 했으므로 본이 계약 식별 하 고 본이 계약을 통해 파트너 로부터 받은 들어오는 메시지를 처리 하는 방법을 구성할 수 있습니다.

1.  **추가** 아래에서 **수신 설정**을 선택합니다.
와 함께 메시지를 교환 하는 hello 파트너 계약에 따라 이러한 속성을 구성 합니다. 속성 설명에 대 한이 섹션의 hello 테이블을 참조 합니다.

    **수신 설정**은 식별자, 승인, 스키마, 제어 번호, 유효성 검사 및 내부 설정이라는 섹션으로 구성됩니다.

    !["수신 설정" 구성](./media/logic-apps-enterprise-integration-edifact/edifact-2.png)  

2. 을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.

계약에는 들어오는 준비 toohandle tooyour 따르는 메시지만 선택한 설정 합니다.

### <a name="identifiers"></a>식별자

| 속성 | 설명 |
| --- | --- |
| UNB6.1(받는 사람 참조 암호) |1 ~ 14자 사이의 영숫자 값을 입력합니다. |
| UNB6.2(받는 사람 참조 한정자) |1 ~ 2자의 영숫자 값을 입력합니다. |

### <a name="acknowledgments"></a>승인

| 속성 | 설명 |
| --- | --- |
| 메시지(CONTRL) 수신 |이 확인란을 tooreturn 기술 (CONTRL) 승인 toohello 교환 보낸 사람을 선택 합니다. hello 승인이 toohello 교환 보낸 사람 hello 규약에 대 한 hello 송신 설정에 따라 보내집니다. |
| 승인(CONTRL) |이 확인란을 tooreturn 기능 (CONTRL) 승인을 toohello 교환 보낸 사람 hello 승인 전송 hello 규약에 대 한 hello 송신 설정에 따라 toohello 교환 보낸 사람을 선택 합니다. |

### <a name="schemas"></a>스키마

| 속성 | 설명 |
| --- | --- |
| UNH2.1(유형) |트랜잭션 집합 유형을 선택합니다. |
| UNH2.2(버전) |Hello 메시지 버전 번호를 입력 합니다. (최소 1자, 최대 3자) |
| UNH2.3(릴리스) |Hello 메시지 릴리스 번호를 입력 합니다. (최소 1자, 최대 3자) |
| UNH2.5(연결 할당 코드) |할당 된 hello 코드를 입력 합니다. (최대 6자. 영숫자여야 함) |
| UNG2.1(앱 보낸 사람 ID) |1 ~ 35자의 영숫자 값을 입력합니다. |
| UNG2.2(앱 보낸 사람 코드 한정자) |최대 4자의 영숫자 값을 입력합니다. |
| 스키마 |이전에 선택 hello toouse 관련된 통합 계정에서 사용할 스키마를 업로드 합니다. |

### <a name="control-numbers"></a>컨트롤 번호
| 속성 | 설명 |
| --- | --- |
| 교환 컨트롤 번호 중복 허용 안 함 |tooblock 중복 교환을이 속성을 선택 합니다. 선택 하면 hello EDIFACT 디코딩 작업 hello 받은 교환에 대 한 hello 교환 컨트롤 번호 (UNB5)가 이전에 처리 된 교환 컨트롤 번호와 일치 하지 않음을 확인 합니다. 두 번호가 일치 하는 hello 교환 처리 되지 않습니다. |
| (일)마다 중복 UNB5 확인 |Toodisallow 중복 교환 컨트롤 번호를 선택한 경우에 hello 기간 tooperform hello hello 적절 한 값이이 설정에 대해 제공 하 여 확인 하는 시간 (일) 지정할 수 있습니다. |
| 그룹 컨트롤 번호 중복 허용 안 함 |중복 그룹 컨트롤 번호 (UNG5)가 있는 교환을 tooblock,이 속성을 선택 합니다. |
| 트랜잭션 집합 컨트롤 번호 중복 허용 안 함 |이 속성 중복 트랜잭션 집합 컨트롤 번호 (UNH1) 선택 된 교환을 tooblock. |
| EDIFACT 승인 컨트롤 번호 |승인에 toodesignate hello 트랜잭션 집합 참조 번호 사용 하기 위해 hello 접두사, 참조 번호 범위 및 접미사에 대 한 값을 입력 합니다. |

### <a name="validations"></a>유효성 검사

각 유효성 검사 행을 완료하면 다른 행이 자동으로 추가됩니다. 모든 규칙을 지정 하지 않으면 유효성 검사 hello "기본" 행을 사용 합니다.

| 속성 | 설명 |
| --- | --- |
| 메시지 유형 |Hello EDI 메시지 유형을 선택 합니다. |
| EDI 유효성 검사 |Hello 스키마의 EDI 속성, 길이 제한, 빈 데이터 요소 및 후행 구분 기호에 정의 된 대로 데이터 형식에 대해 EDI 유효성 검사를 수행 합니다. |
| 확장 유효성 검사 |Hello 데이터 형식이 없는 경우 EDI 유효성 검사에 hello 데이터 요소 요구 사항 및 반복, 열거 및 데이터 길이 유효성 검사 (최소값/최대값)를 허용 합니다. |
| 선행/후행 0 허용 |추가 선행 또는 후행 0 및 공백 문자를 보존합니다. 이러한 문자를 제거하지 마십시오. |
| 선행/후행 0 자르기 |선행 또는 후행 0 및 공백 문자를 제거합니다. |
| 후행 구분 기호 정책 |후행 구분 기호를 생성합니다. <p>선택 **허용 되지 않습니다** tooprohibit 후행 구분 기호를 반드시 hello에서 받은 교환 합니다. Hello 교환에 후행 구분 기호를 있으면, hello 교환이 잘못 선언 되었습니다. <p>선택 **Optional** tooaccept 여부에 관계 없이 후행 구분 기호를 교환 합니다. <p>선택 **필수** hello 받은 교환 때 후행 구분 기호를 반드시 있어야 합니다. |

### <a name="internal-settings"></a>내부 설정

| 속성 | 설명 |
| --- | --- |
| 후행 구분 기호가 허용되는 경우 빈 XML 태그 만들기 |빈 후행 구분 기호에 대 한 XML 태그를 포함 하는이 확인란 toohave hello 교환 보낸 사람을 선택 합니다. |
| 교환을 트랜잭션 집합으로 분할 - 오류 발생 시 트랜잭션 집합 일시 중단|각 트랜잭션 집합을 개별 XML 문서로 교환의 hello 적절 한 봉투 (envelope) toohello 트랜잭션 집합을 적용 하 여 구문 분석 합니다. 유효성 검사에 실패 하는 hello 트랜잭션 집합만 일시 중단 합니다. |
| 교환을 트랜잭션 집합으로 분할 - 오류 발생 시 교환 일시 중단|각 트랜잭션 집합을 개별 XML 문서로 교환의 hello 적절 한 봉투를 적용 하 여 구문 분석 합니다. Hello 교환에 있는 하나 이상의 트랜잭션 집합이 유효성 검사에 실패 하는 경우 hello 전체 교환이 일시 중단 합니다. | 
| 교환 유지 - 오류 발생 시 트랜잭션 집합 일시 중단 |Hello 교환을 그대로 유지, hello 전체 일괄 처리 된 교환에 대해 XML 문서를 만듭니다. 유효성 검사에 실패 하는 hello 트랜잭션 집합만 일시 중단, 다른 모든 트랜잭션 집합을 tooprocess은 계속 합니다. |
| 교환 유지 - 오류 발생 시 교환 일시 중단 |Hello 교환을 그대로 유지, hello 전체 일괄 처리 된 교환에 대해 XML 문서를 만듭니다. Hello 교환에 있는 하나 이상의 트랜잭션 집합이 유효성 검사에 실패 하는 경우 hello 전체 교환이 일시 중단 합니다. |

## <a name="configure-how-your-agreement-sends-messages"></a>규약에서 메시지를 보내는 방법 구성

본이 계약 식별 하 고 본이 계약을 통해 tooyour 파트너를 전송 하는 보내는 메시지를 처리 하는 방법을 구성할 수 있습니다.

1.  **추가** 아래에서 **송신 설정**을 선택합니다.
사용자와 메시지를 교환하는 파트너와의 규약에 따라 이러한 속성을 구성합니다. 속성 설명에 대 한이 섹션의 hello 테이블을 참조 합니다.

    **송신 설정**은 식별자, 승인, 스키마, 봉투, 문자 집합 및 구분 기호, 컨트롤 번호, 유효성 검사라는 섹션으로 구성됩니다.

    !["송신 설정" 구성](./media/logic-apps-enterprise-integration-edifact/edifact-3.png)    

2. 을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.

이제 규약 준비 toohandle 보내는 tooyour 선택 설정을 준수 하는 메시지입니다.

### <a name="identifiers"></a>식별자

| 속성 | 설명 |
| --- | --- |
| UNB1.2(구문 버전) |**1**과 **4** 사이의 값을 선택합니다. |
| UNB2.3(보낸 사람 역라우팅 주소) |1 ~ 14자의 영숫자 값을 입력합니다. |
| UNB3.3(받는 사람 역라우팅 주소) |1 ~ 14자의 영숫자 값을 입력합니다. |
| UNB6.1(받는 사람 참조 암호) |1 ~ 14자의 영숫자 값을 입력합니다. |
| UNB6.2(받는 사람 참조 한정자) |1 ~ 2자의 영숫자 값을 입력합니다. |
| UNB7(응용 프로그램 참조 ID) |1 ~ 14자의 영숫자 값을 입력합니다. |

### <a name="acknowledgment"></a>승인
| 속성 | 설명 |
| --- | --- |
| 메시지(CONTRL) 수신 |Hello 호스팅된 파트너가 기술 (CONTRL) 승인을 tooreceive 경우이 확인란을 선택 합니다. 이 설정은 지정 hello 메시지를 보내는 사람인 호스팅된 hello 파트너 hello 게스트 파트너 로부터 승인을 요청 합니다. |
| 승인(CONTRL) |Hello 호스팅된 파트너가 기능 (CONTRL) 승인을 tooreceive 경우이 확인란을 선택 합니다. 이 설정은 지정 hello 메시지를 보내는 사람인 호스팅된 hello 파트너 hello 게스트 파트너 로부터 승인을 요청 합니다. |
| 허용된 트랜잭션 집합에 대해 SG1/SG4 루프 생성 |Toorequest 기능 승인이 선택한 경우 수락 된 트랜잭션 집합에 대 한 기능 CONTRL 승인에서 SG1/SG4 루프의이 확인란을 tooforce 세대를 선택 합니다. |

### <a name="schemas"></a>스키마
| 속성 | 설명 |
| --- | --- |
| UNH2.1(유형) |트랜잭션 집합 유형을 선택합니다. |
| UNH2.2(버전) |Hello 메시지 버전 번호를 입력 합니다. |
| UNH2.3(릴리스) |Hello 메시지 릴리스 번호를 입력 합니다. |
| 스키마 |Hello 스키마 toouse를 선택 합니다. 스키마는 통합 계정에 있습니다. tooaccess, 스키마는 먼저 통합 계정 tooyour 논리 앱을 연결 합니다. |

### <a name="envelopes"></a>봉투
| 속성 | 설명 |
| --- | --- |
| UNB8(처리 우선 순위 코드) |1자를 넘지 않는 문자는 영문자 값을 입력합니다. |
| UNB10(통신 규약) |1 ~ 40자의 영숫자 값을 입력합니다. |
| UNB11(테스트 표시기) |테스트 데이터 생성 된 교환이 hello이 확인란을 tooindicate 선택 |
| UNA 세그먼트 적용(서비스 문자열 도움말) |이 확인란을 toogenerate hello 교환 toobe 전송에 대 한 UNA 세그먼트를 선택 합니다. |
| UNG 세그먼트 적용(기능 그룹 헤더) |이 확인란을 toocreate hello 메시지가 전송 toohello 게스트 파트너의 hello 기능 그룹 헤더에 그룹화 세그먼트를 선택 합니다. hello 다음 값을 사용 하는 toocreate hello UNG 세그먼트. <p>**UNG1**의 경우, 1 ~ 6자의 영숫자 값을 입력합니다. <p>**UNG2.1**의 경우, 1 ~ 35자의 영숫자 값을 입력합니다. <p>**UNG2.2**의 경우, 최대 4자의 영숫자 값을 입력합니다. <p>**UNG3.1**의 경우, 1 ~ 35자의 영숫자 값을 입력합니다. <p>**UNG3.2**의 경우, 최대 4자의 영숫자 값을 입력합니다. <p>**UNG6**의 경우, 1 ~ 3자의 영숫자 값을 입력합니다. <p>**UNG7.1**의 경우, 1 ~ 3자의 영숫자 값을 입력합니다. <p>**UNG7.2**의 경우, 1 ~ 3자의 영숫자 값을 입력합니다. <p>**UNG7.3**의 경우, 1 ~ 6자의 영숫자 값을 입력합니다. <p>**UNG8**의 경우, 1 ~ 14자의 영숫자 값을 입력합니다. |

### <a name="character-sets-and-separators"></a>문자 집합 및 구분 기호

Hello 문자 집합이 아닌 다른 구분 기호 toobe 각 메시지 유형에 사용할 다른 집합을 입력할 수 있습니다. 주어진된 메시지 스키마에 대 한 문자 집합을 지정 하지 않으면, hello 기본 문자 집합이 사용 됩니다.

| 속성 | 설명 |
| --- | --- |
| UNB1.1(시스템 식별자) |선택 hello EDIFACT 문자 집합 toobe hello 나가는 교환에 적용 합니다. |
| 스키마 |Hello 드롭 다운 목록에서 스키마를 선택 합니다. 각 행을 완료한 후에 새 행이 자동으로 추가됩니다. Hello 선택한 스키마에 대 한 선택 hello 구분 기호는 hello 다음 구분 기호 설명에 따라 toouse 되도록 설정 합니다. |
| 입력 형식 |입력된 형식을 hello 드롭 다운 목록에서 선택 합니다. |
| Component Separator |tooseparate 복합 데이터 요소는 단일 문자를 입력 합니다. |
| Data Element Separator |복합 데이터 요소 내의 단순 데이터 요소 tooseparate 단일 문자를 입력 합니다. |
| Segment Terminator |EDI 세그먼트의 tooindicate hello 끝 단일 문자를 입력 합니다. |
| 접미사 |Hello 세그먼트 식별자와 함께 사용 되는 hello 문자를 선택 합니다. Hello 다음 접미사를 지정 하면 세그먼트 마침 표시 데이터 요소는 비어 있을 수 있습니다. Hello 세그먼트 마침 표시를 비워 두는 경우 접미사를 지정 해야 합니다. |

### <a name="control-numbers"></a>컨트롤 번호
| 속성 | 설명 |
| --- | --- |
| UNB5(교환 컨트롤 번호) |접두사, hello 교환 컨트롤 번호에 대 한 값의 범위 및 접미사를 입력 합니다. 이러한 값은 사용 되는 보내는 교환의 toogenerate입니다. hello 컨트롤 번호는 필수 사항이 hello 접두사와 접미사는 선택 사항입니다. 각각의 새 메시지;에 대 한 hello 컨트롤 번호가 증가 hello 접두사와 접미사 유지 hello 동일 합니다. |
| UNG5(그룹 컨트롤 번호) |접두사, hello 교환 컨트롤 번호에 대 한 값의 범위 및 접미사를 입력 합니다. 이러한 값은 사용 toogenerate hello 그룹 컨트롤 번호입니다. hello 컨트롤 번호는 필수 사항이 hello 접두사와 접미사는 선택 사항입니다. hello 최대값에 도달할 때까지 hello 제어 번호는 각각의 새 메시지에 대 한 증가 hello 접두사와 접미사 유지 hello 동일 합니다. |
| UNH1(메시지 헤더 참조 번호) |접두사, hello 교환 컨트롤 번호에 대 한 값의 범위 및 접미사를 입력 합니다. 이러한 값은 사용 toogenerate hello 메시지 머리글 참조 번호입니다. hello 참조 번호는 필수 사항이 hello 접두사와 접미사는 선택 사항입니다. 각각의 새 메시지; hello 참조 번호가 증가 hello 접두사와 접미사 유지 hello 동일 합니다. |

### <a name="validations"></a>유효성 검사

각 유효성 검사 행을 완료하면 다른 행이 자동으로 추가됩니다. 모든 규칙을 지정 하지 않으면 유효성 검사 hello "기본" 행을 사용 합니다.

| 속성 | 설명 |
| --- | --- |
| 메시지 유형 |Hello EDI 메시지 유형을 선택 합니다. |
| EDI 유효성 검사 |Hello hello 스키마, 길이 제한, 빈 데이터 요소 및 후행 구분 기호의 EDI 속성으로 정의 된 데이터 형식에 대해 EDI 유효성 검사를 수행 합니다. |
| 확장 유효성 검사 |Hello 데이터 형식이 없는 경우 EDI 유효성 검사에 hello 데이터 요소 요구 사항 및 반복, 열거 및 데이터 길이 유효성 검사 (최소값/최대값)를 허용 합니다. |
| 선행/후행 0 허용 |추가 선행 또는 후행 0 및 공백 문자를 보존합니다. 이러한 문자를 제거하지 마십시오. |
| 선행/후행 0 자르기 |선행 또는 후행 0 문자를 제거합니다. |
| 후행 구분 기호 정책 |후행 구분 기호를 생성합니다. <p>선택 **허용 되지 않습니다** tooprohibit 후행 구분 기호를 반드시 hello에 교환을 보낸 합니다. Hello 교환에 후행 구분 기호를 있으면, hello 교환이 잘못 선언 되었습니다. <p>선택 **Optional** toosend 여부에 관계 없이 후행 구분 기호를 교환 합니다. <p>선택 **필수** 후행 구분 기호를 전송 하는 hello 교환 해야 합니다. |

## <a name="find-your-created-agreement"></a>생성된 규약 찾기

1.  Hello에서 모든 규약 속성을 설정 하는 것이 마친 후 **추가** 블레이드에서 선택 **확인** toofinish 계약 및 반환 tooyour 통합 계정 블레이드 만들기.

    이제 새로 추가된 규약이 **규약** 목록에 표시됩니다.

2.  또한 통합 계정 개요에서 규약을 볼 수도 있습니다. 통합 계정 블레이드를 사용 하 여 선택 **개요**을 선택한 후 hello **계약** 바둑판식으로 배열입니다. 

    ![모든 동의 "계약" 타일 tooview 선택](./media/logic-apps-enterprise-integration-edifact/edifact-4.png)   

## <a name="view-swagger-file"></a>Swagger 파일 보기
tooview hello Swagger hello EDIFACT 커넥터에 대 한 내용은 [EDIFACT](/connectors/edifact/)합니다.

## <a name="learn-more"></a>자세한 정보
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  

