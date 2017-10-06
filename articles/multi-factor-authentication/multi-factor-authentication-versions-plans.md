---
title: "계획 aaaAzure MFA 버전 및 소비 | Microsoft Docs"
description: "Multi-factor Authentication 클라이언트 hello 및 hello 다양 한 방법을 사용할 수 있는 버전에 대 한 정보입니다. 각 사용 계획에 대한 세부 정보"
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>어떻게 tooget Azure Multi-factor Authentication

계정을 tooprotecting 있어 2 단계 인증 해야 표준 조직 전체에서 합니다. 이 기능은 tooresources 액세스 권한이 있는 관리자 계정에 특히 중요 합니다. 이러한 이유로 Microsoft 기본 2 단계 확인 기능 tooOffice 365 및 다단계 인증을 제공합니다. Admins에 대 한 tooupgrade hello 기능 하려면 하거나 확장 하면 사용자의 2 단계 확인 toohello rest, Azure Multi-factor Authentication을 구매할 수 있습니다. 

이 문서에서는 hello tooadministrators 및 hello 전체 Azure MFA 버전을 제공 하는 hello 버전 차이점에 설명 하 고 각각에 사용할 수 있는 기능을 지정 합니다. 바꾸려는 경우 toodeploy hello Azure MFA 제공 완료, hello 뒷부분에 나오는 섹션에서는 구현 옵션 및 Microsoft 소비를 계산 하는 방법입니다.

>[!IMPORTANT]
>이 문서는 toobe 위한 이해 가이드 toohelp hello Azure Multi-factor Authentication 다양 한 방법 toobuy 합니다. 가격 및 요금 청구에 대 한 자세한 내용은 항상 참조 해야 toohello [가격 책정 페이지는 Multi-factor Authentication](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)합니다.

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication의 사용 가능한 버전

hello 다음 표에서 설명 multi-factor authentication의 세 버전 간 차이점 및 hello:

| 버전 | 설명 |
| --- | --- |
| Office 365용 Multi-Factor Authentication |이 버전 Office 365 응용 프로그램 에서만 작동 하며 hello Office 365 포털에서 관리 됩니다. 관리자는 [2단계 인증을 사용하여 Office 365 리소스의 보안을 유지](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6)할 수 있습니다. 이 버전은 Office 365 구독에 포함되어 있습니다. |
| Azure 관리자를 위한 Multi-Factor Authentication | Azure 테넌트의 전역 관리자는 전역 관리자 계정에 대해 2단계 인증을 추가 비용 없이 사용할 수 있습니다.|
| Azure Multi-Factor Authentication | 자주 참조 tooas hello "전체" 버전을 Azure Multi-factor Authentication hello 다양 한 기능을 제공합니다. 추가 구성 옵션을 통해 hello 제공 [Azure 클래식 포털](https://manage.windowsazure.com), 고급 보고 및 다양 한 온-프레미스에 대 한 지원 및 클라우드 응용 프로그램입니다. Azure Multi-factor Authentication Azure Active Directory Premium (P1 및 P2 계획) 및 Enterprise Mobility + 보안 (E3 및 E5 계획)에 포함 되 고 수 중 하나를 배포 [hello 클라우드 또는 온-프레미스](multi-factor-authentication-get-started.md)합니다. |

## <a name="feature-comparison-of-versions"></a>버전 기능 비교
hello 다음 표에서 hello에서 사용할 수 있는 hello 기능 목록은 다양 한 버전의 Azure Multi-factor Authentication.

> [!NOTE]
> 이 비교 표는 각 버전의 Multi-factor Authentication의 일부인 hello 기능에 설명 합니다. Hello 전체 Azure Multi-factor Authentication 서비스를 사용 하는 경우 일부 기능 하지 못할 사용 하는지에 따라 [MFA 또는 hello 클라우드에서 MFA 온-프레미스](multi-factor-authentication-get-started.md)합니다.


| 기능 | Office 365용 Multi-Factor Authentication | Azure 관리자를 위한 Multi-Factor Authentication | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| MFA를 사용하여 관리자 계정 보호 |● |● (전역 관리자 계정에만 해당) |● |
| 두 번째 단계로 모바일 앱 |● |● |● |
| 두 번째 단계로 전화 통화 |● |● |● |
| 두 번째 단계로 SMS |● |● |● |
| MFA를 지원하지 않는 클라이언트에 대한 앱 암호 |● |● |● |
| 확인 방법에 대한 관리자 제어 |● |● |● |
| PIN 모드 | | |● |
| 사기 행위 경고 | | |● |
| MFA 보고서 | | |● |
| 일회성 바이패스 | | |● |
| 전화 통화에 대한 사용자 지정 인사말 | | |● |
| 전화 통화에 대한 사용자 지정 발신자 번호 | | |● |
| 신뢰할 수 있는 IP | | |● |
| 신뢰할 수 있는 장치에 대한 MFA 기억 |● |● |● |
| MFA SDK | | |● (Multi-factor Auth 공급자 및 전체 Azure 구독 필요) |
| 온-프레미스 응용 프로그램에 대한 MFA | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>어떻게 tooget Azure Multi-factor Authentication
Azure Multi-factor Authentication에서 제공 하는 hello 전체 기능을 원하는 경우 일부의 옵션이 있습니다.

### <a name="option-1---mfa-licenses"></a>옵션 1 - MFA 라이선스

Azure Multi-factor Authentication 라이선스를 구입 하 고 Azure Active Directory에서 tooyour 사용자를 할당 합니다. 

이 옵션을 사용 하면 또한 라이선스를 갖지 않는 일부 사용자에 대 한 tooprovide 2 단계 인증을 해야 하는 경우에 Azure Multi-factor Authentication 공급자를 만들어야 합니다. 그렇지 않으면 두 번 청구될 수 있습니다.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>옵션 2 - MFA를 포함하는 번들 라이선스

Azure Active Directory Premium (P1 또는 p 2) 또는 Enterprise Mobility + 보안 (E3 또는 e 5)와 같은 Azure Multi-factor Authentication을 포함 하 고 Azure Active Directory에서 tooyour 사용자를 할당 하는 라이선스를 구입 합니다. 

이 옵션을 사용 하면 또한 라이선스를 갖지 않는 일부 사용자에 대 한 tooprovide 2 단계 인증을 해야 하는 경우에 Azure Multi-factor Authentication 공급자를 만들어야 합니다. 그렇지 않으면 두 번 청구될 수 있습니다. 

### <a name="option-3---mfa-consumption-based-model"></a>옵션 3 - MFA 사용량 기반 모델

Azure 구독 내에서 Azure Multi-Factor Authentication 공급자를 만듭니다. Azure MFA 공급자는 모든 다른 Azure 리소스처럼 기업계약, Azure 약정 금액 또는 신용 카드에 대해 청구되는 Azure 리소스입니다. 이러한 공급자는 전체 Azure 구독에만 만들 수 있으며 $0 지출 한도를 포함하는 Azure 구독으로 제한되지 않습니다. 제한된 구독은 옵션 1 및 2처럼 라이선스를 활성화하는 경우 만들어집니다. 

Azure Multi-Factor Authentication 제공자를 사용하는 경우 Azure 구독을 통해 청구되는 두 가지 사용 모델을 사용할 수 있습니다.  

1. **사용자 당** -고정된 된 수의 정기적으로 인증을 요구 하는 직원에 대 한 2 단계 인증 tooenable를 원하는 엔터프라이즈에 대 한 합니다. 사용자별으로 청구 hello Azure AD 테 넌 트 및/또는 Azure MFA 서버에서 MFA에 대해 사용할 수 있는 사용자 수를 기반으로 합니다. 두 Azure ad에서 MFA에 대 한 사용자를 활성화 하는 경우 및 Azure MFA 서버를 도메인 동기화 (Azure AD Connect)를 사용 하는 힙이고 hello 대규모 집합이 사용자를 계산 합니다. 도메인 동기화를 활성화 하지 않으면 다음 Azure ad에서 MFA에 대해 사용할 수 있는 모든 사용자의 hello 합계를 계산 하는 경우 및 Azure MFA 서버입니다. 청구는 매일 계산 하 고 보고 toohello 상거래 시스템입니다. 

  > [!NOTE]
  > 대금 청구 예1: 오늘 MFA에 대해 5,000명의 사용자가 활성화되었습니다. hello MFA 시스템 해당 날짜에 대해 31, 및 보고서 161.29 사용자가 해당 숫자를 나눕니다. 내일 hello MFA 시스템 161.77 사용자를 해당 날짜에 대해 보고 되므로 15 더 많은 사용자를 사용 합니다. Hello 청구 주기가 끝날 때 hello, Azure 구독에 대 한 청구 하는 사용자의 총 hello tooaround 5, 000 추가 합니다. 
  >
  > 청구 예 2: hello 차이를 사용자별 Azure MFA 공급자 toomake 갖도록 라이선스를 갖고 있는 사용자 및 사용자가 없는, 혼합 되어 있습니다. 테넌트에는 4,500개의 Enterprise Mobility + Security 라이선스가 있지만 MFA에 대해 5,000명의 사용자가 활성화되어 있습니다. Azure 구독에는 500명의 사용자에 대해 대금이 청구되고 매일 16.13명의 사용자료 계산 및 보고됩니다. 

2. **인증 단위** -대규모 사용자 그룹에 가끔씩만 인증에 대 한 tooenable 2 단계 인증을 원하는 엔터프라이즈에 대 한 합니다. 요금 청구는 hello hello 이러한 확인 작업의 성공 또는 거부 여부에 관계 없이 Azure MFA 클라우드 서비스에서 수신 하는 2 단계 확인 요청 수를 기반으로 합니다. 이 청구 팩 10 인증에 Azure 사용 내역에 표시 되 고 보고 된 toohello 상거래 시스템 매일 됩니다. 

  > [!NOTE]
  > 청구 예제 3: hello Azure MFA 서비스 3,105 2 단계 확인 요청을 수신 하는 오늘 합니다. Azure 구독에는 310.5개 인증 팩에 대한 요금이 청구됩니다. 

것이 중요 한 toonote에 Azure MFA 라이선스 있을 수 있지만 사용 빈도 기반 구성을 사용에 대 한 결제 합니까 한 합니다. 인증당 Azure MFA 공급자를 설정했다면 라이선스가 있는 사용자가 수행했어도 2단계 인증 요청마다 요금이 청구됩니다. 연결 된 Azure AD 테 넌 트 tooyour 없는 도메인에서 사용자 마다 Azure MFA 공급자를 설정 하면 사용자가 Azure AD에 라이선스를 보유 하는 경우에 활성화 된 사용자별 청구 됩니다. 

## <a name="next-steps"></a>다음 단계

- 가격 책정에 대한 자세한 내용은 [Azure MFA 가격 책정](https://azure.microsoft.com/pricing/details/multi-factor-authentication/)을 참조하세요.

- 선택 여부 toodeploy Azure MFA [hello 클라우드 또는 온-프레미스](multi-factor-authentication-get-started.md)
