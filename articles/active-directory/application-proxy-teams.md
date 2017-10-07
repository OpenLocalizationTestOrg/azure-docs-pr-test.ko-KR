---
title: "팀에서 Azure AD 응용 프로그램 프록시 앱 aaaAccess | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 tooaccess Microsoft 팀을 통해 온-프레미스 응용 프로그램을 사용 합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Microsoft Teams를 통해 온-프레미스 응용 프로그램에 액세스

Azure Active Directory 응용 프로그램 프록시 장소에 관계 없이, single sign on tooon 온-프레미스 응용 프로그램을 제공 하 고 Microsoft 팀은 한 곳에서 공동 작업을 간소화 합니다. Hello 통합 두 함께 의미 사용자가 어떤 상황에서 팀 동료를 통해 생산성을 높일 수 있습니다. 

사용자가 클라우드 앱 tootheir 팀 채널 추가 [탭을 사용 하 여](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), 하지만 온-프레미스 호스트 된 SharePoint 사이트 또는 모두 사용 하는 계획 도구 경우 어떻게 될까요? 응용 프로그램 프록시는 hello 솔루션입니다. 앱을 추가할 수 있다고 tootheir 응용 프로그램 프록시를 통해 게시를 사용 하 여 채널 hello 동일한 외부 Url은 항상 tooaccess가 앱을 원격 사용 합니다. 및 Azure Active Directory를 통해 동일한 single sign on 환경을 전달 하는 hello 통해 응용 프로그램 프록시를 인증 하기 때문에 있습니다.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Hello 응용 프로그램 프록시 커넥터를 설치 하 고 앱 게시

아직 없는 경우, [테 넌 트에 대 한 응용 프로그램 프록시를 구성 하 고 hello 커넥터 설치](active-directory-application-proxy-enable.md)합니다. 그런 다음, 원격 액세스를 위해 [온-프레미스 응용 프로그램을 게시](application-proxy-publish-azure-portal.md)합니다. Hello 앱을 게시 하는 경우 최종 사용자가 앱 tooTeams hello를 추가 하는 경우 해당 정보가 필요 하므로 hello 외부 URL 메모를 확인 합니다.

게시 된 앱 이미 갖지만 외부 사이트의 Url을 기억 하지 못하는 경우에서 조회 hello [Azure 포털](https://portal.azure.com)합니다. 로그인 한 후 너무 탐색**Azure Active Directory** > **엔터프라이즈 응용 프로그램** > **모든 응용 프로그램** > 앱 선택 > **응용 프로그램 프록시**합니다.

## <a name="add-your-app-tooteams"></a>응용 프로그램 tooTeams 추가

응용 프로그램 프록시를 통해 hello 앱을 게시 한 사용자를 게 알립니다을 자신의 팀 채널에 직접 테이블로 추가할 수 있습니다. 사용자가 다음 세 가지 단계를 수행하도록 합니다.

1. 팀이 응용이 프로그램 tooadd 저장할 채널을 선택 toohello 이동  **+**  tooadd 탭 합니다.

   ![탭 추가 선택](./media/application-proxy-teams/add-tab.png)

2. 선택 **웹 사이트** hello 탭 옵션에서입니다.

   ![웹 사이트 추가](./media/application-proxy-teams/website.png)

3. Hello 탭에 이름을 지정 하 고 hello URL toohello 응용 프로그램 프록시 외부 URL을 설정 합니다. 

   ![탭 이름 및 URL 구성](./media/application-proxy-teams/tab-name-url.png)

팀의 멤버 중 하나 hello 탭에 추가 되 면 표시 hello 채널의 모든 사용자에 대 한 합니다. Access toohello 앱을 설치한 모든 사용자는 Microsoft 팀에 사용 하는 hello 자격 증명으로 single sign-on 액세스를 가져옵니다. Access toohello 앱 하지 않은 모든 사용자는 팀의 hello 탭 하지만 toohello 온-프레미스 응용 프로그램 사용 권한을 부여 하 고 Azure 포털 게시 된 버전의 hello 앱 hello 때까지 차단 됩니다. 

## <a name="next-steps"></a>다음 단계

- 너무 방법에 대해 알아봅니다[온-프레미스 SharePoint 사이트를 게시할](application-proxy-enable-remote-access-sharepoint.md) 응용 프로그램 프록시입니다.
- 앱 toouse 구성 [사용자 지정 도메인](active-directory-application-proxy-custom-domains.md) 의 외부 URL에 대 한 합니다. 
