---
title: "Windows 10 용 aaaConnect 도메인에 가입 된 장치 tooAzure AD 환경을 | Microsoft Docs"
description: "관리자가 그룹 정책 tooenable 장치 toobe toohello 도메인에 가입 된 엔터프라이즈 네트워크를 구성할 수는 방법에 대해 설명 합니다."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결
도메인 가입 hello 전통적인 방법 조직 마지막 15 년 등 hello에 대 한 작업에 대 한 장치 연결입니다. Windows Server Active Directory (Active Directory) 작업을 사용 하 여 사용자가 toosign tootheir 장치에서 활성화 있는 또는 학교 계정 및 허용 된 IT toofully 이러한 장치를 관리 합니다. 조직은 일반적으로 tooprovision 장치 toousers 메서드가 imaging에 의존 하 고 일반적으로 toomanage SCCM System Center Configuration Manager () 또는 그룹 정책을 사용 하 여 해당 합니다.


도메인 가입 Windows 10의 이점 장치 tooAzure Active Directory (Azure AD)에 연결한 후에 수행 하는 hello로 제공 합니다.

* Single sign on (SSO) tooAzure AD 리소스 어디에서 든
* 작업을 사용 하 여 toohello enterprise Windows 스토어에 액세스 하거나 학교 계정 (Microsoft 계정이 필요)
* 회사 또는 학교 계정을 사용하여 장치 간 사용자 설정의 엔터프라이즈 규격 로밍(Microsoft 계정 필요 없음)
* 비즈니스용 Windows Hello 및 Windows Hello를 사용하는 회사 또는 학교 계정에 대한 강력한 인증 및 손쉬운 로그인
* 기능 toorestrict 조직 장치 그룹 정책 설정을 준수 하는 toodevices만 액세스

## <a name="prerequisites"></a>필수 조건
도메인 가입 계속 toobe 유용 합니다. 그러나 tooget hello Azure AD 혜택 sso를 사용 하 여 설정의 로밍 직장 또는 학교 계정을, 및 tooWindows 저장소 작업을 사용 하 여 액세스할 이나 학교 계정을, hello를 수행 해야 합니다.

* Azure AD 구독
* Azure AD Connect tooextend hello 온-프레미스 디렉터리 tooAzure AD
* 도메인에 가입 된 장치 tooAzure tooconnect AD 설정 정책
* 장치에 Windows 10 빌드(빌드 10551 또는 이후 버전)

비즈니스 사용자와 Windows Hello Windows Hello tooenable 코드도 hello 다음이 필요 합니다.

- 사용자 인증서를 발급하기 위한 **PKI(공개 키 인프라)**가 있어야 합니다.

- **System Center Configuration Manager 현재 분기** -1606 이상 더 좋은 tooinstall 버전이 필요 합니다.  
자세한 내용은 다음을 참조하세요. 
    - [System Center Configuration Manager용 설명서](https://technet.microsoft.com/library/mt346023.aspx)
    - [System Center Configuration Manager 팀 블로그](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [System Center Configuration Manager의 비즈니스용 Windows Hello 설정](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

대체 toohello PKI 배포 요구 사항으로 할 수 있는 hello 다음:

* Windows Server 2016 Active Directory 도메인 서비스와 몇 가지 도메인 컨트롤러를 보유합니다.

조건부 액세스는 tooenable 없는 추가 배포와 toodomain에 가입 된 장치 액세스를 허용 하는 그룹 정책 설정을 만들 수 있습니다. hello 장치의 준수를 기반으로 toomanage 액세스 제어를 hello 다음이 필요 합니다.

* 비즈니스용 Windows Hello 시나리오에 대한 System Center Configuration Manager 현재 분기(1606 이상)

## <a name="deployment-instructions"></a>배포 지침

toodeploy에 나열 된 hello 단계를 수행 [어떻게 tooconfigure 자동 등록의 Windows 도메인에 가입 된 장치의 Azure Active Directory와](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>다음 단계
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

