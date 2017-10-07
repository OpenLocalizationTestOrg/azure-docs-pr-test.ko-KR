---
title: "기업 (B2B) 메시지-Azure 논리 앱에 대 한 aaaCreate 파트너 | Microsoft Docs"
description: "엔터프라이즈 통합 팩 hello 및 논리 앱 tooadd 파트너 tooyour 통합을 고려 하는 방법에 대해 알아봅니다"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>워크플로에서 기업 간 규약에 파트너 추가 또는 업데이트

파트너는 B2B(기업 간) 트랜잭션에 참여하고 서로 메시지를 교환하는 주체입니다. 사용자와 이러한 트랜잭션의 다른 조직을 나타내는 파트너를 만들려면 서로 전송한 메시지를 식별하고 유효성을 확인하는 정보를 공유해야 합니다. 통합 계정 toorepresent에서 파트너를 만들 수 있습니다 이러한 세부 정보를 설명 하 고 준비 toostart 비즈니스 관계는 둘 다 있습니다.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>파트너는 통합 계정에서 어떤 역할을 갖나요?

파트너 간에 교환 되는 hello 메시지에 대 한 toodefine 세부 정보를 해당 파트너 간의 규약을 만들 있습니다. 그러나 규약을 만들 수 있습니다, 전에 선택 하 여 두 개 이상의 파트너 tooyour 통합 계정을 추가한 여야 합니다. 조직으로 hello hello 계약의 일부 여야 합니다. **호스트 파트너**합니다. 다른 파트너 hello 또는 **게스트 파트너** 나타냅니다 hello 조직 사용자의 조직과 메시지 교환입니다. hello 게스트 파트너는 다른 회사 또는 조직에서 부서도 가능 합니다.

이러한 파트너를 추가한 후에 규약을 만들 수 있습니다.

수신 및 송신 설정은 hello 관점에서의 호스팅 파트너 hello 방향입니다. 예를 들어 hello 설정을 받으며 규약이 hello 호스팅된 파트너에서 게스트 파트너로 보내는 메시지를 수신 하는 방법을 결정 합니다. 마찬가지로, hello 계약에 hello 송신 설정은 호스팅된 hello 파트너 toohello 게스트 파트너로 메시지를 보내는 방법을 나타냅니다.

## <a name="how-toocreate-a-partner"></a>어떻게 toocreate 파트너?

1. Hello Azure 포털에서에서 선택 **찾아보기**합니다.

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. Hello 필터 검색 상자에 입력 **통합**을 선택한 후 **통합 계정** hello 결과 목록에 있습니다.

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Hello 통합 계정을 저장할 tooadd 파트너를 선택 합니다.

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. 선택 hello **파트너** 바둑판식으로 배열입니다.

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. Hello 파트너 블레이드에서 선택 **추가**합니다.

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. 파트너의 이름을 입력하고 **한정자**를 선택합니다. 마지막으로 입력 한 **값** toohelp 앱에 제공 되는 문서를 식별 합니다.

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. 파트너 만들기 프로세스에 선택 hello에 대 한 toosee hello 진행률 *벨* 알림 아이콘입니다.

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. 새 파트너 성공적으로 tooconfirm 추가, 선택 hello **파트너** 바둑판식으로 배열입니다.

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    Hello 파트너 타일을 선택한 후 hello 파트너 블레이드에서 새로 추가 된 파트너에도 표시 됩니다.

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a>통합 계정에서 파트너 tooedit 기존 방법

1. 선택 hello **파트너** 바둑판식으로 배열입니다.
2. Hello 파트너 블레이드를 연 후 tooedit hello 파트너를 선택 합니다.
3. Hello에 **업데이트 파트너** 타일을 변경 합니다.
4. 을 마친 후에 선택할 **저장**, toocancel 변경 내용을 선택 또는 **취소**합니다.

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a>어떻게 toodelete 파트너

1. 선택 hello **파트너** 바둑판식으로 배열입니다.
2. Hello 파트너 블레이드를 연 후 toodelete hello 파트너를 선택 합니다.
3. **삭제**를 선택합니다.

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>다음 단계
* [규약에 대해 자세히 알아보기](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  

