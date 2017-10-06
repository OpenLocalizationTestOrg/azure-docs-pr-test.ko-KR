---
title: "aaaAzure AD Connect 및 페더레이션 | Microsoft Docs"
description: "이 페이지는 Azure AD Connect를 사용 하는 AD FS 작업에 대 한 모든 문서에 대 한 hello 중앙 위치입니다."
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: f9107cf5-0131-499a-9edf-616bf3afef4d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: anandy
ms.openlocfilehash: dc70206eee2296c2320712ef2ade48ccebcc912d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-and-federation"></a>Azure AD Connect 및 페더레이션
Azure AD(Azure Active Directory) Connect를 통해 온-프레미스 AD FS(Active Directory Federation Services) 및 Azure AD와 페더레이션을 구성할 수 있습니다. 페더레이션 로그인을 tooenter 자신의 암호를 다시 필요 없이 온-프레미스 암호-여 tooAzure AD 기반 서비스에서 사용자가 toosign hello 회사 네트워크에서 작업 하는 동안 사용할 수 있습니다. AD FS와 함께 hello 페더레이션 옵션을 사용 하면 AD FS의 새 설치를 배포할 수 있습니다 또는 Windows Server 2012 R2 팜에 있는 기존 설치를 지정할 수 있습니다.

이 항목은 hello Azure AD Connect에 대 한 페더레이션 관련 기능에 대 한 정보에 대 한 홈입니다. 링크를 나열 tooall 관련 항목입니다. 링크 tooAzure AD에 연결. 참조 [Azure Active Directory와 온-프레미스 id 통합](active-directory-aadconnect.md)합니다.

## <a name="azure-ad-connect-federation-topics"></a>Azure AD Connect: 페더레이션 항목
| 항목 | 포함 및 시기 tooread 것 |
|:--- |:--- |
| **Azure AD Connect 사용자 로그인 옵션** | |
| [사용자 로그인 옵션 이해](active-directory-aadconnect-user-signin.md) |다양 한 사용자 로그인 옵션 및 hello Azure 로그인 사용자 경험에 미치는 영향에 대해 알아봅니다. |
| **Azure AD Connect를 사용하여 AD FS 설치** | |
| [필수 구성 요소](active-directory-aadconnect-get-started-custom.md#ad-fs-configuration-pre-requisites) |Azure AD Connect 통해 AD FS 설치를 성공적으로 hello 필수 구성 요소를 참조 하십시오. |
| [AD FS 팜 구성](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs) |Azure AD Connect를 사용하여 새 AD FS 팜을 설치합니다. |
| [대체 로그인 ID를 사용하여 Azure AD와 페더레이션](active-directory-aadconnect-federation-management.md#alternateid) | 대체 로그인 ID를 사용하여 페더레이션 구성  |
| **Hello AD FS 구성 수정** | |
| [복구 hello 신뢰](active-directory-aadconnect-federation-management.md#repairthetrust) |복구 hello 현재 신뢰 사이 온-프레미스 AD FS 및 Office 365/Azure입니다. |
| [새 AD FS 서버 추가](active-directory-aadconnect-federation-management.md#addadfsserver) |초기 설치 후 추가적인 AD FS 서버를 통한 AD FS 팜을 확장합니다. |
| [새 AD FS WAP 서버 추가](active-directory-aadconnect-federation-management.md#addwapserver) |초기 설치 후 추가적인 WAP(웹 응용 프로그램 프록시) 서버를 통한 AD FS 팜을 확장합니다. |
| [새 페더레이션된 도메인 추가](active-directory-aadconnect-federation-management.md#addfeddomain) |Azure AD와 페더레이션 하는 다른 도메인 toobe를 추가 합니다. |
| [Hello SSL 인증서 업데이트](active-directory-aadconnectfed-ssl-update.md)| AD FS 팜에 대 한 hello SSL 인증서를 업데이트 합니다. |
| **기타 페더레이션 구성** | |
| [Azure AD의 여러 인스턴스를 AD FS의 단일 인스턴스로 페더레이션](active-directory-aadconnectfed-single-adfs-multitenant-federation.md) | 단일 AD FS 팜을 사용하여 여러 Azure AD 페더레이션| 
| [사용자 지정 회사 로고/일러스트레이션 추가](active-directory-aadconnect-federation-management.md#customlogo) |Hello AD FS 로그인 페이지에 표시 되는 hello 사용자 지정 로고를 지정 하 여 hello 로그인 환경을 수정 합니다. |
| [로그인 설명 추가](active-directory-aadconnect-federation-management.md#addsignindescription) |Hello 로그인에 대 한 설명을 hello AD FS 로그인 페이지를 변경 합니다. |
| [AD FS 클레임 규칙 수정](active-directory-aadconnect-federation-management.md#modclaims) |수정 하거나 tooAzure AD Connect 동기화 구성을 해당 하는 AD FS에서 클레임 규칙을 추가 합니다. |


## <a name="additional-resources"></a>추가 리소스
* [단일 AD FS를 사용하여 2개의 Azure AD 페더레이션](active-directory-aadconnectfed-single-adfs-multitenant-federation.md)
* [Azure에서 AD FS 배포](active-directory-aadconnect-azure-adfs.md)
* [Azure Traffic Manager를 사용하여 Azure에서 고가용성 교차 지리적 AD FS 배포](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)
