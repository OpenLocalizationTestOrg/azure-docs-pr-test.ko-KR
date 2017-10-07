---
title: "설정에서 Azure AD 사용 하 여 Windows 10 장치 aaaSet | Microsoft Docs"
description: "사용자가 hello 설정 메뉴를 통해 AD tooAzure를 조인할 수는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a>설정에서 Azure AD으로 Windows 10 장치 설정
이미 실행 중인 Windows 7 또는 Windows 8 및 컴퓨터 또는 장치를 사용 하 여 업그레이드 된 tooWindows 10 되었습니다 면 hello 설정 메뉴를 통해 Active Directory (Azure AD) tooAzure 조인할 수 있습니다.

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a>hello 설정 메뉴에서 toojoin tooAzure AD
1. Hello에서 **시작** 메뉴 hello 클릭 **설정을** 참입니다.
2. **설정**에서 **시스템**->**정보**->**Azure AD 연결**을 선택합니다.
   
   <center>
   ![Hello 설정 메뉴에서 Azure AD 조인](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center>
3. 클릭 **계속** hello Azure AD Join 메시지 창에 있습니다.
   
   <center>
   ![Azure AD 연결 메시지 창](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center>
4. 로그인 자격 증명을 제공합니다. 이 로그인 환경을 필요한 toocomplete 인증을 모든 hello 단계가 포함 됩니다. 페더레이션된 테 넌 트의 일부인 경우 관리자가 조직에서 호스팅하는 hello 페더레이션 experience와 함께 제공 합니다.
   <center>
   ![로그인 자격 증명 제공](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center>
5. 조직에서 Azure Multi-factor Authentication tooAzure AD에 추가 하기 위해 구성한, 계속 진행 하기 전에 hello 두 번째 요소를 제공 합니다.
6. 클릭 **Accept** hello에 **관리 되는이 장치 toobe 허용** 화면입니다.
7. "장치는 Azure AD에서 조인 된 tooyour 조직이 이제" hello 메시지를 표시 되어야 합니다.

## <a name="additional-information"></a>추가 정보
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)
* [Microsoft Passport를 통해 암호 없이 ID 인증](active-directory-azureadjoin-passport.md)

