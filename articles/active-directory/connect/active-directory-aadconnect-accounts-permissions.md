---
title: "Azure AD Connect: 계정 및 사용 권한 | Microsoft Docs"
description: "이 항목에는 hello 계정을 사용할 수 없으며 만들 필요한 권한을 설명 합니다."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: 계정 및 사용 권한
hello Azure AD Connect 설치 마법사는 두 개의 서로 다른 경로 제공합니다.

* 기본 설정의 경우 hello 마법사에는 더 많은 권한이 필요합니다.  이 소프트웨어는 toocreate 사용자가 않고도 쉽게 구성을 설정 하거나 사용 권한을 구성할 수 있습니다.
* 사용자 지정 설정에서 hello 마법사 하면 더 많은 선택 사항 및 옵션을 제공 합니다. 그러나 hello 올바른 권한이 사용자가 직접 tooensure이 필요한 경우도 있습니다.

## <a name="related-documentation"></a>관련 설명서
에 hello 설명서 읽지 않은 경우 [Azure Active Directory와 온-프레미스 id 통합](../active-directory-aadconnect.md), hello 다음 표에 링크가 toorelated 항목입니다.

|항목 |링크|  
| --- | --- |
|Azure AD Connect 다운로드 | [Azure AD Connect 다운로드](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Express 설정을 사용하여 설치 | [Azure AD Connect의 빠른 설치](./active-directory-aadconnect-get-started-express.md)|
|사용자 지정 설정을 사용하여 설치 | [Azure AD Connect의 사용자 지정 설치](./active-directory-aadconnect-get-started-custom.md)|
|DirSync에서 업그레이드 | [Azure AD Sync 도구(DirSync)에서 업그레이드](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|설치 후 | [Hello 설치 되었는지 확인 하 고 라이선스 할당](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Express 설정 설치
기본 설정을에서 hello 설치 마법사는 AD DS 엔터프라이즈 관리자 자격 증명을 묻습니다.  따라서 Azure AD Connect에 필요한 권한으로 온-프레미스 Active Directory를 구성할 수 있습니다. DirSync에서 업그레이드 하는 경우 hello AD DS Enterprise Admins 자격 증명이 사용 되는 tooreset hello 계정의 암호를 hello DirSync에 의해 사용 되는. 또한 Azure AD 전역 관리자 자격 증명이 필요합니다.

| 마법사 페이지 | 수집되는 자격 증명 | 필요한 사용 권한 | 용도 |
| --- | --- | --- | --- |
| 해당 없음 |Hello 설치 마법사를 실행 하는 사용자 |로컬 서버 hello 관리자 |<li>Hello로 사용 되는 hello 로컬 계정을 만들고 [엔진 서비스 계정 동기화](#azure-ad-connect-sync-service-account)합니다. |
| TooAzure AD 연결 |Azure AD 디렉터리 자격 증명 |Azure AD에서 글로벌 관리자 역할 |<li>Hello Azure AD 디렉터리에서 동기화를 사용 하도록 설정 합니다.</li>  <li>Hello 생성 [Azure AD 계정](#azure-ad-service-account) Azure AD에서 진행 중인 동기화 작업에 사용 되는 합니다.</li> |
| DS tooAD 연결 |온-프레미스 Active Directory 자격 증명 |Active Directory에 hello EA (Enterprise Admins) 그룹의 구성원 |<li>만듭니다는 [계정](#active-directory-account) 부여 권한 tooit 및 Active Directory에 있습니다. 계정을 만든이 동기화 하는 동안 사용 되는 tooread 및 쓰기 디렉터리 정보입니다.</li> |

### <a name="enterprise-admin-credentials"></a>엔터프라이즈 관리자 자격 증명
이러한 자격 증명 hello 설치 중에 사용 되 고 hello 설치가 완료 된 후에 사용 되지 않습니다. hello 엔터프라이즈 관리자, 하지 hello 도메인 관리자의 모든 도메인에서 Active Directory의 hello 권한을 설정할 수 않도록 해야 합니다.

### <a name="global-admin-credentials"></a>글로벌 관리자 자격 증명
이러한 자격 증명 hello 설치 중에 사용 되 고 hello 설치가 완료 된 후에 사용 되지 않습니다. 사용 되는 toocreate hello [Azure AD 계정](#azure-ad-service-account) 변경 tooAzure AD를 동기화 하는 데 사용 합니다. 또한 hello 계정을 Azure ad에서 sync를 기능으로 있습니다.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Hello에 대 한 사용 권한을 만든 기본 설정에 대 한 AD DS 계정
hello [계정](#active-directory-account) 읽기 및 쓰기 tooAD DS가 다음 기본 설정 하 여 만들 때 권한을 hello에 생성 합니다.

| 사용 권한 | 용도 |
| --- | --- |
| <li>디렉터리 변경 내용 복제</li><li>모든 디렉터리 변경 내용 복제 |암호 동기화 |
| 모든 속성 사용자 읽기/쓰기  |가져오기 및 Exchange 하이브리드 |
| 모든 속성 iNetOrgPerson 읽기/쓰기  |가져오기 및 Exchange 하이브리드 |
| 모든 속성 그룹 읽기/쓰기 |가져오기 및 Exchange 하이브리드 |
| 모든 속성 연락처 읽기/쓰기 |가져오기 및 Exchange 하이브리드 |
| 암호 재설정 |비밀번호 쓰기 저장을 사용하기 위한 준비 |

## <a name="custom-settings-installation"></a>사용자 지정 설정 설치
Azure AD Connect 버전 1.1.524.0 hello 사용 되는 계정 tooconnect tooActive 디렉터리를 만들 hello 옵션 toolet hello Azure AD Connect 마법사는 나중에 한 합니다.  이전 버전 hello 설치 하기 전에 hello 계정이 만들어지도록 해야 합니다. 이 계정에 부여 해야 하는 hello 사용 권한을 확인할 수 있습니다 [hello AD DS 계정 만들기](#create-the-ad-ds-account)합니다. 

| 마법사 페이지 | 수집되는 자격 증명 | 필요한 사용 권한 | 용도 |
| --- | --- | --- | --- |
| 해당 없음 |Hello 설치 마법사를 실행 하는 사용자 |<li>로컬 서버 hello 관리자</li><li>전체 SQL Server를 사용할 경우 시스템 관리자 (SA) SQL에서 hello 사용자에 게 이어야 합니다.</li> |기본적으로 hello로 사용 되는 hello 로컬 계정을 만듭니다 [엔진 서비스 계정 동기화](#azure-ad-connect-sync-service-account)합니다. admin 님 안녕하세요 특정 계정을 지정 하지 않을 때에 hello 계정이 생성 됩니다. |
| 동기화 서비스, 서비스 계정 옵션을 설치합니다. |AD 또는 로컬 사용자 계정 자격 증명 |사용자 권한은 부여 hello 설치 마법사 |Admin 님 안녕하세요 계정을 지정 하는 경우이 계정은 hello 동기화 서비스에 대 한 hello 서비스 계정으로 사용 됩니다. |
| TooAzure AD 연결 |Azure AD 디렉터리 자격 증명 |Azure AD에서 글로벌 관리자 역할 |<li>Hello Azure AD 디렉터리에서 동기화를 사용 하도록 설정 합니다.</li>  <li>Hello 생성 [Azure AD 계정](#azure-ad-service-account) Azure AD에서 진행 중인 동기화 작업에 사용 되는 합니다.</li> |
| 디렉터리에 연결 |연결 된 tooAzure AD은 각 포리스트에 대 한 온-프레미스 Active Directory 자격 증명 |hello 권한을 종속 기능에 사용 하도록 설정 하 고이 찾을 수 있습니다 [hello AD DS 계정 만들기](#create-the-ad-ds-account) |이 계정은 동기화 하는 동안 사용 되는 tooread 및 쓰기 디렉터리 정보입니다. |
| AD FS 서버 |각 서버 hello 목록에 대해 hello 마법사 자격 증명을 수집 hello 마법사를 실행 하는 hello 사용자의 hello 로그온 자격 증명이 부족 하 여 tooconnect 때 |도메인 관리자 |설치 하 고 hello AD FS 서버 역할을 구성 합니다. |
| 웹 응용 프로그램 프록시 서버 |각 서버 hello 목록에 대해 hello 마법사 자격 증명을 수집 hello 마법사를 실행 하는 hello 사용자의 hello 로그온 자격 증명이 부족 하 여 tooconnect 때 |Hello 대상 컴퓨터에 로컬 관리자 |WAP 서버 역할 설치 및 구성 |
| 프록시 트러스트 자격 증명 |페더레이션 서비스 신뢰 자격 증명 (hello 자격 증명 hello 모드 해제 프록시 사용 tooenroll hello FS에서에서 신뢰 인증서 |Hello AD FS 서버의 로컬 관리자 인 도메인 계정 |FS-WAP 신뢰 인증서의 초기 등록. |
| AD FS 서비스 계정 페이지에서 "도메인 사용자 계정 옵션 사용" |AD 사용자 계정 자격 증명 |도메인 사용자 |hello AD 사용자 계정 자격 증명에 제공 되는 hello AD FS 서비스의 hello 로그온 계정으로 사용 됩니다. |

### <a name="create-hello-ad-ds-account"></a>Hello AD DS 계정 만들기
hello에 지정한 계정은 hello **디렉터리 연결** 페이지 이전 tooinstallation Active Directory에에서 존재 해야 합니다.  Hello 필요한 사용 권한을 부여 있어야 합니다. hello 설치 마법사는 동기화 중는 hello 사용 권한 및 문제를 찾을 수만 확인 하지 않습니다.

사용 하면 필요한 권한을 hello 선택적 기능에 따라 달라 집니다. 여러 도메인이 있는 경우 hello 포리스트에 있는 모든 도메인에 대 한 hello 권한이 부여 되어야 합니다. 이러한 기능을 사용 하지 않도록 하는 경우 기본 hello **도메인 사용자** 권한으로 합니다.

| 기능 | 권한 |
| --- | --- |
| msDS-ConsistencyGuid 기능 |Toohello 게스트가 ConsistencyGuid 특성에서 설명 하는 쓰기 권한이 [게스트가 ConsistencyGuid sourceAnchor로 사용 하 여 디자인 개념-](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)합니다. | 
| 암호 동기화 |<li>디렉터리 변경 내용 복제</li>  <li>모든 디렉터리 변경 내용 복제 |
| Exchange 하이브리드 배포 |에 설명 된 사용 권한을 toohello 특성 쓰기 [Exchange 하이브리드 쓰기 저장](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) 사용자, 그룹 및 연락처에 대 한 합니다. |
| Exchange 메일 공용 폴더 |에 설명 된 사용 권한을 toohello 특성 읽기 [Exchange 메일에 대 한 공용 폴더](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) 공용 폴더에 대 한 합니다. | 
| 비밀번호 쓰기 저장 |에 설명 된 사용 권한을 toohello 특성 쓰기 [암호 관리 시작](../active-directory-passwords-writeback.md) 사용자에 대 한 합니다. |
| 장치 쓰기 저장 |[장치 쓰기 저장](active-directory-aadconnect-feature-device-writeback.md)에 설명한 대로 PowerShell 스크립트에 부여된 사용 권한입니다. |
| 그룹 쓰기 저장 |동기화된 **Office 365 그룹**에 대해 그룹 개체를 읽기, 만들기, 업데이트 및 삭제합니다.  자세한 내용은 [그룹 쓰기 저장](active-directory-aadconnect-feature-preview.md#group-writeback)을 참조하세요.|

## <a name="upgrade"></a>업그레이드
Azure AD Connect tooa 새 릴리스 버전에서 업그레이드할 경우 다음 권한을 hello가 필요 합니다.

| 주체 | 필요한 사용 권한 | 용도 |
| --- | --- | --- |
| Hello 설치 마법사를 실행 하는 사용자 |로컬 서버 hello 관리자 |이진을 업데이트합니다. |
| Hello 설치 마법사를 실행 하는 사용자 |ADSyncAdmins의 구성원 |TooSync 규칙 및 기타 구성 변경합니다. |
| Hello 설치 마법사를 실행 하는 사용자 |전체 SQL server를 사용 하는 경우: DBO (또는 유사한 곳) hello 동기화 엔진 데이터베이스의 |새 열을 사용한 테이블 업데이트와 같이 데이터베이스 수준을 변경합니다. |

## <a name="more-about-hello-created-accounts"></a>계정을 만든 hello 대 한 자세한 정보
### <a name="active-directory-account"></a>Active Directory 계정
Express 설정을 사용하는 경우 계정은 동기화에 사용되는 Active Directory에서 만들어집니다. 만든 hello 계정은 hello 사용자 컨테이너에서 hello 포리스트 루트 도메인에 있으며 접두사로 사용 이름을 **MSOL_**합니다. hello 계정이 만료 되지 않는 긴 복잡 한 암호 사용 하 여 생성 됩니다. 사용자 도메인에 암호 정책이 있는 경우 길고 복잡한 암호가 이 계정에 대해 허용되는지 확인합니다.

![AD 계정](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

사용자 지정 설정을 사용 하는 경우 라면 hello 설치를 시작 하기 전에 hello 계정 만들기를 담당 합니다.

### <a name="azure-ad-connect-sync-service-account"></a>Azure AD Connect 동기화 서비스 계정
hello 동기화 서비스가 서로 다른 계정에서 실행 될 수 있습니다. **가상 서비스 계정**(VSA), **그룹 관리 서비스 계정**(gMSA/sMSA) 또는 일반 사용자 계정으로 실행할 수 있습니다. hello 지원 옵션 변경 된 hello로의 Connect 2017 년 4 월 릴리스 새로 설치를 수행 합니다. Azure AD Connect의 이전 버전을 업그레이드하는 경우 이러한 추가 옵션을 사용할 수 없습니다.

| 계정 유형 | 설치 옵션 | 설명 |
| --- | --- | --- |
| [가상 서비스 계정](#virtual-service-account) | 빠른 및 사용자 지정, 2017년 4월 이후 | 도메인 컨트롤러에 설치를 제외한 모든 express 설치에 사용 되는 hello 옵션입니다. 사용자 지정에 대 한 또 다른 옵션을 사용 하지 않으면 hello 기본 옵션입니다. |
| [그룹 관리 서비스 계정](#group-managed-service-account) | 사용자 지정, 2017년 4월 이후 | 원격 SQL server를 사용 하 여 경우 것이 좋습니다 toouse 그룹 관리 서비스 계정입니다. |
| [사용자 계정](#user-account) | 빠른 및 사용자 지정, 2017년 4월 이후 | AAD_가 접두사로 추가되는 사용자 계정은 Windows Server 2008에 설치되는 경우 및 도메인 컨트롤러에 설치되는 경우 설치 중에만 만들어집니다. |
| [사용자 계정](#user-account) | 빠른 및 사용자 지정, 2017 3월 이전 | AAD_가 접두사로 추가되는 사용자 계정은 설치 중에 만들어집니다. 사용자 지정 설치를 사용하는 경우 다른 계정을 지정할 수 있습니다. |

Connect를 사용 하 여 빌드 2017 년 3 월에 또는 이후 Windows hello 서비스 계정에 대해 hello 암호를 재설정 하지 해야 하는 다음에 이전 보안상의 이유로 hello 암호화 키를 제거 합니다. Azure AD Connect를 다시 설치 하지 않고 다른 계정 hello 계정 tooany를 변경할 수 없습니다. 에서 업그레이드 하는 tooa 빌드 2017 년 4 월 또는 이상 버전에서는 다음 있기는 hello 서비스 계정에서 지원 되는 toochange hello 암호 하지만 사용 되는 hello 계정을 변경할 수 없습니다.

> [!Important]
> 처음 설치할 hello 서비스 계정을 설정할 수 있습니다. 없으면 hello 설치가 완료 되 면 toochange hello 서비스 계정을 지원 합니다.

이 테이블은 권장 되는 hello 기본적으로 테이블 및 hello에 대 한 지원 되는 옵션에는 서비스 계정 동기화 합니다.

범례:

- **굵게** hello 기본 옵션을 나타내고 대부분의 경우 hello에 권장 옵션을 선택 합니다.
- *기울임꼴* 나타냅니다 hello hello 기본 옵션 이므로 때 권장 옵션을 선택 합니다.
- 2008 - Windows Server 2008에 설치하는 경우 기본 옵션
- 굵지 않은 글꼴 - 지원되는 옵션
- Hello 서버에서 로컬 계정-로컬 사용자 계정
- 도메인 계정 - 도메인 사용자 계정
- sMSA - [독립 실행형 관리 서비스 계정](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA - [그룹 관리 서비스 계정](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>사용자 지정 | 원격 SQL</br>사용자 지정 |
| --- | --- | --- | --- |
| **독립 실행형/작업 그룹 컴퓨터** | 지원되지 않음 | **VSA**</br>로컬 계정(2008)</br>로컬 계정 |  지원되지 않음 |
| **도메인에 가입된 컴퓨터** | **VSA**</br>로컬 계정(2008) | **VSA**</br>로컬 계정(2008)</br>로컬 계정</br>도메인 계정</br>sMSA,gMSA | **gMSA**</br>도메인 계정 |
| **도메인 컨트롤러** | **도메인 계정** | *gMSA*</br>**도메인 계정**</br>sMSA| *gMSA*</br>**도메인 계정**|

#### <a name="virtual-service-account"></a>가상 서비스 계정
가상 서비스 계정은 암호가 없고 Windows에 의해 관리되는 특수한 유형의 계정입니다.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

hello VSA는 의도 한 toobe hello 동기화 엔진 및 SQL에 있는 hello 시나리오에 사용 되는 동일한 서버입니다. 원격 SQL을 사용 하 여 경우 toouse 권장는 [그룹 관리 서비스 계정](#managed-service-account) 대신 합니다.

이 기능을 사용하려면 Windows Server 2008 R2 이상이 필요합니다. Windows Server 2008에서 Azure AD Connect를 설치한 경우 hello 설치 toousing 대체는 [사용자 계정](#user-account) 대신 합니다.

#### <a name="group-managed-service-account"></a>그룹 관리 서비스 계정
원격 SQL server를 사용할 경우 toousing 권장는 **그룹 관리 서비스 계정은**합니다. 방법에 대 한 자세한 내용은 Active Directory 그룹 관리 서비스 계정에 대 한 참조 tooprepare [그룹 관리 서비스 계정 개요](https://technet.microsoft.com/library/hh831782.aspx)합니다.

toouse hello에이 옵션 [필수 구성 요소 설치](active-directory-aadconnect-get-started-custom.md#install-required-components) 페이지에서 **기존 서비스 계정을 사용 하 여**를 선택 하 고 **관리 서비스 계정**합니다.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
지원 되는 toouse 이기도 한 [독립 실행형 관리 서비스 계정](https://technet.microsoft.com/library/dd548356.aspx)합니다. 그러나 hello 로컬 컴퓨터에만 사용할 수 있습니다 이러한 되어 있으므로 없는 혜택 toouse hello 기본 가상 서비스 계정 보다 합니다.

이 기능을 사용하려면 Windows Server 2012 이상이 필요합니다. 이전 운영 체제 toouse 필요 하 고 원격 SQL을 사용 하 여 다음 사용 해야 합니다는 [사용자 계정](#user-account)합니다.

#### <a name="user-account"></a>사용자 계정
로컬 서비스 계정 (지정 하지 않는 한 hello 계정 toouse 사용자 지정 설정에서) hello 설치 마법사에 의해 만들어집니다. hello 계정이 붙은 **AAD_** 으로 hello 실제 동기화 서비스 toorun에 사용 합니다. 도메인 컨트롤러에 Azure AD Connect를 설치 하는 경우 hello 계정이 hello 도메인에 생성 됩니다. hello **AAD_** 경우 서비스 계정 hello 도메인에 배치 해야 합니다.
   - SQL Server를 실행하는 원격 서버를 사용합니다.
   - 인증이 필요한 프록시를 사용합니다.

![서비스 계정 동기화](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

hello 계정이 만료 되지 않는 긴 복잡 한 암호 사용 하 여 생성 됩니다.

이 계정은 hello에 대 한 hello 암호를 사용 하는 toostore 다른 계정을 안전 하 게에서 됩니다. 이러한 계정 암호 hello 데이터베이스에 암호화 되어 저장 됩니다. Windows 데이터 보호 API (DPAPI)를 사용 하 여 hello 암호화 서비스 비밀 키 암호화도 hello hello 암호화 키에 대 한 개인 키 보호 됩니다.

전체 SQL Server를 사용 하는 경우 hello 서비스 계정은 hello hello 동기화 엔진에 대 한 hello 만든 데이터베이스의 DBO입니다. hello 서비스에는 다른 사용 권한과 함께 의도 한 대로 작동 하지 않습니다. SQL 로그인도 생성됩니다.

hello 계정 권한 toofiles, 레지스트리 키 및 기타 개체 관련된 toohello 동기화 엔진에도 부여 됩니다.

### <a name="azure-ad-service-account"></a>Azure AD 서비스 계정
Azure AD의 계정 hello 동기화 서비스 사용에 대해 만들어집니다. 이 계정은 표시 이름으로 식별할 수 있습니다.

![AD 계정](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

hello hello 서버 hello 계정의 이름은 hello hello 사용자 이름의 두 번째 부분에서 식별할 수 있습니다. Hello 그림 hello 서버 이름은 FABRIKAMCON를입니다. 준비 서버가 있는 경우 각 서버는 고유한 계정을 포함합니다.

hello 서비스 계정이 만료 되지 않는 긴 복잡 한 암호 사용 하 여 생성 됩니다. 특별 한 역할 부여 **디렉터리 동기화 계정** 있는 사용 권한을 tooperform 디렉터리 동기화는 작업만 포함 합니다. 이 특수 기본 제공 역할 hello Azure AD Connect 마법사 외부에서 부여할 수 없습니다. hello Azure 포털을 보여 줍니다 hello 역할에이 계정을 **사용자**합니다.

Azure AD에서 동기화 서비스 계정은 20개로 제한됩니다. 기존 Azure AD 서비스 계정 하면 Azure AD에서 Azure AD PowerShell cmdlet을 다음 hello 실행 tooget hello 목록:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

사용 하지 않는 tooremove Azure AD 서비스 계정, Azure AD PowerShell cmdlet을 다음 hello 실행:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>다음 단계
[Azure Active Directory와 온-프레미스 ID 통합](../active-directory-aadconnect.md)에 대해 자세히 알아봅니다.
