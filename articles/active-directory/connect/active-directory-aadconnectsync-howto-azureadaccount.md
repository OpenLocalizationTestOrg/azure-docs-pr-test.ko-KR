---
title: "Azure AD Connect 동기화: toomanage hello Azure AD 서비스 계정을 어떻게 | Microsoft Docs"
description: "이 항목 toorestore hello Azure AD 서비스 계정 하는 방법을 설명 합니다."
services: active-directory
keywords: "Tooreset hello에 대 한 암호 방법을 Azure AD Connect 동기화 서비스 계정 커넥터 hello AADSTS70002, AADSTS50054,"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a>Azure AD Connect 동기화: 어떻게 toomanage hello Azure AD 서비스 계정
hello 서비스 hello Azure AD 커넥터에서 사용 하는 계정은 무료 toobe 서비스. 자격 증명 tooreset 해야 할 경우이 항목은 드립니다. 예를 들어, 전역 관리자는 실수 PowerShell을 사용 하 여 hello 서비스 계정에 대해 hello 암호 재설정으로 가집니다.

## <a name="reset-hello-credentials"></a>Hello 자격 증명 다시 설정
Azure AD 커넥터 hello에 정의 된 hello 서비스 계정이 tooauthentication 문제 때문에 Azure AD에 연결할 수 없는 경우에 hello 암호를 재설정할 수 있습니다.

1. Toohello Azure AD Connect 동기화 서버에 로그인 하 고 PowerShell을 시작 합니다.
2. `Add-ADSyncAADServiceAccount`을 실행합니다.  
   ![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)
3. Azure AD 전역 관리자 자격 증명을 제공합니다.

이 cmdlet는 hello hello 서비스 계정의 암호를 다시 설정 하 고 hello 동기화 엔진 및 Azure AD에서 모두 업데이트 합니다.

## <a name="known-issues-these-steps-can-solve"></a>이 단계에서 해결할 수 있다고 알려진 문제
이 섹션은 hello Azure AD 서비스 계정에서 다시 설정 하는 자격 증명으로 수정 된 고객에 의해 보고 된 오류 목록입니다.

- - -
이벤트 6900  
hello 서버 암호 변경 알림을 처리 하는 동안 예기치 않은 오류가 발생 했습니다.  
AADSTS70002: 자격 증명의 유효성 검사 오류. AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS50054: 이전 암호가 인증에 사용되었습니다.

- - -
이벤트 659  
암호 정책 동기화 구성을 검색하는 도중 오류 발생. Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:  
AADSTS70002: 자격 증명의 유효성 검사 오류. AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS50054: 이전 암호가 인증에 사용되었습니다.

## <a name="next-steps"></a>다음 단계
**개요 항목**

* [Azure AD Connect 동기화: 동기화의 이해 및 사용자 지정](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

