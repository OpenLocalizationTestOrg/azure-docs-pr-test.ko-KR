---
title: "Azure Active Directory의 aaaIntroduction toodevice 관리 | Microsoft Docs"
description: "장치 관리의 활용 방법 tooget 제어 환경에서 리소스에 액세스 하는 hello 장치에 대해 알아봅니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Azure Active Directory의 toodevice 관리 소개

먼저 모바일, 클라우드 우선 세계에서 Azure Active Directory (Azure AD)에 single sign on toodevices, 앱 및 서비스를 어디에서 든 수 있습니다. 장치-BYOD Bring Your Own 장치 ()를 포함 하 여 hello 확산 됨에 따라와 IT 전문가 문제에 직면 두 가지 상반 되 목표:

- 있어 선택의 폭 hello 최종 사용자에 게 toobe 생산성을 아무 곳에 나 때마다
- 언제 든 지 hello 회사 자산을 보호 합니다.

장치를 통해 tooyour 회사 자산 사용자가 액세스 하 게 됩니다. tooprotect 회사 자산을 IT 관리자는 toohave 제어를 원하는 합니다. 이렇게 하면 사용자가 보안 및 규정 준수 표준을 충족 하는 장치에서 사용자 리소스에 액세스 하는 있는지 toomake 있습니다. 

장치 관리에 대 한 hello foundation 이기도 [장치 기반 조건부 액세스](active-directory-conditional-access-policy-connected-applications.md)합니다. 장치 기반 조건부 액세스를 통해 신뢰할 수 있는 장치 액세스 환경의 tooresources만를 사용할 수 있는지 확인할 수 있습니다.   

이 항목에서는 Azure Active Directory에서 장치 관리가 작동되는 방식을 설명합니다.

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>Azure AD의 hello 제어에서 사용 중인 장치 가져오기

Azure AD의 hello 제어 아래에 있는 장치 tooget 두 가지 옵션이 있습니다.

- 등록 
- 가입

**등록** 장치 tooAzure AD toomanage 있습니다는 장치 id를 사용 합니다. 장치를 등록할 때 Azure AD 장치 등록 id가 사용 되는 tooauthenticate hello 장치 경우는 사용자가 로그인 tooAzure AD 사용 하 여 hello 장치를 제공 합니다. Identity tooenable hello를 사용 하거나 장치를 비활성화할 수 있습니다.

Microsoft Intune 같은 모바일 장치 management(MDM) 솔루션을 함께 사용 하면 Azure AD의 장치 특성이 hello hello 장치에 대 한 추가 정보로 업데이트 됩니다. 이렇게 하면 사용자의 보안 및 규정 준수에 대 한 표준 장치 toomeet에서 액세스를 적용 하는 toocreate 조건부 액세스 규칙이 있습니다. Microsoft Intune에서 장치를 등록하는 방법에 대한 자세한 내용은 Intune에서 관리를 위한 장치 등록을 참조하세요.

**조인** 장치는 확장 tooregistering 장치입니다. 이 즉, 제공 장치를 등록 하 고 더하기 toothis에 hello 혜택을 모두, hello 로컬 상태는 장치에도 변경 합니다. Hello 로컬 상태를 변경 합니다. 개인 계정 대신는 조직 회사 또는 학교 계정을 사용 하 여 사용자가 toosign-tooa 장치가 있습니다.

## <a name="azure-ad-registered-devices"></a>Azure AD 등록 장치   

hello 등록 하는 Azure AD 장치 ´ ֲ ° hello에 대 한 지원 된 tooprovide **BYOD Bring Your Own 장치 ()** 시나리오입니다. 이 시나리오에서 사용자는 개인 장치를 사용하여 조직의 Azure Active Directory 제어 리소스에 액세스할 수 있습니다.  

![Azure AD 등록 장치](./media/device-management-introduction/03.png)

hello 액세스 hello 장치에서 입력 된 회사 또는 학교 계정을 기반으로 합니다.  
예를 들어, 작업 또는 학교 계정 tooa 개인용 컴퓨터, 태블릿 또는 휴대폰 Windows 10 사용자 tooadd 수 있도록 합니다.  
회사 또는 학교 계정, hello 장치는 사용자가 추가 하는 경우 Azure AD에 등록 되 고 필요에 따라 조직 구성 hello 모바일 장치 관리 (MDM) 시스템에 등록 합니다. 조직의 사용자는 작업을 추가 하거나 계정 tooa 개인 장치를 편리 하 게 학교 수 있습니다.:

- Hello에 대 한 작업 응용 프로그램에 액세스할 때 처음
- Hello를 통해 수동으로 **설정을** hello 경우 Windows 10의 메뉴 

Windows 10, iOS, Android 및 macOS용 Azure AD 등록 장치를 구성할 수 있습니다.

## <a name="azure-ad-joined-devices"></a>Azure AD 가입 장치

Azure AD 조인 장치의 hello 목표는 toosimplify를입니다.

- 회사 소유 장치의 Windows 배포 
- 액세스 tooorganizational 앱 및 모든 Windows 장치에서 리소스

![Azure AD 등록 장치](./media/device-management-introduction/02.png)


이러한 목표는 Azure AD에 hello 제어 작업 소유 장치를 가져오기 위한 셀프 서비스 환경과 사용자가 제공 하 여 수행 됩니다.  
**Azure AD 가입**은 클라우드 우선/클라우드 전용 조직을 위해 고안되었습니다. 일반적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 소규모 및 중간 규모 비즈니스가 해당됩니다. 

Azure AD 조인 장치의 구현 이점을 다음 hello로 제공 합니다.

- **Single Sign-on (SSO)** tooyour Azure SaaS 앱 및 서비스를 관리 합니다. 사용자가 회사 리소스에 액세스할 때 추가 인증 메시지가 표시되지 않습니다. hello SSO 기능은 짝수 없는 시기 연결된 toohello 도메인 네트워크를 사용할 수 있습니다.

- 가입 장치 간 사용자 설정의 **엔터프라이즈 규정 준수 로밍**. 사용자가 장치에서 tooconnect Microsoft 계정 (예: Hotmail) toosee 설정을 필요 하지 않습니다.

- **액세스 tooWindows Store for Business** AD 계정을 사용 하 여 합니다. 사용자가 hello 조직에서 미리 선택 된 응용 프로그램의 인벤토리에서 선택할 수 있습니다.

- **Windows Hello** toowork 리소스에 안전 하 고 편리한 액세스에 대 한 지원.

- **액세스 제한** 규정 준수 정책을 충족 하는 장치만에서 tooapps 합니다.

Azure AD 가입은 기본적으로 온-프레미스 Windows Server Active Directory 인프라가 없는 조직을 위해 고안되었으나, 다음과 같은 시나리오에서 확실히 사용할 수 있습니다.

- 태블릿 및 휴대폰 제어와 같은 모바일 장치를 tooget 해야 할 경우 예를 들어는 온-프레미스 도메인 가입을 사용할 수 없습니다.

- 사용자는 주로 tooaccess Office 365 또는 Azure AD와 통합 된 SaaS 응용 프로그램에 있어야 합니다.

- Active Directory에 대신 Azure AD에 toomanage 사용자 그룹을 원하는합니다. 이 적용할 수, 예를 들어 tooseasonal 직원, 하청 업체 또는 학생 합니다.

- 제한 된 온-프레미스 인프라와 원거리 지사 사무실의 조인 기능 tooworkers를 tooprovide 사용 하는 것이 좋습니다.

Windows 10 장치에 대한 Azure AD 가입 장치를 구성할 수 있습니다.


## <a name="hybrid-azure-ad-joined-devices"></a>하이브리드 Azure AD 가입 장치

10 년 이상,에 대 한 대부분의 조직에서는 hello 도메인 가입 tootheir 온-프레미스 Active Directory tooenable 사용:

- IT 부서 toomanage 작업 소유 장치를 중앙 위치에서 합니다.

- 해당 Active Directory를 사용 하 여 tootheir 장치에서 사용자가 toosign 직장 이나 학교 계정을 합니다. 

일반적으로 조직에 온-프레미스 공간 이미징 메서드 tooprovision 장치에 의존 하 고 자주 사용 **SCCM System Center Configuration Manager ()** 또는 **그룹 정책 (GP)** toomanage 해당 합니다.

사용자 환경에 온-프레미스 AD 사용 공간을 Azure Active Directory에서 제공 하는 hello 기능에서 혜택을 하려면 또한, 하이브리드 Azure AD 조인 장치의 구현할 수 있습니다. 둘 다 있는 장치, 조인 된 tooyour 온-프레미스 Active Directory와 Azure Active Directory 합니다.

![Azure AD 등록 장치](./media/device-management-introduction/01.png)


다음과 같은 경우에 Azure AD 하이브리드 가입 장치를 사용해야 합니다.

- NTLM을 사용 하는 Win32 앱 배포 toothese 장치가 / Kerberos입니다.

- GP 또는 SCCM 필요한 / DCM toomanage 장치입니다.

- 직원에 게 toocontinue toouse 이미징 솔루션 tooconfigure 장치 원하는합니다.

Windows 10 및 하위 수준 장치(예: Windows 8 및 Windows 7)에 대한 하이브리드 Azure AD 가입 장치를 구성할 수 있습니다.

## <a name="summary"></a>요약

Azure AD의 장치 관리를 사용하면 다음과 같은 작업을 수행할 수 있습니다. 

- Azure AD의 hello 제어에서 사용 중인 장치를 가져와 hello 과정을 단순화

- 사용자가 쉽게 toouse 액세스 tooyour 조직의 클라우드 기반 리소스 제공

thumb의 규칙으로 인해 다음을 사용해야 합니다.

- 개인 장치를 위한 Azure AD 등록 장치

- Azure AD에 가입 하지 않은 장치 tooan에 가입 된 장치 온-프레미스 AD 

- Azure AD 하이브리드 가입 하는 장치 tooan에 가입 된 장치 온-프레미스 AD     




## <a name="next-steps"></a>다음 단계

- tooget toomanage 장치에 Azure 포털에서 참조 hello 하는 방법에 대해 간략하게 [hello Azure 포털을 사용 하 여 장치를 관리 합니다.](device-management-azure-portal.md)

- 장치 기반 조건부 액세스에 대해 자세히 toolearn 참조 [Azure Active Directory 장치 기반 조건부 액세스 정책 구성](active-directory-conditional-access-policy-connected-applications.md)합니다.

- toosetup 하이브리드 가입 하는 Azure AD 장치 참조 [tooconfigure 하이브리드 Azure Active Directory에 가입 하는 장치](device-management-hybrid-azuread-joined-devices-setup.md)합니다.


