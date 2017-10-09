---
title: "응용 프로그램 프록시 응용 프로그램에 대 한 aaaNo 작업 커넥터 그룹을 찾을 | Microsoft Docs"
description: "커넥터 응용 프로그램에 hello Azure AD 응용 프로그램 프록시 커넥터 그룹에 없는 작업 없을 때 발생 하는 문제 해결"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>응용 프로그램 프록시 응용 프로그램에 대해 작동하는 커넥터 그룹 없음

Azure Active Directory와 통합 tooresolve hello 일반적인 문제 1 응용 프로그램 프록시 응용 프로그램에 대 한 커넥터 없을 때 직면 하는이 문서 도움말입니다.

## <a name="overview-of-steps"></a>단계 개요
커넥터 응용 프로그램에 대 한 커넥터 그룹에 없는 작업 인 경우 몇 가지 방법으로 tooresolve hello 문제가 있습니다.

-   Hello 그룹에서 커넥터가 없는 경우에 다음을 수행할 수 있습니다.

    -   Hello 오른쪽 온-프레미스 서버에 새 커넥터를 다운로드 하 고 toothis 그룹 할당

    -   현재 커넥터 hello 그룹으로 이동

-   Hello 그룹에 활성 커넥터가 없는 경우에 다음을 수행할 수 있습니다.

    -   커넥터 아니기 때문에 hello 이유를 식별 및 해결

    -   현재 커넥터 hello 그룹으로 이동

tooknow hello 문제가 중 어느 응용 프로그램에서 hello "Application Proxy" 메뉴를 열고 hello 커넥터 그룹 경고 메시지를 확인 합니다. Hello 그룹 중 하나 (있어야 hello 그룹에서 없음) 커넥터가 하나 이상 필요 하거나 (비활성 커넥터 있을 가능성이 높습니다) 되지만 활성 커넥터가 없는 있는지를 지정 합니다.

   ![Azure Portal에서 커넥터 그룹 선택](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

이러한 각 옵션에 대 한 세부 정보를 아래 hello 해당 섹션을 참조 합니다. 이러한 각 hello 커넥터 관리 페이지에서 시작 한다고 가정 합니다. 위의 hello 오류 메시지에서 찾으려는 경우 hello 경고 메시지를 클릭 하 여 toothis 페이지를 이동할 수 있습니다. 그렇지 않으면 너무 이동 하 여 찾을 수 있습니다**Azure Active Directory**에, **엔터프라이즈 응용 프로그램**, 다음 **응용 프로그램 프록시입니다.**

   ![Azure Portal에서 커넥터 그룹 관리](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>새 커넥터 다운로드

새 커넥터 toodownload hello hello 페이지 위쪽에 hello "커넥터 다운로드" 단추를 사용 합니다.

hello 응용 프로그램으로 동일한 서버를 hello 하는 참고 hello 커넥터 요구 toobe 직접적인 toohello 백 엔드 응용 프로그램을 사용 하는 컴퓨터에 설치 하 고에 일반적으로 배치 됩니다. 다운로드 한 후 커넥터 hello이이 메뉴에 표시 됩니다. hello 커넥터를 클릭 하 고 hello "커넥터 그룹" 드롭 다운 toomake toohello 권한 그룹에 속해 있는지를 사용 하 여 키를 누릅니다. Hello 변경 내용을 저장 합니다.

   ![Hello Azure 포털에서에서 hello 커넥터를 다운로드 합니다.](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>활성 커넥터 이동

Toohello 그룹에 속해야 하며 시야 toohello 대상 백 엔드 응용 프로그램을 포함 하는 활성 커넥터를 설정한 경우 커넥터 hello hello 할당 된 그룹으로 이동할 수 있습니다. 따라서 toodo hello 커넥터를 클릭 합니다. Hello "커넥터 그룹" 필드에 hello 드롭 다운 tooselect hello 올바른 그룹을 사용 하 고 저장을 클릭 합니다.

## <a name="resolve-an-inactive-connector"></a>비활성 커넥터 해결

있더라도 hello hello 그룹의 커넥터 비활성 상태인 경우에 하지 않는 컴퓨터에 있을 가능성이 있는 모든 hello 필요한 포트의 차단을 해제 합니다.

hello 포트를 참조 하십시오.이 문제를 조사 하는 중에 대 한 내용은 문서 문제를 해결 합니다.

## <a name="next-steps"></a>다음 단계
[Azure AD 응용 프로그램 프록시 커넥터 이해](application-proxy-understand-connectors.md)


