---
title: "Azure AD tooan 갤러리 응용 프로그램 프로 비전 aaaHow tooconfigure 사용자 | Microsoft Docs"
description: "다양 한 사용자 계정을 프로 비전 하 고 hello Azure AD 응용 프로그램 갤러리에에서 이미 나열 되어 tooapplications 프로 비전 해제 신속 하 게 구성 하는 방법"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>어떻게 tooconfigure 사용자 Azure AD tooan 갤러리 응용 프로그램을 프로 비전

*사용자 계정 프로 비전* hello 행위 만들기, 업데이트 및/또는 응용 프로그램의 로컬 사용자 프로필 저장소에 사용자 계정 레코드를 사용 하지 않도록 설정 합니다. 대부분의 클라우드 및 SaaS 응용 프로그램 자체 로컬 사용자 프로필 저장소에 hello 사용자 역할 및 사용 권한을 저장 하 고 해당 로컬 저장소에는 이러한 사용자 레코드의 현재 상태는 *필요한* single sign-on 및 액세스 toowork에 대 한 합니다.

Azure 포털 hello에 hello **프로 비전** hello 왼쪽된 탐색 창에서 탭에 엔터프라이즈 응용 프로그램에서 해당 앱에 대해 지원 되는 어떤 프로 비전 모드를 표시 합니다. 다음 두 값 중 하나일 수 있습니다.

## <a name="configuring-an-application-for-manual-provisioning"></a>수동 프로비전에 대한 응용 프로그램 구성

*수동* 프로 비전 해당 응용 프로그램에서 제공 하는 hello 메서드를 사용 하 여 수동으로 사용자 계정을 만들어야 함을 의미 합니다. 해당 앱의 관리 포털에 로그인하고 웹 기반 사용자 인터페이스를 사용하여 사용자를 추가한다는 의미일 수 있습니다. 또는 해당 응용 프로그램에서 제공하는 메커니즘을 사용하여 사용자 계정 세부 정보를 스프레드시트에 업로드한다는 의미일 수 있습니다. 설명서 hello 제공 hello 앱 또는 연락처 hello 앱 개발자 toodetermine wat 메커니즘을 사용할 수 있습니다.

수동 모드 hello 나타나는지 지정된 된 응용 프로그램에 대 한 자동 Azure AD 커넥터를 프로 비전을 이미 만들었다고 hello 앱에 대 한 아직 의미 합니다. 또는 hello 앱은 하지 지원 hello 필수 사용자 관리 API는 toobuild에 대 한 자동화 된 프로비저닝 커넥터 것을 의미 합니다.

지정된 된 앱에 대 한 자동 프로 비전 toorequest 지원, 원하는 경우에 요청을 채울 수 <http://aka.ms/aadapprequest>합니다.

## <a name="configuring-an-application-for-automatic-provisioning"></a>자동 프로비전에 대한 응용 프로그램 구성

*자동*이란 Azure AD 프로비전 커넥터가 이 응용 프로그램에 대해 개발되었음을 의미합니다. Azure AD 서비스 및 작동 방법을 프로 비전 hello에 대 한 자세한 내용은 참조 [자동화 사용자 프로 비전 및 프로 비전 해제 tooSaaS Azure Active Directory와 응용 프로그램](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)합니다.

Tooprovision 특정 사용자 및 그룹 tooan 응용 프로그램 참조 하는 방법에 대 한 자세한 내용은 [엔터프라이즈 앱에 대 한 사용자 계정 프로 비전 관리](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning)합니다.

실제 단계 필요한 tooenable hello 및 구성 자동 프로 비전 hello 응용 프로그램에 따라 달라 집니다.

>[!NOTE]
>설치 프로그램을 응용 프로그램에 대 한 프로비저닝 자습서 특정 toosetting hello 및 hello 앱과 Azure AD toocreate hello 프로비저닝 연결 해당 단계 tooconfigure 다음 검색 하 여 시작 해야 합니다. 
>
>

응용 프로그램 자습서를 찾을 수 있습니다 [방법에 대 한 자습서의 목록 tooIntegrate SaaS 앱 Azure Active Directory와](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list)합니다.

Tooreview 수 프로 비전을 설정 하는 경우에 중요 한 사항은 tooconsider 및 hello 특성 매핑 및 Azure AD toohello 응용 프로그램에서 어떤 사용자 (또는 그룹) 속성 흐름을 정의 하는 워크플로 구성 합니다. Hello "일치 하는 속성"을 설정 사용된 toouniquely 수 식별 및 사용자/그룹 hello 두 시스템 간에 일치 합니다. 이 중요한 프로세스에 대한 자세한 정보

## <a name="next-steps"></a>다음 단계
[Azure Active Directory에서 SaaS 응용 프로그램에 대한 사용자 프로비전 특성 매핑 사용자 지정](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

