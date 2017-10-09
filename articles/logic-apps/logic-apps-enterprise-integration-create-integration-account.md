---
title: "aaaCreate, 연결, 삭제 또는 Azure 논리 앱에 통합 계정을 이동 | Microsoft Docs"
description: "어떻게 통합 toocreate 계정을 한 tooyour 논리 앱 연결"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>통합 계정이란?

통합 계정 toomanage 아티팩트, 스키마, 맵, 인증서, 파트너 및 규약을 포함 하 여 엔터프라이즈 통합 앱을 허용 합니다. 만들 모든 통합 응용 프로그램 통합 계정 tooaccess를 사용 하 여 이러한 스키마, 맵, 인증서, 및 등입니다.

## <a name="create-an-integration-account"></a>통합 계정 만들기

1.  Toohello 로그인 [Azure 포털](http://portal.azure.com "Azure 포털")합니다. Hello 왼쪽된 메뉴에서 선택 **더 많은 서비스**합니다.

    !["추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다. Hello 결과 목록에서 선택 **통합 계정**합니다.

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Hello 페이지의 hello 위쪽 선택 **추가**합니다.

    ![[추가] 선택](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. 통합 계정 및 선택 hello toouse 되도록 Azure 구독 이름을 지정 합니다. 새 **리소스 그룹**을 만들거나 기존 리소스 그룹을 선택할 수 있습니다. 그런 다음 호스팅 통합 계정의 **위치** 및 **가격 책정 계층**을 선택합니다. 

    준비되면 **만들기**를 선택합니다.

    ![통합 계정의 세부 정보를 제공합니다.](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure에 1 분 내에 완료 해야 하는 hello 선택한 위치에 통합 계정 프로 비전 합니다.

5. Hello 페이지를 새로 고칩니다. 새 통합 계정이 나열되어 있습니다.

    ![새 통합 계정이 표시됩니다.](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

다음으로 hello 통합 계정을 해당 만든된 tooyour 논리 앱을 연결 합니다. 

## <a name="link-an-integration-account-tooa-logic-app"></a>통합 계정 tooa 논리 앱 연결

toogive 논리 앱 toomaps, 스키마, 계약 및 기타 아티팩트 링크 hello 통합 계정 tooyour 논리 앱 통합 계정에 액세스 합니다.

### <a name="prerequisites"></a>필수 조건

* 통합 계정
* 논리 앱

> [!NOTE] 
> 통합 계정 및 논리 앱 hello에 있는지 확인 *동일한 Azure 위치* 시작 하기 전에.


1. Hello Azure 포털에서에서 논리 앱을 선택 하 고 논리 앱의 위치를 확인 합니다.

    ![논리 앱을 선택하고 위치를 확인합니다.](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. **설정**에서 **통합 계정**을 선택합니다.

    !["통합 계정" 선택](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. Hello에서 **통합 계정 선택** toolink tooyour 논리 앱을 원하는 선택 hello 통합 계정 목록입니다. 링크의 경우, toofinish 선택 **저장**합니다.

    ![통합 계정 선택](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    계정이 연결 된 tooyour 논리 앱이 고 통합 계정에서 모든 아티팩트는 이제 사용 가능한 tooyour 논리 앱의 통합을 보여 주는 알림을 받게 됩니다.

    ![연결 된 논리 앱 tooyour 통합 계정](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

이제을 통합 계정을 연결 된 tooyour 논리 앱, 논리 앱에서 B2B hello 커넥터를 사용할 수 있습니다. 일반적인 B2B 커넥터 일부에는 XML 유효성 검사 및 플랫 파일 인코딩/디코딩이 포함되어 있습니다.  

## <a name="delete-your-integration-account"></a>통합 계정 삭제

1. **추가 서비스**를 선택합니다.

    !["추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다. Hello 결과 목록에서 선택 **통합 계정**합니다.

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. 원하는 toodelete hello 통합 계정을 선택 합니다.

    ![통합 계정 toodelete 선택](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. Hello 메뉴에서 선택 **삭제**합니다.

    !["삭제" 선택](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Choice toodelete hello 통합 계정을 확인 합니다.

## <a name="move-your-integration-account"></a>통합 계정 이동

toomove 통합 계정 tooanother Azure 구독 또는 리소스 그룹에서 다음이 단계를 수행 합니다.

> [!IMPORTANT]
> 통합 계정 이동한 후에 모든 스크립트 toouse hello 새 리소스 Id를 업데이트 해야 합니다.

1. **추가 서비스**를 선택합니다.

    !["추가 서비스"를 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Hello 검색 상자에 필터에 대 한 "통합"을 입력 합니다. Hello 결과 목록에서 선택 **통합 계정**합니다.

    !["통합"에 대해 필터링하고 "통합 계정"을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. 원하는 toomove hello 통합 계정을 선택 합니다. **설정** 아래에서 **속성**을 선택합니다.

    ![통합 계정 toomove를 선택 합니다. [설정] 아래에서 [속성]을 선택합니다.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Hello 리소스 그룹 또는 통합 계정에 연결 된 Azure 구독으로 변경 합니다.

    ![리소스 그룹 변경 또는 구독 변경 선택](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>다음 단계
* [규약에 대해 자세히 알아보기](../logic-apps/logic-apps-enterprise-integration-agreements.md "엔터프라이즈 통합 규약에 대해 알아보기")  

