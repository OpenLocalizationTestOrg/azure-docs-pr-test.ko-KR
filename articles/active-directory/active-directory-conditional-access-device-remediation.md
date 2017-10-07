---
title: "aaaYou에서에서 가져올 수 없는 있습니다 hello에 Windows 장치에서 Azure 포털 | Microsoft Docs"
description: "고정할 수 없는 위치에 대해 알아봅니다 여기에서에서 이릅니다 get 접근자와 어떤를 확인 하는 tooavoid이 대화이 상자를 실행 합니다."
services: active-directory
keywords: "장치 기반 조건부 액세스, 장치 등록, 장치 등록 사용, 장치 등록 및 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>Windows 장치 상에서 '여기에서 가져올 수 없습니다'

예를 들어 조직의 SharePoint Online 인트라넷에 액세스하려 할 때 *여기에서 가져올 수 없습니다*라는 메시지가 있는 페이지가 표시될 수 있습니다. 관리자가 특정 조건에 대 한 액세스 tooyour 조직 리소스를 방지 하는 조건부 액세스 정책을 구성 때문에이 페이지를 표시 됩니다. 필요한 toocontact 기술 지원팀 또는 사용자 관리자 tooget이이 문제를 해결할 수 있습니다, 하는 동안 몇 가지 방법으로, 직접 아웃 먼저 시도할 수 있습니다.

사용 하는 경우는 **Windows** 장치를 다음 hello 확인 해야 합니다.

- 지원되는 브라우저를 사용하고 있는가?

- 장치에서 지원되는 Windows 버전을 실행하고 있는가?

- 장치가 규격을 준수하는가?






## <a name="supported-browser"></a>지원되는 브라우저

관리자가 조건부 액세스 정책을 구성한 경우, 지원되는 브라우저를 사용하여 조직의 리소스를 액세스할 수 있습니다. Windows 장치에서는 **Internet Explorer** 및 **Edge**만 지원됩니다.

Hello 오류 페이지 hello 세부 정보 섹션을 보면 tooan 지원 되지 않는 브라우저 인해는 리소스를 액세스할 수 있는지 여부를 쉽게 식별할 수 있습니다.

![지원되지 않은 브라우저에 대한 "여기에서 가져올 수 없습니다" 메시지](./media/active-directory-conditional-access-device-remediation/02.png "시나리오")

hello만 재구성 toouse hello 응용 프로그램이 지 원하는 장치 플랫폼에 대 한 브라우저입니다. 지원되는 브라우저의 전체 목록은 [지원되는 브라우저](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies)를 참조하세요.  


## <a name="supported-versions-of-windows"></a>지원되는 Windows 버전

hello 다음 장치에서 Windows 운영 체제 hello에 대 한 적용 되어야 합니다. 

- 장치에서 Windows 데스크톱 운영 체제를 실행 하는 경우 toobe Windows 7 이상이 필요 합니다.
- 장치에서 Windows server 운영 체제를 실행 하는 경우 필요한 toobe Windows Server 2008 R2 이상. 


## <a name="compliant-device"></a>규정 준수 장치

관리자가 규격 장치 에서만에서 액세스 tooyour 조직 리소스를 허용 하는 조건부 액세스 정책을 구성 했을 수 있습니다. toobe 규격 장치에 조인 된 tooyour 중 하나 여야 합니다. 온-프레미스 Active Directory 또는 Azure Active Directory tooyour 조인 합니다.

Hello 오류 페이지의 hello 세부 정보 섹션을 검색 하 여 호환 되지 않는 tooa 장치 인해는 리소스를 액세스할 수 있는지 여부를 쉽게 식별할 수 있습니다.
 
![등록되지 않은 장치에 대한 "여기에서 가져올 수 없습니다" 메시지](./media/active-directory-conditional-access-device-remediation/01.png "시나리오")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>가입 된 장치 tooan 온-프레미스 Active Directory 인가요?

**장치에 가입 되어 있으면 tooan 온-프레미스 Active Directory 조직에서:**

1. 작업 계정 (Active Directory 계정)를 사용 하 여 tooWindows에 로그인 하 고 있는지 확인 합니다.
2. 가상 사설망 (VPN) 또는 DirectAccess를 통해 tooyour 회사 네트워크에 연결 합니다.
3. 연결 된 후 hello Windows 로고 키 + L hello 키 toolock 키를 눌러 Windows 세션입니다.
4. 작업 계정 자격 증명을 입력하여 Windows 세션의 잠금을 해제합니다.
5. 잠시 기다렸다가 tooaccess hello 응용 프로그램 또는 서비스 후 다시 시도 하십시오.
6. 표시 되 면 hello 동일한 페이지에서 hello **자세히** 링크를 선택한 다음 hello 세부 정보를 사용 하 여 관리자에 문의 하십시오.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>조인 되지 장치 tooan 온-프레미스 Active Directory 인가요?

장치에 가입 되지 않은 경우 tooan 온-프레미스 Active Directory 및 Windows 10을 실행, 두 가지 옵션이 있습니다.

* Azure AD 조인을 실행합니다.
* 작업을 추가 또는 학교 계정 tooWindows

이러한 옵션의 차이점에 대한 자세한 내용은 [작업 공간에서 Windows 10 장치 사용](active-directory-azureadjoin-windows10-devices.md)을 참조하세요.  
장치가

- Tooyour 조직에 속한 Azure AD Join을 실행 해야 합니다.
- 개인 장치 또는 Windows phone 작업 추가 또는 학교 계정 tooWindows 해야 



#### <a name="azure-ad-join-on-windows-10"></a>Windows 10에서 Azure AD 조인

hello 단계 toojoin 장치 tooAzure AD 사용자는 연결의 Windows 10을 실행 하는 hello 버전. hello를 실행 중인 Windows 10 운영 체제의 toodetermine hello 버전 **winver** 명령: 

![Windows 버전](./media/active-directory-conditional-access-device-remediation/03.png )


**Windows 10 1주년 업데이트(버전 1607):**

1. 열기 hello **설정을** 응용 프로그램입니다.
2. **계정** > **회사 또는 학교에 액세스**를 클릭합니다.
3. **Connect**를 클릭합니다.
4. 클릭 **이 장치 tooAzure AD Join**합니다.
5. Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.
6. 로그아웃한 후 작업 계정으로 로그인합니다.
7. Tooaccess hello 응용 프로그램을 다시 시도 합니다.

**Windows 10 2015년 11월 업데이트(버전 1511):**

1. 열기 hello **설정을** 응용 프로그램입니다.
2. **시스템** > **정보**를 클릭합니다.
3. **Azure AD 조인**을 클릭합니다.
4. Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.
5. 로그아웃한 후 작업 계정(Azure AD 계정)으로 로그인합니다.
6. Tooaccess hello 응용 프로그램을 다시 시도 합니다.


#### <a name="workplace-join-on-windows-81"></a>Windows 8.1에서 작업 공간 연결

장치가 도메인에 가입 되지 않은 작업 공간 연결 toodo, Windows 8.1 실행 및 Microsoft Intune에 등록을 하는 경우 다음 단계 hello지 않습니다.

1. **PC 설정**을 엽니다.
2. **네트워크** > **작업 공간**을 클릭합니다.
3. **조인**을 클릭합니다.
4. Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.
5. **켜기**를 클릭합니다.
6. Tooaccess hello 응용 프로그램을 다시 시도 합니다.



#### <a name="add-your-work-or-school-account-toowindows"></a>작업을 추가 또는 학교 계정 tooWindows 


**Windows 10 1주년 업데이트(버전 1607):**

1. 열기 hello **설정을** 응용 프로그램입니다.
2. **계정** > **회사 또는 학교에 액세스**를 클릭합니다.
3. **Connect**를 클릭합니다.
4. Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.
5. Tooaccess hello 응용 프로그램을 다시 시도 합니다.


**Windows 10 2015년 11월 업데이트(버전 1511):**

1. 열기 hello **설정을** 응용 프로그램입니다.
2. **계정** > **사용자 계정**을 클릭합니다.
3. **회사 또는 학교 계정 추가**를 클릭합니다.
4. Tooyour 조직 인증, 메시지가 표시 되 고 표시 되는 hello 단계를 수행 하는 경우 다단계 인증을 제공 합니다.
5. Tooaccess hello 응용 프로그램을 다시 시도 합니다.





## <a name="next-steps"></a>다음 단계
[Azure Active Directory 조건부 액세스](active-directory-conditional-access.md)

