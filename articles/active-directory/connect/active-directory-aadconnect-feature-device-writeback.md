---
title: "Azure AD Connect: 장치 쓰기 저장 사용 | Microsoft Docs"
description: "이 세부 정보를 어떻게 문서 Azure AD Connect를 사용 하 여 tooenable 장치 쓰기 저장"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: 장치 쓰기 저장 사용
> [!NOTE]
> 구독 tooAzure AD Premium 장치 쓰기 저장에 대 한 필요 합니다.
> 
> 

hello 설명서에서는 Azure AD Connect에서 tooenable hello 장치 쓰기 저장 기능 하는 방법을 설명 합니다. 장치 쓰기 저장은 hello 다음 시나리오에서에서 사용 됩니다.

* 장치 tooADFS에 따라 조건부 액세스를 사용 하도록 설정 (2012 R2 이상) 보호 된 응용 프로그램 (신뢰 당사자 트러스트).

이 방법은 보안을 강화 하 고 tooapplications에 액세스 하는 보증 tootrusted 장치에만 부여 됩니다. 조건부 액세스에 대한 자세한 내용은 [조건부 액세스로 위험 관리](../active-directory-conditional-access.md) 및 [Azure Active Directory Device Registration을 사용하여 온-프레미스 조건부 액세스 설정](../active-directory-conditional-access-automatic-device-registration-setup.md)을 참조하세요.

> [!IMPORTANT]
> <li>장치는 hello 사용자로 포리스트 동일 hello에 있어야 합니다. 장치 다시 작성 해야 tooa 단일 포리스트, 이후이 기능은 사용자의 다중 포리스트 배포를 현재 지원 하지 않습니다.</li>
> <li>Toohello 온-프레미스 Active Directory 포리스트에 하나의 장치 등록 구성 개체를 추가할 수 있습니다. 이 기능은 토폴로지 여기서 hello 온-프레미스 Active Directory에서 동기화 된 toomultiple Azure AD 디렉터리와 호환 되지 않습니다.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>1부: Azure AD Connect 설치
1. 사용자 지정 또는 Express 설정을 사용하여 Azure AD Connect를 설치합니다. 모든 사용자 및 장치 쓰기 저장을 활성화 하기 전에 동기화 그룹으로 toostart를 사용 하는 것이 좋습니다.

## <a name="part-2-prepare-active-directory"></a>2부: Active Directory 준비
장치 쓰기 저장을 사용 하기 위한 단계 tooprepare 다음 hello를 사용 합니다.

1. Azure AD Connect가 설치 되어 있는 hello 컴퓨터에서 관리자 모드에서 PowerShell을 시작 합니다.
2. Hello Active Directory PowerShell 모듈 설치 되지 않은 경우 다음 명령을 hello를 사용 하 여 설치 합니다.
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Hello Azure Active Directory PowerShell 모듈 설치 되지 않은 경우 다운로드 하 고 설치 원본 [Azure Active Directory에 대 한 Windows PowerShell 모듈 (64 비트 버전)](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다. 이 구성 요소는 hello 로그인 도우미를 Azure AD Connect와 함께 설치 되는 종속성을 갖습니다.
4. 엔터프라이즈 관리자 자격 증명으로 hello 다음 명령을 실행 하 고 PowerShell을 종료 합니다.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

엔터프라이즈 관리자 자격 증명 필요 되므로 필요한 변경 내용을 toohello 구성 네임 스페이스입니다. 도메인 관리자의 사용 권한으로는 부족합니다.

![장치 쓰기 저장 사용을 위한 Powershell](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

설명:

* 존재하지 않는 경우 CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn]에서 새 컨테이너 및 개체를 생성하고 구성합니다.
* 존재하지 않는 경우 CN=RegisteredDevices,[domain-dn]에서 새 컨테이너 및 개체를 생성하고 구성합니다. 이 컨테이너에서 장치 개체를 만듭니다.
* Active Directory의 장치를 toomanage hello Azure AD 커넥터 계정에 필요한 사용 권한을 설정합니다.
* 여러 포리스트에 Azure AD Connect 설치 하는 경우에 toorun 하나의 포리스트에 필요 합니다.

매개 변수

* DomainName: 장치 개체를 만드는 Active Directory 도메인입니다. 참고: 지정된 Active Directory 포리스트에 대한 모든 장치는 단일 도메인에 만들어집니다.
* Hello 디렉터리에 Azure AD Connect toomanage 개체에 의해 사용 될 AdConnectorAccount: Active Directory 계정입니다. Azure AD Connect 동기화 tooconnect tooAD에서 사용 하는 hello 계정입니다. Express 설정을 사용 하 여를 설치한 경우 MSOL_ 접두사로 hello 계정입니다.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>3부: Azure AD Connect에서 장치 쓰기 저장 사용
Azure AD Connect에서 tooenable 장치 쓰기 저장 프로시저를 수행 하는 hello를 사용 합니다.

1. Hello 설치 마법사를 다시 실행 합니다. 선택 **동기화 옵션을 사용자 지정** 페이지 hello 추가 작업에서 클릭 하 여 **다음**합니다.
   ![사용자 지정 설치 사용자 지정 동기화 옵션](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. Hello 선택적 기능 페이지에 장치 쓰기 저장은 더 이상 회색입니다. 경우 hello Azure AD Connect 준비 단계 완료 되지 않은 점에 유의 하십시오 hello 선택적 기능 페이지에 장치 쓰기 저장으로 비활성화 됩니다. 장치 쓰기 저장에 대 한 hello 확인란을 클릭 **다음**합니다. Hello 확인란은 여전히 사용 하지 않도록 설정 하는 경우 참조 hello [문제 해결 섹션](#the-writeback-checkbox-is-still-disabled)합니다.
   ![사용자 지정 설치 장치 쓰기 저장 선택적 기능](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. Hello 쓰기 저장 페이지에서 제공 하는 hello 도메인 hello 기본 장치 쓰기 저장 포리스트도 표시 됩니다.
   ![사용자 지정 설치 장치 쓰기 저장 대상 포리스트](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. 추가 구성 변경 없이 마법사 hello hello 설치를 완료 합니다. 필요한 경우 너무 참조[Azure AD Connect의 사용자 지정 설치 합니다.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>조건부 액세스 사용
이 시나리오에서 사용할 수 있는 자세한 지침 tooenable [Azure Active Directory Device Registration을 사용 하 여 온-프레미스 조건부 액세스 설정](../active-directory-conditional-access-automatic-device-registration-setup.md)합니다.

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>장치는 동기화 된 tooActive 디렉터리를 확인 하십시오.
장치 쓰기 저장은 이제 제대로 작동해야 합니다. 장치 개체 toobe 쓰기 저장 tooAD too3 시간까지 걸릴 수 있으므로 주의 합니다.  장치를 적절 하 게 동기화 되 고 tooverify hello 동기화 규칙을 완료 한 후 hello지 않습니다.

1. Active Directory 관리 센터를 시작합니다.
2. Hello 페더레이션된 되 고 도메인 내에서 RegisteredDevices를 확장 합니다.
   ![Active Directory 관리 센터 등록 장치](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. 현재 등록된 장치가 나열됩니다.
   ![Active Directory 관리 센터 등록 장치 목록](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>문제 해결
### <a name="hello-writeback-checkbox-is-still-disabled"></a>hello 쓰기 저장 확인란은 여전히 사용할 수 없습니다.
Hello 확인란 위의 hello 단계를 수행한 경우에 장치 쓰기 저장을 해제에 대 한 hello 하는 경우 다음 단계는 안내해 마법사 hello 상자를 사용 하기 전에 어떤 hello 설치를 통해 확인 합니다.

먼저 첫 번째로

* 하나 이상의 포리스트에 Windows Server 2012R2가 있는지 확인합니다. hello 장치 개체 유형 있어야 합니다.
* Hello 설치 마법사가 이미 실행 한 다음 변경 내용을 발견 되지 않습니다. 이 경우 hello 설치 마법사를 완료 하 고 다시 실행 합니다.
* Hello 초기화 스크립트에서 제공 하는 hello 계정 실제로 hello 올바른 사용자 hello Active Directory Connector에서 사용 되는지 확인 합니다. tooverify이를 다음이 단계를 수행 합니다.
  * Hello 시작 메뉴에서 열고 **동기화 서비스**합니다.
  * 열기 hello **커넥터** 탭 합니다.
  * Active Directory 도메인 서비스 형식과 hello 커넥터를 찾아 선택 합니다.
  * **작업** 아래에서 **속성**을 선택합니다.
  * 너무 이동**tooActive Directory 포리스트에 연결**합니다. 이 화면 일치 hello ् य ा ख toohello 스크립트에 지정 된 해당 hello 도메인과 사용자 이름을 확인 합니다.
    ![동기화 서비스 관리자의 커넥터 계정](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Active Directory의 구성 확인:

* Device Registration Service hello 위치 아래에 있는 해당 hello 확인 (CN DeviceRegistrationService, CN = 장치 등록 서비스, CN = = 장치 등록 구성, CN = Services, CN = Configuration) 구성 명명 컨텍스트 내에서.

![문제 해결, 구성 네임스페이스의 DeviceRegistrationService](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Hello 구성 네임 스페이스를 검색 하 여 구성 개체가 하나씩만 확인 합니다. 가 둘 이상의 hello 중복을 삭제 합니다.

![문제를 해결 하며, hello 중복 개체에 대 한 검색](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* Hello 장치 등록 서비스 개체에 hello 특성 게스트가 DeviceLocation 있고 값이 있는지를 확인 합니다. 조회는 hello objectType 게스트가 DeviceContainer과 함께 사용할이 위치 하 고 있는지 확인 하십시오.

![문제 해결, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![문제 해결, RegisteredDevices 개체 클래스](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Active Directory Connector 필수 사용 권한이 hello 이전 단계에서 발견 하는 hello 등록 된 장치 컨테이너에서 hello 사용 하는 hello 계정을 확인 합니다. 다음은이 컨테이너에서 hello 예상 사용 권한입니다.

![문제 해결, 컨테이너에 대한 권한 확인](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Hello Active Directory 계정에 대 한 권한이 hello CN 확인 = 장치 등록 구성, CN = Services, CN = 구성 개체입니다.

![문제 해결, 장치 등록 구성에 대한 권한 확인](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>추가 정보
* [조건부 액세스를 사용한 위험 관리](../active-directory-conditional-access.md)
* [Azure Active Directory Device Registration을 사용하여 온-프레미스 조건부 액세스 설정](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)에 대해 자세히 알아봅니다.

