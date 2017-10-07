---
title: "aaaHow toogrant 권한 tooa 개발 된 응용 프로그램 | Microsoft Docs"
description: "Azure AD 포털 또는 URL 매개 변수 방법 hello toogrant 권한은 tooyour 개발 된 응용 프로그램 사용 하 여"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a>어떻게 toogrant 권한을 tooa 개발 된 응용 프로그램

앱에서 미리 toogrant 동의 원하는 하거나 tooan 앱 동의한 하지는 동안 오류가 발생 실행 중인 경우 아래에 다음이 단계를 시도 하십시오.

## <a name="how-tooperform-admin-consent-for-your-application"></a>어떻게 응용 프로그램에 대 한 관리 동의가 tooperform

이 hello 조직의 모든 사용자에 대 한 동의 toohello 응용 프로그램에 부여 됩니다.

1. Toohello 이동 **앱 등록** 블레이드로는 **전역 관리자**을 선택한 후 hello 앱.

2. 선택 **필요한 권한**, 마지막으로 hello **사용 권한 부여** hello hello 블레이드 위쪽에 단추입니다.

또는 너무 요청을 만들 수*login.microsoftonline.com* 와 응용 프로그램 구성에 추가 하 고 *프롬프트 & = admin\_동의*합니다. 관리자 자격 증명을 사용 하 여 서명 후 hello 앱 승인 된 모든 사용자에 대 한 합니다.

## <a name="how-tooforce-user-consent-for-your-application"></a>어떻게 응용 프로그램에 대 한 사용자 동의 tooforce

* 인증 요청에 추가 *프롬프트 & 동의 =* tooconsent 최종 사용자가 인증 될 때마다 해야 합니다.

## <a name="next-steps"></a>다음 단계

[승인 및 앱 통합 tooAzureAD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[AzureAD v2.0 수렴형 앱에 대한 동의 및 권한 부여](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[AzureAD StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
