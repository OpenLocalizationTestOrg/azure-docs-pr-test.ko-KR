---
title: "hello Azure Active Directory 포털에서 aaaSign 기능 작업 보고서 오류 코드 | Microsoft Docs"
description: "로그인 활동 보고서 오류 코드에 대한 참조입니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: a0ca5b706bfeb0c7ce669712468a083a394712b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-report-error-codes-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory 포털의 로그인 활동 보고서 오류 코드

Hello 사용자 로그인 보고서에서 제공 하는 hello 정보를 통해 답변 tooquestions와 같은 찾을 수 있습니다.

- Azure Active Directory를 사용하여 로그인한 사람은?
- 서명된 앱은?
- 실패한 로그인은? 그리고 실패한 경우 이유는?

이 항목 목록 hello 오류 코드 및 관련된 설명을 hello 합니다. 

## <a name="how-can-i-display-failed-sign-ins"></a>실패한 로그인을 표시하려면 어떻게 해야 합니까? 

첫 번째 항목 지점 tooall 로그인 활동 데이터는  **[로그인](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)**  hello에 **활동** 섹션 **Azure Active**합니다.


![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/61.png "로그인 활동")


로그인 보고서에서 **실패**를 **로그인 상태**로 선택하여 실패한 로그인을 모두 표시할 수 있습니다.


![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/06.png "로그인 활동")

Hello 열립니다 hello 표시 목록에서 항목을 클릭 하면 **활동 세부 정보: 로그인** 블레이드입니다. 이 보기 기능에 대 한 로그인을 hello를 포함 하 여 Azure Active Directory를 추적 하는 모든 hello 정보를 제공 **로그인 오류 코드** 및 **실패 이유**합니다.

![로그인 활동](./media/active-directory-reporting-activity-sign-ins-errors/05.png "로그인 활동")


대체 toousing hello Azure 포털 tooaccess hello 로그인 데이터도 사용 하 여 hello [보고 API](active-directory-reporting-api-getting-started-azure-portal.md)합니다.


hello 다음 섹션에서는 제공 된 모든 가능한 오류와 hello의 전체 목록은 관련 설명 합니다. 

## <a name="error-codes"></a>오류 코드

| 오류| 설명 |
| --- | --- |
| 50001| X 라는 hello 서비스 사용자 Y 라는 hello 테 넌 트에 없습니다. 이 hello 테 넌 트의 관리자에 게 여 hello 응용 프로그램을 설치 하지 않은 경우 발생할 수 있습니다. 또는 리소스 사용자 hello 디렉터리에서 찾을 수 없습니다. 또는 사용할 수 없습니다.|
| 50008| SAML 어설션이 없거나 hello 토큰에 잘못 구성 됩니다.|
| 50011| hello 회신 주소 요소가 잘못 구성 되었거나 hello 응용 프로그램으로 구성 된 회신 주소와 일치 하지 않습니다.|
| 50053| 사용자에 너무 여러 번 잘못 된 사용자 ID 또는 암호와 toosign 려 때문에 계정이 잠겨 있습니다.|
| 50054| 이전 암호가 인증에 사용되었습니다.|
| 50055| 잘못된 암호입니다. 만료된 암호를 입력했습니다.|
| 50057| 사용자 계정을 사용할 수 없습니다.|
| 50058| 사용자의 id에 대 한 정보가 없습니다 자격 증명 또는 사용자 테 넌 트에 없습니다 또는 자동 로그인 요청을 보냈습니다 하지만 사용자가 로그인 이나 서비스에서 없습니다 tooauthenticate hello 사용자 제공 중에서 찾을 수 있습니다.|
| 50074| 강력한 인증(2단계)이 필요합니다.|
| 50079| 사용자는 두 번째 단계 인증에 대 한 tooenroll 필요|
| 50126| 잘못된 사용자 이름 또는 암호이거나 잘못된 온-프레미스 사용자 이름 또는 암호입니다.|
| 50131| 다양한 조건부 액세스 오류에 사용됩니다. 예: 잘못 된 Windows 장치 상태 이면 요청이 차단 기한 toosuspicious 활동, 액세스 정책 및 보안 정책을 결정 합니다.|
| 50133| 세션 기한 tooexpiration 또는 최근에 암호 변경을 올바르지 않습니다.|
| 50144| 사용자의 Active Directory 암호가 만료되었습니다.|
| 65001| 응용 프로그램 X 권한 tooaccess 응용 Y 없는 또는 hello 사용 권한 해지 되었습니다. 또는 hello 사용자 또는 관리자가 되지 동의 toouse hello 응용 프로그램 ID X. 송신이 사용자 및 리소스에 대 한 대화형 권한 부여 요청을 합니다. Hello 사용자 또는 관리자가 toouse hello 응용 프로그램 ID X. 보내기 권한 부여 요청 tooyour 테 넌 트 관리자 tooact hello 응용 프로그램을 대신 하 여 동의 하지 또는: 리소스에 대 한 Y: Z.|
| 65005| 리소스 액세스 목록 hello 리소스에서 응용 프로그램을 검색할 수를 포함 하지 않거나 hello 클라이언트 응용 프로그램에서 해당 필수 리소스 액세스 목록 또는 잘못 된 반환 된 그래프 서비스에 지정 되지 않은 액세스 tooresource를 요청 하는 hello 응용 프로그램이 필요 요청 또는 리소스를 찾을 수 없습니다.|
| 70001| X 라는 hello 응용 프로그램 Y 라는 hello 테 넌 트에 없습니다. 이 수 발생할 hello 응용 프로그램으로 설치 되지 않은 경우 hello hello 테 넌 트 또는 승인된 tooby 관리자 hello 테 넌 트의 모든 사용자입니다. 인증 요청 toohello 잘못 된 테 넌 트를 보냈을 수 있습니다.|
| 80001| 사용할 수 있는 인증 에이전트가 없습니다.|
| 80002| 인증 에이전트의 암호 유효성 검사 요청 시간이 초과되었습니다.|
| 80003| 인증 에이전트에서 받은 응답이 잘못되었습니다.|
| 80004| 로그인 요청에 잘못된 UPN(사용자 계정 이름)이 사용되었습니다.|
| 80005| 인증 에이전트: 오류가 발생했습니다.|
| 80007| 인증 에이전트 수 없습니다 tooconnect tooActive 디렉터리입니다.|
| 80010| 인증 에이전트 수 없습니다 toodecrypt 암호입니다.|
| 81001| 사용자의 Kerberos 티켓이 너무 큽니다.|
| 81002| 없습니다 toovalidate 사용자의 Kerberos 티켓입니다.|
| 81003| 없습니다 toovalidate 사용자의 Kerberos 티켓입니다.|
| 81004| Kerberos 인증 시도가 실패했습니다.|
| 81008| 없습니다 toovalidate 사용자의 Kerberos 티켓입니다.|
| 81009| 없습니다 toovalidate 사용자의 Kerberos 티켓입니다.|
| 81010| 원활한 SSO 없으므로 hello 사용자의 Kerberos 티켓이 만료 되었거나 올바르지 않습니다.|
| 81011| 없습니다 toofind 사용자 개체 hello 사용자의 Kerberos 티켓에 대 한 정보를 기반 합니다.|
| 81012| tooAzure AD에서에서 toosign hello 사용자는 hello 장치에 로그인 하는 hello 사용자와에서 다릅니다.|
| 81013| 없습니다 toofind 사용자 개체 hello 사용자의 Kerberos 티켓에 대 한 정보를 기반 합니다.|
| 90014| 예상된 된 필드는 hello 자격 증명에 없을 경우 다양 한 경우에 사용 합니다.|
| 90093| 그래프는 hello 요청에 대 한 금지 된 오류 코드와 함께 반환 합니다.|



## <a name="next-steps"></a>다음 단계

자세한 내용은 참조 hello [hello Azure Active Directory 포털의 로그인 활동 보고서](active-directory-reporting-activity-sign-ins.md)합니다.

