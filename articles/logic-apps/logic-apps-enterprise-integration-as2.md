---
title: "B2B 엔터프라이즈 통합-Azure 논리 앱에 대 한 aaaAS2 메시지 | Microsoft Docs"
description: "Azure Logic Apps과 B2B 엔터프라이즈 통합용 AS2 메시지 교환"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>논리 앱과 엔터프라이즈 통합용 AS2 메시지 교환

Azure Logic Apps의 AS2 메시지를 교환하기 전에 AS2 규약을 만들고 통합 계정에 해당 규약을 저장해야 합니다. 다음은 방법에 대 한 hello 단계 toocreate AS2 계약입니다.

## <a name="before-you-start"></a>시작하기 전에

다음은 필요한 hello 항목입니다.

* 이미 정의되고 Azure 구독과 연결된 [통합 계정](../logic-apps/logic-apps-enterprise-integration-accounts.md)
* 두 개 이상의 [파트너](logic-apps-enterprise-integration-partners.md) 이미 통합 계정에 정의 되 고 아래에서 AS2 hello 한정자를 사용 하 여 구성 **비즈니스 Id**

> [!NOTE]
> 규약을 만들 때 hello 계약 파일의 hello 콘텐츠 hello 계약 형식과 일치 해야 합니다.    

[통합 계정을 만들고](../logic-apps/logic-apps-enterprise-integration-accounts.md) [파트너를 추가](logic-apps-enterprise-integration-partners.md)한 후에 다음과 같은 단계에 따라 AS2 규약을 만들 수 있습니다.

## <a name="create-an-as2-agreement"></a>AS2 규약 만들기

1.  Toohello 로그인 [Azure 포털](http://portal.azure.com "Azure 포털")합니다.  

2.  Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다. Hello 검색 상자에 입력 **통합** 필터로 합니다. Hello 결과 목록에서 선택 **통합 계정**합니다.

    > [!TIP]
    > 표시 되지 않으면 **더 많은 서비스**, 먼저 tooexpand hello 메뉴를 할 수 있습니다. 축소 된 hello 메뉴의 hello 위쪽 선택 **표시 메뉴**합니다.

    ![추가 서비스, "통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. Hello에 **통합 계정** 블레이드 열리면 toocreate hello 계약 원하는 선택 hello 통합 계정입니다.
통합 계정이 표시되지 않으면 [먼저 만듭니다](../logic-apps/logic-apps-enterprise-integration-accounts.md "통합 계정에 대한 모든 정보") 를.  

    ![여기서 toocreate hello 계약 hello 통합 계정 선택](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Hello 선택 **계약** 바둑판식으로 배열입니다. 계약 타일 없다면 먼저 hello 타일을 추가 합니다.

    !["규약" 타일 선택](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. 열리면 hello 계약 블레이드에서 선택 **추가**합니다.

    !["추가" 선택](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. **추가** 아래에서 규약의 **이름**을 입력합니다. **규약 유형**에 **AS2**를 선택합니다. 선택 hello **호스트 파트너**, **호스트 Id**, **게스트 파트너**, 및 **게스트 Identity** 의 계약에 대 한 합니다.

    ![규약 세부 정보 제공](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | 속성 | 설명 |
    | --- | --- |
    | 이름 |Hello 계약의 이름 |
    | 규약 유형 | AS2여야 함 |
    | 호스트 파트너 |규약에는 호스트 및 게스트 파트너가 필요합니다. hello 호스트 파트너에는 hello 규약을 구성 하는 hello 조직을 나타냅니다. |
    | 호스트 ID |Hello 호스트 파트너에 대 한 식별자 |
    | 게스트 파트너 |규약에는 호스트 및 게스트 파트너가 필요합니다. hello 게스트 파트너에는 hello 호스트 파트너와 비즈니스를 수행 하는 hello 조직을 나타냅니다. |
    | 게스트 ID |Hello 게스트 파트너에 대 한 식별자 |
    | 수신 설정 |이러한 속성에는 계약에 의해 수신 된 tooall 메시지 적용 됩니다. |
    | 송신 설정 |이러한 속성에는 규약을 전송한 tooall 메시지 적용 됩니다. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>규약에서 수신된 메시지를 처리하는 방법 구성

Hello 규약 속성을 설정한 했으므로 본이 계약 식별 하 고 본이 계약을 통해 파트너 로부터 받은 들어오는 메시지를 처리 하는 방법을 구성할 수 있습니다.

1.  **추가** 아래에서 **수신 설정**을 선택합니다.
와 함께 메시지를 교환 하는 hello 파트너 계약에 따라 이러한 속성을 구성 합니다. 속성 설명은이 섹션의 hello 표를 참조 합니다.

    !["수신 설정" 구성](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. 필요에 따라 들어오는 메시지의 hello 속성을 선택 하 여 재정의할 수 있습니다 **메시지 속성 재정의**합니다.

3. toorequire 모든 들어오는 메시지 toobe 서명, 선택 **메시지 서명 필요**합니다. Hello에서 **인증서** 목록에서 기존 [게스트 파트너 공용 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md) hello 메시지에 hello 서명을 유효성을 검사 합니다. 하거나 없는 경우 hello 인증서를 만듭니다.

4.  암호화 된 모든 들어오는 메시지의 toobe 선택 toorequire **메시지 암호화**합니다. Hello에서 **인증서** 목록에서 기존 [호스트 파트너 개인 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md) 들어오는 메시지의 암호를 해독 합니다. 하거나 없는 경우 hello 인증서를 만듭니다.

5. 압축 toorequire 메시지 toobe 선택 **메시지 압축 필요**합니다.

6. 받은 메시지에 대 한 동기 메시지 처리 알림 (MDN) toosend 선택 **MDN 보내기**합니다.

7. 받은 메시지에 Mdn을 등록 하는 toosend **서명 된 MDN 보내기**합니다.

8. toosend 비동기 Mdn 메시지를 받는 선택 **비동기 MDN 보내기**합니다.

9. 을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.

계약에는 들어오는 준비 toohandle tooyour 따르는 메시지만 선택한 설정 합니다.

| 속성 | 설명 |
| --- | --- |
| 메시지 속성 재정의 |받은 메시지의 속성을 재정의할 수 있음을 나타냅니다. |
| 메시지 서명 필요 |디지털 서명 메시지 toobe가 필요 합니다. 서명 확인에 대 한 hello 게스트 파트너 공용 인증서를 구성 합니다.  |
| 메시지 암호화 필요 |암호화 메시지 toobe가 필요 합니다. 암호화되지 않은 메시지는 거부됩니다. Hello 메시지를 암호 해독을 위한 hello 호스트 파트너 개인 인증서를 구성 합니다.  |
| 메시지 압축 필요 |압축 메시지 toobe가 필요 합니다. 압축되지 않은 메시지는 거부됩니다. |
| MDN 텍스트 |hello 기본 메시지 처리 알림 (MDN) toobe toohello 메시지 보낸 사람에 게를 전송 합니다. |
| MDN 전송 |전송 Mdn toobe가 필요 합니다. |
| 서명된 MDN 전송 |서명 된 Mdn toobe가 필요 합니다. |
| MIC 알고리즘 |메시지 서명을 위한 알고리즘 toouse hello를 선택 합니다. |
| 비동기 MDN 전송 | 비동기적으로 전송 하는 메시지 toobe가 필요 합니다. |
| URL | 여기서 toosend hello Mdn hello URL을 지정 합니다. |

## <a name="configure-how-your-agreement-sends-messages"></a>규약에서 메시지를 보내는 방법 구성

본이 계약 식별 하 고 본이 계약을 통해 tooyour 파트너를 전송 하는 보내는 메시지를 처리 하는 방법을 구성할 수 있습니다.

1.  **추가** 아래에서 **송신 설정**을 선택합니다.
와 함께 메시지를 교환 하는 hello 파트너 계약에 따라 이러한 속성을 구성 합니다. 속성 설명은이 섹션의 hello 표를 참조 합니다.

    ![Hello "송신 설정" 속성 설정](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. toosend 서명 된 메시지 tooyour 파트너에서 선택 **메시지 서명 사용**합니다. Hello에 hello 메시지 서명을 위한 **MIC 알고리즘** 목록, 선택 hello *호스트 파트너 개인 인증서 MIC 알고리즘*합니다. 및 hello **인증서** 목록에서 기존 [호스트 파트너 개인 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)합니다.

3. toosend 암호화 된 메시지 toohello 파트너에서 선택 **메시지 암호화 사용**합니다. Hello에 hello 메시지를 암호화 하기 위한 **암호화 알고리즘** 목록, 선택 hello *게스트 파트너 공용 인증서 알고리즘*합니다.
및 hello **인증서** 목록에서 기존 [게스트 파트너 공용 인증서](../logic-apps/logic-apps-enterprise-integration-certificates.md)합니다.

4. 선택 toocompress hello 메시지 **메시지 압축 사용**합니다.

5. 선택 단일 줄으로 toounfold hello HTTP content-type 헤더 **HTTP 헤더 펼침**합니다.

6. tooreceive hello에 대 한 동기 Mdn 메시지를 보낸 **MDN 요청**합니다.

7. 전송 hello 메시지에 Mdn을 등록 하는 tooreceive **서명 된 MDN 요청**합니다.

8. tooreceive hello에 대 한 비동기 Mdn 메시지를 보낸 **비동기 MDN 요청**합니다. 이 옵션을 선택 하는 경우 여기서 toosend hello Mdn에 대 한 hello URL을 입력 합니다.

9. toorequire 비 거부 수신 선택 **NRR**합니다.  

10. MIC hello에 toospecify 알고리즘 형식 toouse 하거나 hello AS2 메시지나 MDN을의 헤더를 나가는 hello 로그인 선택 **SHA2 알고리즘 형식**합니다.  

11. 을 마친 후 확인 되었는지 toosave 설정을 선택 하 여 **확인**합니다.

이제 규약 준비 toohandle 보내는 tooyour 선택 설정을 준수 하는 메시지입니다.

| 속성 | 설명 |
| --- | --- |
| 메시지 서명 사용 |Hello 계약 toobe 서명에서 보낸 모든 메시지가 필요 합니다. |
| MIC 알고리즘 |hello 메시지 서명을 위한 알고리즘 toouse 합니다. Hello 메시지 서명을 위한 hello 호스트 파트너 개인 인증서 MIC 알고리즘을 구성 합니다. |
| 인증서 |메시지 서명을 위한 인증서 toouse hello를 선택 합니다. Hello 메시지 서명을 위한 hello 호스트 파트너 개인 인증서를 구성 합니다. |
| 메시지 암호화 사용 |이 규약에서 보낸 모든 메시지를 암호화하도록 요구합니다. Hello 메시지를 암호화 하기 위한 hello 게스트 파트너 공용 인증서 알고리즘을 구성 합니다. |
| 암호화 알고리즘 |메시지 암호화에 대 한 암호화 알고리즘 toouse를 hello 합니다. Hello 메시지를 암호화 하기 위한 hello 게스트 파트너 공용 인증서를 구성 합니다. |
| 인증서 |hello 인증서 toouse tooencrypt 메시지입니다. Hello 메시지를 암호화 하기 위한 hello 게스트 파트너 개인 인증서를 구성 합니다. |
| 메시지 압축 사용 |이 규약에서 보낸 모든 메시지를 압축하도록 요구합니다. |
| HTTP 헤더 펼침 |Hello HTTP content-type 헤더를 한 줄에 배치합니다. |
| MDN 요청 |이 규약에서 보낸 모든 메시지에 대한 MDN을 요구합니다. |
| 서명된 MDN 요청 |Toobe 서명 toothis 계약 전송 되는 모든 Mdn 필요 합니다. |
| 비동기 MDN 요청 |비동기 Mdn 전송 toobe toothis 동의가 필요합니다. |
| URL |여기서 toosend hello Mdn hello URL을 지정 합니다. |
| NRR 사용 |해결 되었으며 수신 비 거부 수신 (NRR) hello 데이터 증거를 제공 하는 통신 특성이 필요 합니다. |
| SHA2 알고리즘 형식 |MIC hello 또는 hello AS2 메시지 또는 MDN의 헤더를 나가는 hello 로그인에서 알고리즘 형식 toouse를 선택 합니다. |

## <a name="find-your-created-agreement"></a>생성된 규약 찾기

1.  Hello에서 모든 규약 속성을 설정 하는 것이 마친 후 **추가** 블레이드에서 선택 **확인** toofinish 계약 및 반환 tooyour 통합 계정 블레이드 만들기.

    이제 새로 추가된 규약이 **규약** 목록에 표시됩니다.

2.  또한 통합 계정 개요에서 규약을 볼 수도 있습니다. 통합 계정 블레이드를 사용 하 여 선택 **개요**을 선택한 후 hello **계약** 바둑판식으로 배열입니다. 

    ![모든 동의 "계약" 타일 tooview 선택](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Hello swagger 보기
Hello 참조 [세부 정보를 swagger](/connectors/as2/)합니다. 

## <a name="next-steps"></a>다음 단계
* [엔터프라이즈 통합 팩 hello에 대 한 자세한](logic-apps-enterprise-integration-overview.md "엔터프라이즈 통합 팩에 대 한 자세한 정보")  
