---
title: "AD aaaAzure Microsoft 클라우드 독일에 연결"
description: "Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합니다. 이렇게 하면 tooprovide Office 365, Azure 및 SaaS 응용 프로그램에 대 한 일반 id를 Azure AD와 통합 되어 있습니다."
keywords: "소개 tooAzure AD Connect, Azure AD Connect 개요, Azure AD Connect 이란 active directory, 독일에 블랙 포리스트를 설치 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Microsoft 클라우드 독일의 Azure AD Connect - 공개 미리 보기
## <a name="introduction"></a>소개
Azure AD Connect는 온-프레미스 Active Directory와 Azure Active Directory 간의 동기화를 제공합니다.
현재 대부분의 hello 시나리오의 [Microsoft 클라우드 독일](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) hello 연산자에서 수행 해야 합니다. Microsoft 클라우드 독일을 사용할 때는 hello 다음 중 주의 해야 합니다.

* hello 성공적으로 다음 Url 동기화 toooccur에 프록시 서버에 열려 있어야 합니다.
  
  * *.microsoftonline.de
  * *.windows.net
  * * 인증서 해지 목록
* Tooyour Azure AD 디렉터리에 로그인 할 때 hello onmicrosoft.de 도메인의 계정을 사용 해야 합니다.
* 같은 기능 hello 사용할 수 없습니다.
  * Azure AD Connect Health
  * 자동 업데이트
 
## <a name="download"></a>다운로드
Hello Azure AD Connect 블레이드 hello 포털 내에서 Azure AD Connect를 다운로드할 수 있습니다.  Toolocate hello Azure AD Connect 블레이드 아래의 hello 지침을 사용 합니다.

### <a name="hello-azure-ad-connect-blade"></a>Azure AD Connect 블레이드 hello
Toohello Azure 포털에에서 로그인 하면 다음 hello지 않습니다.

1. TooBrowse 이동
2. Azure Active Directory 선택
3. 그런 다음 Azure AD Connect 선택

Hello 다음을 표시 되어야 합니다.

![Azure AD Connect 블레이드](media/active-directory-aadconnect-germany/germany1.png)

hello 다음 설명 hello 블레이드에 표시 된 hello 기능입니다.

| 제목 | 설명 |
| --- | --- |
| 동기화 상태 |동기화가 활성화되었는지 아니면 비활성화되었는지 여부를 알려줍니다. |
| 최신 동기화 |마지막으로 성공한 동기화가 완료 되었습니다 hello 합니다. |
| 페더레이션된 도메인 |현재 구성 된 페더레이션된 도메인 hello 수가 표시 됩니다. |

## <a name="installation"></a>설치
Azure AD Connect tooinstall hello 설명서를 사용할 수 있습니다 [여기](active-directory-aadconnect.md#install-azure-ad-connect)합니다.

## <a name="advanced-features-and-additional-information"></a>고급 기능 및 추가 정보
사용자 지정 설정이나 고급 구성에 대한 추가 정보 및 지침은 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)을 시작하세요.  이 페이지 tooadditional 지침 정보와 링크를 제공합니다.

