---
title: "사용자를 위해 Azure AD Join를 aaaSetting | Microsoft Docs"
description: "관리자가 온-프레미스 디렉터리 및 장치 등록에 Azure AD 조인을 설치하는 방법을 설명합니다."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: bfc5d415-c918-4d8b-afee-b3f41cc28469
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 60a5aeb11292cb6057ab1065c3ab77e5981d0cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-ad-join-in-your-organization"></a>조직에서 Azure AD 조인 설정
Tooeither 동기화가 필요한 Azure Active Directory Join (Azure AD Join)를 설정 하기 전에 온-프레미스 디렉터리의 사용자가 toohello 클라우드 또는 Azure AD에서 관리 되는 계정을 수동으로 만들어야 합니다.

에 대해서는 온-프레미스 사용자 tooAzure AD를 동기화 하는 중에 대 한 자세한 정보가 [Azure Active Directory와 온-프레미스 id 통합](active-directory-aadconnect.md)합니다.

만들기 및 Azure AD에서 사용자 관리, 너무 참조 toomanually[Azure AD의 사용자 관리](https://msdn.microsoft.com/library/azure/hh967609.aspx)합니다.

## <a name="set-up-device-registration"></a>장치 등록 설정
1. 관리자 권한으로 Azure 포털 toohello에 로그온 합니다.
2. Hello 왼쪽된 창에서 선택 **Active Directory**합니다.
3. Hello에 **디렉터리** 탭에서 디렉터리를 선택 합니다.
4. 선택 hello **구성** 탭 합니다.
5. Toohello 이동 **장치** 섹션.
6. Hello에 **장치** 탭, hello 다음을 설정 합니다.  
   * **최대 수의 장치 사용자 단위**: hello 최대 Azure AD에서 사용자가 있는 장치 수를 선택 합니다.  사용자가이 할당량에 도달 됩니다 수 tooadd 추가 장치 하나 이상의 기존 장치가 제거 될 때까지 합니다.
   * **필요한 MULTI-FACTOR AUTH tooJOIN 장치**: 사용자가 필요한 tooprovide 쓸지를 설정할 두 번째 인증 단계 toojoin 자신의 장치 tooAzure AD 합니다. Azure Multi-factor Authentication에 대 한 자세한 내용은 참조 하십시오. [hello 클라우드에서 Azure Multi-factor Authentication 시작](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)합니다.
   * **사용자가 AZURE AD 조인 장치의 수 있습니다.**: toojoin 장치 tooAzure AD는 사용할 수 있는 hello 사용자 및 그룹을 선택 합니다.
   * **추가 관리자에 AZURE AD 조인 장치의**: Azure AD Premium 또는 Enterprise Mobility Suite (EMS) hello 있습니다 선택할 수 있는 사용자는 로컬 관리자 권한이 부여 됩니다 toohello 장치입니다. 전역 관리자 및 장치 소유자에게는 기본적으로 로컬 관리자 권한이 부여됩니다.

<center>![장치 등록 설정](./media/active-directory-azureadjoin/active-directory-aadjoin-configure-devices.png) </center>

사용자를 위해 Azure AD Join를 설정한 후 tooAzure AD 통해 자신의 회사 또는 개인 장치를 연결할 수 있습니다.

다음은 hello 세 가지 시나리오를 Azure AD Join tooenable 사용자 tooset을 사용할 수 있습니다.

* 사용자가 회사 소유의 장치를 조인할 tooAzure AD 직접 합니다.
* 사용자가 회사 소유의 도메인 가입 장치 toohello 온-프레미스 Active Directory와 hello 장치 tooAzure AD까지 확장 합니다.
* 사용자가 추가 작업 또는 학교 계정 tooWindows 개인 장치에

## <a name="additional-information"></a>추가 정보
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

