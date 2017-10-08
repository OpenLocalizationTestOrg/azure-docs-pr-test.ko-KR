---
title: "Azure MFA 클라우드 또는 서버 사이의 aaaChoose | Microsoft Docs"
description: "이 적합 한지를 요청 하 여 내 사용자가 현재 위치 및 toosecure 시도 I에 있는 어떤 오전 hello multi-factor authentication 보안 솔루션을 선택 합니다.  클라우드, MFA 서버 또는 AD FS를 선택합니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: ec2270ea-13d7-4ebc-8a00-fa75ce6c746d
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: bd9639e5f744f586d9143c6e90b105ed645eecb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="choose-hello-azure-multi-factor-authentication-solution-for-you"></a>Hello Azure Multi-factor Authentication 솔루션 선택
있기 때문에 여러 버전의 Azure Multi-factor Authentication (MFA), 버전을 적절 한 toouse hello 몇 가지 질문 toofigure를 대답 해야 했습니다.  해당 질문은 다음과 같습니다.

* [어떤 toosecure 려 하는데](#what-am-i-trying-to-secure)
* [Hello 사용자는 어디에 있습니까](#where-are-the-users-located)
* [어떤 기능이 필요합니까?](#what-featured-do-i-need)

hello 다음 섹션에서는 한 지침을 제공 각 이러한 응답을 결정 합니다.

## <a name="what-am-i-trying-toosecure"></a>어떤 toosecure 시도 있습니까?
toodetermine hello 올바른 2 단계 확인 솔루션을 먼저 우리 질문에 대답 해야 hello 무엇 인가 하는 동안 toosecure 보조 인증 방법 사용 합니다.  Azure에 있는 응용프로그램입니까?  또는 원격 액세스 시스템입니까?  항목을 파악 함으로써 포함 상태 toosecure, Multi-factor Authentication toobe 사용 하도록 설정 해야 하는 위치의 hello 질문에 응답할 수 있습니다.  

| 동안 toosecure 무엇입니까 | Hello 클라우드에서 MFA | MFA 서버  |
| --- |:---:|:---:|
| 자사 Microsoft 앱 |● |● |
| Hello 응용 프로그램 갤러리에서 SaaS 응용 프로그램 |● |  |
| Azure AD 앱 프록시를 통해 웹 응용프로그램 게시됨 |● |  |
| Azure AD 응용프로그램 프록시를 통해 IIS 응용프로그램 게시되지 않음 | |● |
| VPN, RDG와 같은 원격 액세스 | ● | ● |

## <a name="where-are-hello-users-located"></a>Hello 사용자는 어디에 있습니까
다음으로, 사용자에 게 있는 보면 hello 클라우드에 관계 없이 toodetermine hello 올바른 솔루션 toouse 있습니다 또는 온-프레미스를 사용 하 여 MFA 서버 hello 합니다.

| 사용자 위치 | Hello 클라우드에서 MFA | MFA 서버  |
| --- |:---:|:---:|
| Azure Active Directory |● | |
| Azure AD 및 AD FS로 페더레이션을 사용한 온-프레미스 AD |● |● |
| Azure AD 및 DirSync를 사용한 온-프레미스 AD, Azure AD Sync, Azure AD Connect - 암호 동기화 없음 |● |● |
| Azure AD 및 DirSync를 사용한 온-프레미스 AD, Azure AD Sync, Azure AD Connect - 암호 동기화 사용 |● | |
| 온-프레미스 Active Directory | |● |

## <a name="what-features-do-i-need"></a>어떤 기능이 필요합니까?
hello 다음 표에서 비교 hello 클라우드에서 Multi-factor authentication 및 Multi-factor Authentication 서버 hello로 사용할 수 있는 hello 기능 합니다.

| 기능 | Hello 클라우드에서 MFA | MFA 서버  |
| --- |:---:|:---:|
| 두 번째 단계로 모바일 앱 알림 | ● | ● |
| 두 번째 단계로 모바일 앱 확인 코드 | ● | ● |
| 두 번째 단계로 전화 통화 | ● | ● |
| 두 번째 단계로 단방향 SMS | ● | ● |
| 두 번째 단계로 양방향 SMS | | ● |
| 두 번째 단계로 하드웨어 토큰 | | ● |
| MFA를 지원하지 않는 Office 365 클라이언트에 대한 앱 암호 | ● | |
| 인증 방법에 대한 관리자 제어 | ● | ● |
| PIN 모드 | | ● |
| 사기 행위 경고 |● | ● |
| MFA 보고서 |● | ● |
| 일회성 바이패스 | | ● |
| 전화 통화에 대한 사용자 지정 인사말 | ● | ● |
| 전화 통화에 대한 사용자 지정 가능한 발신자 번호 | ● | ● |
| 신뢰할 수 있는 IP | ● | ● |
| 신뢰할 수 있는 장치에 대한 MFA 기억 | ● | |
| 조건부 액세스 | ● | ● |
| 캐시 |  | ● |

## <a name="next-steps"></a>다음 단계

toouse multi-factor authentication 또는 hello와 MFA 서버 온-프레미스 클라우드, 여부에서는 시작할 수를 설정 하 고 Azure Multi-factor Authentication을 사용 하 여 있음을 확인 했습니다. **시나리오를 나타내는 hello 아이콘을 선택 합니다.**

<center>




[![클라우드](./media/multi-factor-authentication-get-started/cloud2.png)](multi-factor-authentication-get-started-cloud.md)  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[![서버](./media/multi-factor-authentication-get-started/server2.png)](multi-factor-authentication-get-started-server.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </center>
