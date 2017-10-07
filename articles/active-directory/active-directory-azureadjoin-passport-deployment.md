---
title: "aaaEnable Microsoft 비즈니스용 Windows Hello 조직의 | Microsoft Docs"
description: "조직에 배포 지침 tooenable Microsoft Passport 합니다."
services: active-directory
documentationcenter: 
keywords: "Microsoft Passport 구성, 비즈니스용 Microsoft Windows Hello 배포"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a>조직에서 비즈니스용 Microsoft Windows Hello 사용
후 [Azure Active Directory와 Windows 10 도메인에 가입 된 장치에 연결](active-directory-azureadjoin-devices-group-policy.md), 조직에서 비즈니스에 대 한 Microsoft Windows Hello tooenable 다음 hello지 않습니다.

1. System Center Configuration Manager 배포  
2. 정책 설정 구성
3. Hello 인증서 프로필 구성  

## <a name="deploy-system-center-configuration-manager"></a>System Center Configuration Manager 배포
비즈니스 키에 대 한 Windows Hello를 기반으로 toodeploy 사용자 인증서를 다음 hello 필요 합니다.

* **System Center Configuration Manager 현재 분기** -1606 이상 더 좋은 tooinstall 버전이 필요 합니다. 자세한 내용은 참조 hello [System Center Configuration Manager에 대 한 설명서](https://technet.microsoft.com/library/mt346023.aspx) 및 [System Center Configuration Manager 팀 블로그](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)합니다.
* **공개 키 인프라 (PKI)** -tooenable Microsoft Windows Hello 사용자 인증서를 사용 하 여 비즈니스에 대 한 위치에서 PKI를 있어야 합니다. 하나를 갖고 있지 않거나 toouse 원하는 경우 Windows Server 2016이 설치 되어 10551 (또는 그 이상)를 작성 하는 새 도메인 컨트롤러를 배포할 수 사용자 인증서에 대 한 것입니다. 다음과 같이 hello 너무[기존 도메인에서 복제 도메인 컨트롤러를 설치](https://technet.microsoft.com/library/jj574134.aspx) 또는 너무[새 환경을 만드는 경우 새 Active Directory 포리스트를 설치](https://technet.microsoft.com/library/jj574166)합니다. (Iso hello에 다운로드할 수 있는 [Signiant 미디어 교환이](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)

## <a name="configure-policy-settings"></a>정책 설정 구성
Microsoft Windows Hello tooconfigure hello 비즈니스 정책 설정에 대 한 두 가지 옵션이 있습니다.

* Active Directory에서 그룹 정책 
* System Center Configuration Manager hello 

사용 하 여 그룹 정책 Active Directory에는 비즈니스 정책 설정에 대 한 Microsoft Windows Hello 메서드 tooconfigure 권장 hello입니다. 

System Center Configuration Manager를 사용 하는 것이 인증서를 사용할 때 그 toodeploy hello 기본 방법입니다. 이 시나리오의 경우

* 호환 hello 최신 배포 시나리오
* Windows 10 버전 1607 이상 hello 클라이언트 쪽에서 필요합니다.

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a>Active Directory에서 그룹 정책을 통해 비즈니스용 Microsoft Windows Hello 구성
**단계**:

1. 서버 관리자를 열고 너무 이동**도구** > **그룹 정책 관리**합니다.
2. 그룹 정책 관리에서 해당 하는 Azure AD Join tooenable 원하는 toohello 도메인은 toohello 도메인 노드를 이동 합니다.
3. **그룹 정책 개체**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 선택합니다. 예를 들어 그룹 정책 개체에 이름을 지정하고 비즈니스용 Windows Hello를 사용하도록 설정합니다. **확인**을 클릭합니다.
4. 새 그룹 정책 개체를 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.
5. 너무 이동**컴퓨터 구성** > **정책** > **관리 템플릿** > **Windows 구성 요소** > **비즈니스용 Windows Hello**합니다.
6. **비즈니스용 Windows Hello 사용**을 마우스 오른쪽 단추로 클릭한 다음 **편집**을 선택합니다.
7. 선택 hello **Enabled** 옵션 단추를 선택한 다음 클릭 **적용**합니다. **확인**을 클릭합니다.
8. 이제 hello 그룹 정책 개체 tooa 선택한 위치에 연결할 수 있습니다. tooenable이이 정책은 모든 링크 hello 그룹 정책 toohello 도메인은 조직에서 hello 도메인에 가입 된 Windows 10 장치에 대 한 합니다. 예:
   * Windows 10 도메인에 가입된 컴퓨터가 배치될 Active Directory의 특정 OU(조직 구성 단위)입니다.
   * Azure AD에 자동 등록될 Windows 10 도메인에 가입된 컴퓨터를 포함하는 특정 보안 그룹입니다.

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a>System Center Configuration Manager를 사용하여 비즈니스용 Windows Hello 구성
**단계**:

1. 열기 hello **System Center Configuration Manager**를 이동한 후 너무**자산 및 호환성 > 규정 준수 설정 > 회사 리소스 액세스 > 비즈니스 프로필에 대 한 Windows Hello**합니다.
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. 도구 모음의 hello hello 위쪽에 클릭 **프로필 비즈니스용 Windows Hello 만들**합니다.
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. Hello에 **일반** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    a. Hello에 **이름** 텍스트 상자, 예를 들어 프로필에 대 한 이름 입력 **내 WHfB 프로필**합니다.
   
    b. **다음**을 누릅니다.
4. Hello에 **지원 되는 플랫폼** 대화 상자에서 비즈니스 프로필에 대 한이 Windows Hello로 프로 비전 됩니다을 클릭 한 다음 선택 hello 플랫폼 **다음**합니다.
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. Hello에 **설정을** 대화 상자에서 hello 다음 단계를 수행 합니다.
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    a. **비즈니스용 Windows Hello 구성**에서 **사용**을 선택합니다.
   
    b. **TPM(신뢰할 수 있는 플랫폼 모듈) 사용**에서 **필수**를 선택합니다. 
   
    c. **인증 방법**에서 **인증서 기반**을 선택합니다.
   
    d. **다음**을 누릅니다.
6. Hello에 **요약** 대화 상자를 클릭 하 여 **다음**합니다.
7. Hello에 **완료** 대화 상자를 클릭 하 여 **닫기**합니다.
8. 도구 모음의 hello hello 위쪽에 클릭 **배포**합니다.
   
    ![비즈니스용 Windows Hello 구성](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a>Hello 인증서 프로필 구성
인증서 기반 인증을 온-프레미스 인증을 위해 사용 하는 경우 tooconfigure 필요 하 고 인증서 프로필을 배포 합니다. 이 작업을 위해서는 tooset NDES 서버 및 hello System Center Configuration Manager에서에서 인증서 등록 지점 사이트 역할을 합니다. 자세한 내용은 참조 hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx)합니다.

1. 열기 hello **System Center Configuration Manager**를 이동한 후 너무**자산 및 호환성 > 규정 준수 설정 > 회사 리소스 액세스 > 인증서 프로필**합니다.
2. 스마트 카드 로그인 EKU(확장 키 사용)가 있는 템플릿을 선택합니다.

Hello에 **SCEP 등록** 페이지 toochoose hello 인증서 프로필의 필요한 **설치, 그렇지 않으면 작업 실패에 대 한 tooPassport** hello로 **키 저장소 공급자**합니다.

## <a name="next-steps"></a>다음 단계
* [Hello 엔터프라이즈용 Windows 10: 작업에 대 한 방법으로 toouse 장치](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join을 통해 기능 10 tooWindows 장치 클라우드를 확장합니다.](active-directory-azureadjoin-user-upgrade.md)
* [Microsoft Passport를 통해 암호 없이 ID 인증](active-directory-azureadjoin-passport.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용에 대 한 AD 도메인에 가입 된 장치 tooAzure 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

