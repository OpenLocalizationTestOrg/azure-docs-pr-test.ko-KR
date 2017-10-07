---
title: "aaaTwo 단계 확인 및 Azure MFA AD FS-| Microsoft Docs"
description: "Azure MFA 및 AD FS와 tooget 시작 하는 방법을 설명 하는 hello Azure Multi-factor authentication 페이지입니다."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Azure Multi-Factor Authentication 및 Active Directory Federation Services 시작
<center>![클라우드](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

조직에서 AD FS를 사용하여 온-프레미스 Active Directory를 Azure Active Directory에 페더레이션한 경우 Azure Multi-Factor Authentication 사용을 위한 두 가지 옵션이 있습니다.

* Azure Multi-Factor Authentication 또는 Active Directory Federation Services를 사용하여 클라우드 리소스 보안 유지
* Azure Multi-factor Authentication 서버를 사용하여 클라우드 및 온-프레미스 리소스 보안 유지

다음 표에 hello Azure Multi-factor Authentication AD FS와 리소스를 보호 하는 hello 확인 경험을 요약

| 확인 환경 - 브라우저 기반 앱 | 확인 환경 - 비 브라우저 기반 앱 |
|:--- |:--- |:--- |
| Azure Multi-Factor Authentication을 사용하여 Azure AD 리소스 보안 유지 |<li>hello 첫 번째 확인 단계는 수행 하는 온-프레미스 AD FS를 사용 하 여 합니다.</li> <li>hello 두 번째 단계는 클라우드 인증을 사용 하 여 실행 하는 전화 기반 방법.</li> |
| Active Directory Federation Services를 사용하여 Azure AD 리소스 보안 유지 |<li>hello 첫 번째 확인 단계는 수행 하는 온-프레미스 AD FS를 사용 하 여 합니다.</li><li>hello 두 번째 단계는 hello 클레임을 적용 하 여 수행된 된 온-프레미스를입니다.</li> |

페더레이션된 사용자의 앱 암호 관련 주의 사항:

* 앱 암호는 클라우드 인증을 사용하여 확인되므로 페더레이션을 바이패스합니다. 앱 암호를 설정할 때 페더레이션이 능동적으로 사용됩니다.
* 앱 암호를 사용할 경우 온-프레미스 클라이언트 액세스 제어 설정은 적용되지 않습니다.
* 앱 암호에 대한 온-프레미스 인증 로깅 기능이 손실됩니다.
* 계정 사용 안 함/삭제가 hello 클라우드 id에서 앱 암호 사용 안 함/삭제가 지연 되는 디렉터리 동기화에 대 한 toothree 시간이 걸릴 수 있습니다.

## <a name="next-steps"></a>다음 단계
Azure Multi-factor 인증 또는 AD FS와 함께 Azure Multi-factor Authentication 서버 hello에 대 한 설정에 대 한 자세한 내용은 다음 문서는 hello 참조:

* [Azure Multi-Factor Authentication 및 AD FS를 사용하여 클라우드 리소스 보안 유지](multi-factor-authentication-get-started-adfs-cloud.md)
* [Windows Server 2012 R2 AD FS와 Azure Multi-factor Authentication 서버를 사용하여 클라우드 및 온-프레미스 리소스 보안 유지](multi-factor-authentication-get-started-adfs-w2k12.md)
* [AD FS 2.0과 함께 Azure Multi-factor Authentication 서버를 사용하여 클라우드 및 온-프레미스 리소스 보안 유지](multi-factor-authentication-get-started-adfs-adfs2.md)
