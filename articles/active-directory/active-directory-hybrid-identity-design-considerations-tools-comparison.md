---
title: "하이브리드 ID: 디렉터리 통합 도구 비교 | Microsoft Docs"
description: "이 페이지는 hello를 비교 하는 포괄적인 표 디렉터리 통합에 사용할 수 있는 다양 한 디렉터리 통합 도구를 제공 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>하이브리드 ID 디렉터리 통합 도구 비교
Hello 년간 hello 디렉터리 통합 도구 증가 있고 발전 하 고 있습니다.  이 문서는 toohelp 이러한 도구를 간편된 하 게 볼 및 각각에 사용할 수 있는 hello 기능 비교를 제공 합니다.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect hello 구성 요소 이전에 Dirsync 및 AAD Sync로 릴리스된 기능을 통합 합니다. 이러한 도구를 개별적으로 출시 되 고 더 이상 되 고 향후 모든 개선 업데이트 tooAzure AD에에서 포함 될 연결, 여기서 tooget hello 최신 기능 항상 알 수 있도록 합니다.
> 
> 디렉터리 동기화 및 Azure AD Sync는 사용되지 않습니다. 자세한 내용은 [여기](active-directory-aadconnect-dirsync-deprecated.md)를 참조하세요.
> 
> 

Hello 각 hello 테이블에 대 한 다음 키를 사용 합니다.

● = 지금 사용 가능  
FR = 향후 릴리스  
PP = 공개 미리 보기 상태  

## <a name="on-premises-toocloud-synchronization"></a>온-프레미스 tooCloud 동기화
| 기능 | Azure Active Directory 연결 | Azure Active Directory 동기화 서비스(AAD Sync) | Azure Active Directory 동기화 도구(디렉터리 동기화) | Forefront Identity Manager(FIM) 2010 R2 | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Toosingle 연결 온-프레미스 AD 포리스트에 |● |● |● |● |● |
| 연결 toomultiple 온-프레미스 AD 포리스트가 있음 |● |● | |● |● |
| 연결 toomultiple 온-프레미스 Exchange 조직 |● | | | | |
| Toosingle 온-프레미스 LDAP 디렉터리 연결 |FR | | |● |● |
| Toomultiple 온-프레미스 LDAP 디렉터리 연결 |FR | | |● |● |
| 연결 tooon 온-프레미스 AD와 온-프레미스 LDAP 디렉터리의 경우 |FR | | |● |● |
| Toocustom 시스템 (즉, SQL, Oracle, MySQL 등)에 연결 |FR | | |● |● |
| 고객 정의 특성(디렉터리 확장) 동기화 |● | | | | |
| Tooon 온-프레미스 HR (예:: SAP, Oracle eBusiness, PeopleSoft) 연결 |FR | | |● |● |
| Tooon 온-프레미스 시스템을 프로 비전에 대 한 FIM 동기화 규칙 및 커넥터를 지원 합니다. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>클라우드 tooOn-프레미스 간 동기화
| 기능 | Azure Active Directory 연결 | Azure Active Directory 동기화 서비스 | Azure Active Directory 동기화 도구(디렉터리 동기화) | Forefront Identity Manager(FIM) 2010 R2 | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 장치의 쓰기 저장 |● | |● | | |
| 특성 쓰기 저장(Exchange 하이브리드 배포) |● |● |● |● |● |
| 그룹 개체의 쓰기 저장 |● | | | | |
| 암호의 쓰기 저장(SSPR(셀프 서비스 암호 재설정) 및 암호 변경에서) |● |● | | | |

## <a name="authentication-feature-support"></a>인증 기능 지원
| 기능 | Azure Active Directory 연결 | Azure Active Directory 동기화 서비스 | Azure Active Directory 동기화 도구(디렉터리 동기화) | Forefront Identity Manager(FIM) 2010 R2 | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 단일 온-프레미스 AD 포리스트에 대한 암호 동기화 |● |● |● | | |
| 여러 온-프레미스 AD 포리스트에 대한 암호 동기화 |● |● | | | |
| 페더레이션이 있는 Single Sign-On |● |● |● |● |● |
| 암호의 쓰기 저장(SSPR 및 암호 변경에서) |● |● | | | |

## <a name="set-up-and-installation"></a>설정 및 설치
| 기능 | Azure Active Directory 연결 | Azure Active Directory 동기화 서비스 | Azure Active Directory 동기화 도구(디렉터리 동기화) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| 도메인 컨트롤러에서 설치 지원 |● |● |● | |
| SQL Express를 사용하여 설치 지원 |● |● |● | |
| 디렉터리 동기화에서 쉽게 업그레이드 |● | | | |
| Admin UX tooWindows 서버 언어의 지역화 |● |● |● | |
| 최종 사용자 UX tooWindows 서버 언어의 지역화 | | | |● |
| Windows Server 2008 및 Windows Server 2008 R2 지원 |● 동기화용, 페더레이션용이 아님 |● |● |● |
| Windows Server 2012 및 Windows Server 2012 R2 지원 |● |● |● |● |

## <a name="filtering-and-configuration"></a>필터링 및 구성
| 기능 | Azure Active Directory 연결 | Azure Active Directory 동기화 서비스 | Azure Active Directory 동기화 도구(디렉터리 동기화) | Forefront Identity Manager(FIM) 2010 R2 | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| 도메인 및 조직 구성 단위에 대한 필터링 |● |● |● |● |● |
| 개체의 특성 값에 대한 필터링 |● |● |● |● |● |
| 특성 toobe 동기화 (MinSync)의 최소 집합을 허용 합니다. |● |● | | | |
| 특성 흐름에 적용 하는 다른 서비스 템플릿을 toobe 허용 |● |● | | | |
| AD tooAzure AD의에서 흐름에서 특성 제거 허용 |● |● | | | |
| 특성 흐름에 대한 고급 사용자 지정 허용 |● |● | |● |● |

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

