---
title: "Azure Active Directory 장치 기반 조건부 액세스 정책이 aaaConfigure | Microsoft Docs"
description: "어떻게 tooconfigure Azure Active Directory 장치 기반 조건부 액세스 정책에 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc5923b8ccee4335442c17ef63b2ee6f098e104e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-active-directory-device-based-conditional-access-policies"></a>Azure Active Directory 장치 기반 조건부 액세스 정책 구성

[Azure AD(Azure Active Directory) 조건부 액세스](active-directory-conditional-access-azure-portal.md)를 사용하여 권한 있는 사용자가 리소스를 액세스하는 방법을 미세 조정할 수 있습니다. 예를 들어 hello toocertain 리소스 tootrusted 장치에 액세스를 제한 합니다. 신뢰할 수 있는 장치를 요구하는 조건부 액세스 정책을 장치 기반 조건부 액세스 정책이라고도 합니다.

이 항목에서는 Azure AD에 연결 된 응용 프로그램에 대 한 정책 tooconfigure 장치 기반 조건부 액세스 하는 방법에 대 한 정보를 제공 합니다. 


## <a name="before-you-begin"></a>시작하기 전에

장치 기반 조건부 액세스는 **Azure AD 조건부 액세스**와 **Azure AD 장치 관리**를 함께 연결합니다. 가 아닌 이러한 영역 중 하나에 대해 잘 알고 아직 hello 이벤트에 대 한 다음 항목을 읽어야 합니다.

- **[Azure Active Directory의 조건부 액세스](active-directory-conditional-access-azure-portal.md)**  -이 항목에서는 액세스 하 고 관련된 용어를 hello 조건부의 개념적인 개요를 제공 합니다.

- **[Azure Active Directory에서 소개 toodevice 관리](device-management-introduction.md)**  -이 항목에서는 간략히 hello의 다양 한 옵션이 있는 Azure AD 사용 하 여 tooconnect 장치입니다. 


## <a name="trusted-devices"></a>신뢰할 수 있는 장치

먼저 모바일, 클라우드 우선 세계에서 Azure Active Directory single sign on toodevices, 앱 및 서비스를 어디에서 든 수 있습니다. 특정 toohello 적절 한 사용자 액세스를 부여, 사용자 환경에서 리소스 충분 한 아닐 수 있습니다. 또한 toohello 적절 한 사용자를도 필요할 수 신뢰할 수 있는 장치 toobe tooaccess 리소스를 사용 합니다. 사용자 환경에서 정의할 수 있습니다에 기반 하는 신뢰할 수 있는 장치는 다음 구성 요소 hello:

- hello [장치 플랫폼](active-directory-conditional-access-azure-portal.md#device-platforms) 장치에서
- 장치는 규정을 준수하는지 여부
- 장치가 도메인에 가입되어 있는지 여부 

hello [장치 플랫폼](active-directory-conditional-access-azure-portal.md#device-platforms) 장치에서 실행 되는 hello 운영 체제의 특징은 합니다. 장치 기반 조건부 액세스 정책에서 액세스 toocertain 리소스 toospecific 장치 플랫폼을 제한할 수 있습니다.



장치 기반 조건부 액세스 정책에서 신뢰할 수 있는 장치 toobe 준수 상태로 표시 됨을 요구할 수 있습니다.

![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/24.png)

장치는 hello 디렉터리 내에서 호환으로 표시할 수 있습니다.

- Intune 
- Azure AD와 통합되는 타사 모바일 장치 관리 시스템  

만 있는 장치를 연결 된 tooAzure AD 규격으로 표시할 수 있습니다. 장치 tooAzure Active Directory tooconnect hello 다음 옵션을 사용할 수 있습니다. 

- Azure AD 등록
- Azure AD 가입
- 하이브리드 Azure AD 가입

    ![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/26.png)

온-프레미스 AD (Active Directory) 공간을 설정한 경우에 연결 된 tooAzure AD 하지만 신뢰할 수 있는 조인된 tooyour AD toobe 되지 않는 장치를 고려할 수 있습니다.

![클라우드 앱](./media/active-directory-conditional-access-policy-connected-applications/25.png)


## <a name="next-steps"></a>다음 단계

장치 기반 조건부 액세스 정책이 사용자 환경에서를 구성 하기 전에 hello 살펴보면 취해야 [Azure Active Directory의 조건부 액세스에 대 한 유용한](active-directory-conditional-access-best-practices.md)합니다.

