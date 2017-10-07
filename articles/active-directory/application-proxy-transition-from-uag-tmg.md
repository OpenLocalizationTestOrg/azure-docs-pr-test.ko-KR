---
title: "aaaUpgrade tooAzure AD 응용 프로그램 프록시 | Microsoft Docs"
description: "Microsoft Forefront 또는 Unified Access Gateway를 업그레이드하는 경우 가장 좋은 프록시 솔루션을 선택합니다."
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
ms.date: 07/27/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7dc2633140b384e25792470dadbb7f3fa7992a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compare-remote-access-solutions"></a>원격 액세스 솔루션 비교

Azure Active Directory 응용 프로그램 프록시는 Microsoft에서 제공하는 두 가지 원격 액세스 솔루션 중 하나입니다. 다른 hello는 웹 응용 프로그램 프록시, hello 온-프레미스 버전. 이 두 가지 솔루션은 이전에 Microsoft에서 제공한 제품인 Microsoft Forefront TMG(Threat Management Gateway) 및 UAG(Unified Access Gateway)를 대체합니다. 이 문서 toounderstand를 사용 하 여 이러한 네 가지 솔루션에서 다른 tooeach를 비교 하는 방법입니다. 경우 여전히 hello를 사용 하 여 더 이상 사용 되지 TMG 또는 UAG 솔루션의 응용 프로그램 프록시 hello 프로그램 마이그레이션 tooone이 문서 toohelp 계획을 사용 합니다. 


## <a name="feature-comparison"></a>기능 비교

이 테이블 toounderstand를 사용 하 여 게이트웨이 TMG (Threat Management), Unified Access Gateway (UAG), 응용 프로그램 프록시 WAP (웹), 및 Azure AD 응용 프로그램 프록시 (AP) 비교 tooeach 다른 방법입니다.

| 기능 | TMG | UAG | WAP | AP |
| ------- | --- | --- | --- | --- |
| 인증서 인증 | 예 | 예 | - | - |
| 선택적으로 브라우저 앱 게시 | 예 | 예 | 예 | 예 |
| 사전 인증 및 Single Sign-On | 예 | 예 | 예 | 예 | 
| 계층 2/3 방화벽 | 예 | 예 | - | - |
| 전달 프록시 기능 | 예 | - | - | - |
| VPN 기능 | 예 | 예 | - | - |
| 다양한 프로토콜 지원 | - | 예 | 예, HTTP를 통해 실행하는 경우 | 예, HTTP 또는 원격 데스크톱 게이트웨이를 통해 실행하는 경우 |
| ADFS 프록시 서버 역할 수행 | - | 예 | 예 | - |
| 응용 프로그램 액세스에 대한 단일 포털 | - | 예 | - | 예 |
| 응답 본문 링크 변환 | 예 | 예 | - | 예 | 
| 헤더를 사용한 인증 | - | 예 | - | 예, PingAccess 사용 | 
| 클라우드 규모 보안 | - | - | - | 예 | 
| 조건부 액세스 | - | 예 | - | 예 |
| Hello 완충 영역 (DMZ)에 구성 요소가 없습니다 | - | - | - | 예 |
| 인바운드 연결 없음 | - | - | - | 예 |

대부분의 시나리오에 대 한 hello 최신 솔루션으로 Azure AD 응용 프로그램을 것이 좋습니다. 웹 응용 프로그램 프록시는 AD FS용 프록시 서버가 필요한 시나리오에서만 사용할 수 있으며, Azure Active Directory에서는 사용자 지정 도메인을 사용할 수 없습니다. 

Azure AD 응용 프로그램 프록시 제공 될 때 고유한 유리 toosimilar 제품을 포함 하 여 비교 합니다.

- Azure AD tooon 온-프레미스 리소스를 확장합니다.
   - 클라우드 규모 보안 및 보호
   - 조건부 액세스 및 Multi-factor Authentication과 같은 기능에 쉽게 tooenable는
- Hello 완충 영역에 없는 계정
- 필요한 인바운드 연결 없음
- 사용자가 toofor o 365를 비롯 한 모든 응용 프로그램을 이동 수, Azure AD와 SaaS 앱 통합를 온-프레미스 웹 응용 프로그램에 대 한 액세스 패널입니다. 


## <a name="next-steps"></a>다음 단계

- [Azure AD 응용 프로그램 tooprovide 보안 된 원격 액세스 tooon 온-프레미스 응용 프로그램을 사용 하 여](active-directory-application-proxy-get-started.md)
- [Forefront TMG 및 UAG tooApplication 프록시에서에서 전환](https://blogs.technet.microsoft.com/isablog/2015/06/30/modernizing-microsoft-application-access-with-web-application-proxy-and-azure-active-directory-application-proxy/)합니다.
