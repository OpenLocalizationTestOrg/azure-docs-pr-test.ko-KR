---
title: "aaaUnexpected 동의 확인 프롬프트 tooan 응용 프로그램에 로그인 할 때 | Microsoft Docs"
description: "어떻게 응용 프로그램에 대 한 동의 확인 프롬프트를 표시 하는 경우 tootroubleshoot 통합 한 예기치 않은 Azure AD와"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Tooan 응용 프로그램에 로그인 할 때 예기치 않은 동의 확인 프롬프트

Azure Active Directory와 통합 하는 많은 응용 프로그램 사용 권한 toovarious 리소스 순서 toorun에 필요 합니다. 이러한 리소스는 Azure Active Directory와도 통합 되어 때 hello Azure AD를 사용 하 여 요청에 사용 권한을 tooaccess 동의 프레임 워크 것입니다. 

따라서 표시 된 hello 처음으로 응용 프로그램을 사용 하는 한 번 종종 동의 확인 됩니다. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>사용자에게 동의 확인 프롬프트를 표시하는 시나리오

다양한 시나리오에서 추가 프롬프트를 예상할 수 있습니다.

* hello hello 응용 프로그램에 필요한 사용 권한 집합이 변경 되었습니다.

* 이제 다른 (비관리자) 사용자가 사용 하는 hello 응용 프로그램 hello에 대 한 처음으로 사용할 수 없어서 관리자로 hello 동의한 사용자에 원래 toohello 응용 프로그램입니다.

* hello 동의한 사용자에 원래 toohello 응용 프로그램 관리자는 했지만에-를 대신 하 여 hello 전체 조직을 동의 하지 않을 않았습니다.

* hello 응용 프로그램을 사용 하 여 [증분 및 동적 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) 승인을 처음 후 toorequest 추가 권한이 있습니다. 이것은 추가 응용 프로그램의 선택적 기능이 초기 기능에 필요한 것 이상의 권한을 필요로 할 경우에 종종 사용됩니다.

* 동의가 처음에 부여된 후에 해지되었습니다.

* hello 개발자가 사용 될 때마다 hello 응용 프로그램 toorequire 동의 확인 프롬프트를 구성 (참고:이 가장 좋은 방법은).

## <a name="next-steps"></a>다음 단계

-   [Azure Active Directory에서 앱, 사용 권한 및 동의(v1.0 끝점)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [범위, 권한 및 hello Azure Active Directory (v2.0 끝점)에 동의](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


