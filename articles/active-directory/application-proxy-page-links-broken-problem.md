---
title: "aaaLinks hello 페이지에서 응용 프로그램 프록시 응용 프로그램에 대해 작동 하지 않는 | Microsoft Docs"
description: "Azure AD와 통합 하는 응용 프로그램 프록시 응용 프로그램에 대 한 링크가 끊어진 tootroubleshoot 발급 하는 방법"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>응용 프로그램 프록시 응용 프로그램에 대 한 hello 페이지에는 링크가 작동 하지 않습니다.

이 문서가 도움이 되었나요 tootroubleshoot Azure Active Directory 응용 프로그램 프록시 응용 프로그램에 대 한 링크 올바르게 작동 하지 않는 이유.

## <a name="overview"></a>개요 
응용 프로그램 프록시 응용 프로그램을 게시 한 후 hello 링크만 hello 응용 프로그램에서 기본적으로 작업 링크 toodestinations hello 내에 포함 된 지 루트 URL을 게시 합니다. hello 링크 hello 응용 프로그램 내에서 작동 하지 않는, hello 응용 프로그램에 대 한 내부 URL hello 아마도 모든 hello 대상 hello 응용 프로그램 내에서 링크의 포함 되지 않습니다.

**이런 문제가 발생하는 이유는 무엇인가요?** 응용 프로그램 프록시 시도 tooresolve hello URL 내에서 내부 URL로 hello 동일 응용 프로그램에서 링크를 클릭 했을 때 응용 프로그램 또는 외부에서 사용 가능한 URL로 합니다. Hello 링크 내에 없는 tooan 내부 URL을 가리키는 경우 hello 동일 응용 프로그램 이러한 버킷 tooeither 속해야 하며 찾을 수 없음 오류가 발생 하지 않습니다.

## <a name="ways-you-can-resolve-broken-links"></a>끊어진 링크 문제를 해결할 수 있는 방법

이 문제는 세 가지 방법으로 tooresolve 합니다. 아래 hello 선택 항목에 나열 된 복잡성에 있습니다.

1.  내부 URL hello hello 응용 프로그램에 대 한 모든 hello 관련 링크를 포함 하는 루트 인지 확인 합니다. 이렇게 하면 동일한 hello 내에서 콘텐츠 게시로 확인 하는 모든 링크 toobe 응용 프로그램입니다.

    Hello 내부 URL을 변경 해도 toochange hello 사용자가 페이지를 방문 하지 않을 경우 hello 홈 페이지 URL toohello 변경 이전에 내부 URL을 게시 합니다. 너무 이동 하 여이 작업을 수행할 수 있습니다 "Azure Active Directory"-&gt; 앱 등록-&gt; hello 응용 프로그램-선택&gt; 속성입니다. 이 속성 탭에서 조정할 수 있습니다 "홈 페이지 URL" hello 필드 표시 toobe hello 방문 페이지를 원하는 합니다.

2.  응용 프로그램에서 정규화 된 도메인 이름 (Fqdn)을 사용 하는 경우 사용 하 여 [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish 응용 프로그램입니다. Hello 동일한 URL toobe 모두 내부적으로 사용 되며 외부에서이 기능을 사용 합니다.

    이 옵션 hello 응용 프로그램 toointernal Url에서 링크를 눌러도 hello 외부적으로 인식도 이후 응용 프로그램에서 hello 링크는 응용 프로그램 프록시를 통해 외부에서 액세스할 수 있는지 확인 합니다. 모든 링크에 여전히 toobelong tooa 필요 응용 프로그램을 게시 합니다. 그러나이 옵션 hello 링크 필요 하지 않습니다 toobelong toohello 동일한 응용 프로그램 toomultiple 응용 프로그램에 속할 수 있습니다.

3.  이러한 옵션 중 어느 것도 쉽지 않은 경우 hello 미리 보기 URL 변환/다시 쓰기를 수행 하는 새로운 기능에 대 한 조인 합니다. 이 옵션을 사용 내부 Url 또는 응용 프로그램의 HTML hello 본문에 있는 링크 수 toohello 외부 응용 프로그램 프록시 Url을 게시 변환 "매핑" 되거나, 합니다. HTML 또는 CSS hello에 대 한 링크에 대 한이 에서만 작동 하 고이 경우에 도움이 되지 링크가 JS를 통해 생성 됩니다. 

결과적으로, 강력 하 게 사용할 수 있는 권장 hello [사용자 지정 도메인](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) 가능 하면 솔루션입니다. Toojoin hello 미리 보기를 보려면 전자 메일로 보내는 < aadapfeedback@microsoft.com > hello applicationId(s) 사용 합니다.

## <a name="next-steps"></a>다음 단계
[기존 온-프레미스 프록시 서버 작업](application-proxy-working-with-proxy-servers.md)

