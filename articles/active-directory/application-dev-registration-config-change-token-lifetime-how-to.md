---
title: "사용자 지정 개발 응용 프로그램에 대 한 기본값 aaaHow toochange hello 토큰 수명 | Microsoft Docs"
description: "방법을 Azure AD에서 개발 중인 응용 프로그램에 대 한 tooupdate 토큰 수명 정책"
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
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>Toochange hello 토큰 수명 개발 된 응용 프로그램에 대 한 기본 설정 하는 방법

Azure AD Premium에는 응용 프로그램 개발자와 기밀 클라이언트에 대 한 발급 된 토큰의 테 넌 트 관리자 tooconfigure hello 수명을 수 있습니다. 토큰 수명 정책은 테 넌 트 전반 또는 액세스 되는 hello 리소스에 설정 됩니다.

 * 토큰 수명 정책을 tooset 해야 toodownload hello [Azure AD PowerShell 모듈이](https://www.powershellgallery.com/packages/AzureADPreview)합니다.

 * Hello 실행 **연결-azure Ad-확인** 명령입니다.

 * Hello 최대 사용 기간 단일 요소 새로 고침 토큰을 설정 하는 정책의 예는 다음과 같습니다. Hello 정책을 만듭니다.```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * 체크 아웃 hello [구성 토큰 수명](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) toolearn 어떻게 문서 toocreate 기타 사용자 지정 합니다.

## <a name="next-steps"></a>다음 단계
[토큰 수명 구성](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Azure AD 토큰 참조](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

