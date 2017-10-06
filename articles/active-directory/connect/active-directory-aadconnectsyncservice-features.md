---
title: "aaaAzure AD Connect 동기화 서비스 기능 및 구성 | Microsoft Docs"
description: "Azure AD Connect 동기화 서비스의 서비스 쪽 기능을 설명합니다."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 213aab20-0a61-434a-9545-c4637628da81
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 7ad05c45bb6b5fd5deaa3466e2936b19d3d9eabb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-features"></a>Azure AD Connect 동기화 서비스 기능
Azure AD Connect의 hello 동기화 기능에는 두 가지 구성 요소에 있습니다.

* hello 온-프레미스 구성 요소 라는 **Azure AD Connect 동기화**라고도 **동기화 엔진이**합니다.
* Azure ad에서로 알려져 있는 hello 서비스 **Azure AD Connect 동기화 서비스**

이 항목에서는 다음 hello 기능이 하는 방법에 대해 설명의 hello **Azure AD Connect 동기화 서비스** 작업 및 방법 Windows PowerShell을 사용 하 여 구성할 수 있습니다.

이러한 설정을 hello 구성 [Azure Active Directory에 대 한 Windows PowerShell 모듈](http://aka.ms/aadposh)합니다. Azure AD Connect에서 다운로드하여 별도로 설치합니다. 이 항목에서 설명 하는 hello cmdlet hello에 도입 된 [2016 년 3 월 릴리스 (빌드 9031.1)](http://social.technet.microsoft.com/wiki/contents/articles/28552.microsoft-azure-active-directory-powershell-module-version-release-history.aspx#Version_9031_1)합니다. 이 항목에서 설명 하는 hello cmdlet 없는 또는 결과 동일 하 고 있는지 확인 하는 hello를 생성 하지 않는 경우 hello 최신 버전을 실행 합니다.

를 실행 하 여 Azure AD 디렉터리에서 toosee hello 구성 `Get-MsolDirSyncFeatures`합니다.  
![Get-MsolDirSyncFeatures 결과](./media/active-directory-aadconnectsyncservice-features/getmsoldirsyncfeatures.png)

이러한 설정 중 대부분은 Azure AD Connect에서만 변경할 수 있습니다.

hello 다음 설정을 구성할 수 있습니다 하 여 `Set-MsolDirSyncFeature`:

| DirSyncFeature | 주석 |
| --- | --- |
| [EnableSoftMatchOnUpn](#userprincipalname-soft-match) |또한 tooprimary SMTP 주소에 userPrincipalName에 개체 toojoin를 허용합니다. |
| [SynchronizeUpnForManagedUsers](#synchronize-userprincipalname-updates) |(페더레이션 되지 않은) 사용자가 관리 되는 사용이 허가 hello 동기화 엔진 tooupdate hello userPrincipalName 특성을 허용합니다. |

기능을 사용하도록 설정한 후 다시 해제할 수 없습니다.

> [!NOTE]
> 2016 년 8 월 24 일에서 기능 hello *특성 복원 력 중복* 은 새로운 Azure에 대 한 기본값으로 사용 가능 AD 디렉터리입니다. 또한 이 기능은 이 날짜 이전에 생성된 디렉터리에서 롤아웃되고 사용하도록 설정됩니다. 디렉터리가 있을 때 프로그램 tooget에 대 한이 기능 사용 전자 메일 알림을 받습니다.
> 
> 

hello 다음과 같은 Azure AD Connect에서 구성 된 설정과으로 수정할 수 없으며 `Set-MsolDirSyncFeature`:

| DirSyncFeature | 주석 |
| --- | --- |
| DeviceWriteback |[Azure AD Connect: 장치 쓰기 저장 사용](active-directory-aadconnect-feature-device-writeback.md) |
| DirectoryExtensions |[Azure AD Connect 동기화: 디렉터리 확장](active-directory-aadconnectsync-feature-directory-extensions.md) |
| [DuplicateProxyAddressResiliency<br/>DuplicateUPNResiliency](#duplicate-attribute-resiliency) |다른 개체 보다는 hello 전체 개체 내보내기 작업 중 실패의 중복 때 격리 하는 특성 toobe를 수 있습니다. |
| PasswordSync |[Azure AD Connect 동기화로 암호 동기화 구현](active-directory-aadconnectsync-implement-password-synchronization.md) |
| UnifiedGroupWriteback |[미리 보기: 그룹 쓰기 저장](active-directory-aadconnect-feature-preview.md#group-writeback) |
| UserWriteback |현재 지원되지 않습니다. |

## <a name="duplicate-attribute-resiliency"></a>중복 특성 복원력
Tooprovision 실패 하는 대신 개체와 중복 된 Upn/proxyAddresses, hello 중복 된 특성은 "격리" 임시 값이 할당 됩니다. Hello 충돌이 해결 되 면 hello 임시 UPN은 toohello 적절 한 값을 자동으로 변경 합니다. 자세한 내용은 [ID 동기화 및 중복 특성 복원력](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)을 참조하세요.

## <a name="userprincipalname-soft-match"></a>UserPrincipalName 소프트 일치
또한 toohello에서 소프트 일치 UPN에 대 한 사용이 기능을 사용 하는 경우 [기본 SMTP 주소](https://support.microsoft.com/kb/2641663), 항상 활성화 되어 있습니다. 소프트-일치가 toomatch 사용 되는 기존 클라우드 사용자가 온-프레미스 사용자와 Azure AD에서 합니다.

필요한 toomatch 온-프레미스 AD 계정 hello 클라우드에서 만든 계정 가진 Exchange Online을 사용 하지 않는 경우이 기능은 유용 합니다. 이 시나리오에서는 일반적으로 설명 tooset hello SMTP 특성에에서 없는 hello 클라우드입니다.

이 기능은 새로 만든 Azure AD 디렉터리에 기본적으로 설정되어 있습니다. 다음을 실행하여 이 기능을 사용하도록 설정했는지 확인할 수 있습니다.  

```
Get-MsolDirSyncFeatures -Feature EnableSoftMatchOnUpn
```

Azure AD 디렉터리에서 이 기능을 사용하도록 설정하지 않은 경우 다음을 실행하여 설정할 수 있습니다.  

```
Set-MsolDirSyncFeature -Feature EnableSoftMatchOnUpn -Enable $true
```

## <a name="synchronize-userprincipalname-updates"></a>UserPrincipalName 업데이트 동기화
지금까지 온-프레미스에서 hello 동기화 서비스를 사용 하 여 업데이트 toohello UserPrincipalName 특성에 차단 된 이러한 조건을 모두 true가 아니면:

* hello 사용자 (페더레이션 되지 않은)으로 관리 됩니다.
* hello 사용자 라이선스를 할당 되지 않았습니다.

자세한 내용은 참조 하십시오. [온-프레미스 UPN 또는 대체 로그인 ID 사용자를 Office 365, Azure 또는 Intune 이름이 일치 하지 않습니다 hello](https://support.microsoft.com/kb/2523192)합니다.

이 기능을 사용 하면 변경 된 온-프레미스 되 고 암호 동기화를 사용 하 여 hello 동기화 엔진 tooupdate hello userPrincipalName가 있습니다. 페더레이션을 사용하는 경우 이 기능은 지원되지 않습니다.

이 기능은 새로 만든 Azure AD 디렉터리에 기본적으로 설정되어 있습니다. 다음을 실행하여 이 기능을 사용하도록 설정했는지 확인할 수 있습니다.  

```
Get-MsolDirSyncFeatures -Feature SynchronizeUpnForManagedUsers
```

Azure AD 디렉터리에서 이 기능을 사용하도록 설정하지 않은 경우 다음을 실행하여 설정할 수 있습니다.  

```
Set-MsolDirSyncFeature -Feature SynchronizeUpnForManagedUsers -Enable $true
```

이 기능을 사용하도록 설정하면 기존 userPrincipalName 값이 그대로 유지됩니다. 사용자에 게 hello 일반 델타 동기화는 hello userPrincipalName 특성 온-프레미스의 다음 변경 시 hello UPN을 업데이트 합니다.  

## <a name="see-also"></a>참고 항목
* [Azure AD Connect 동기화](active-directory-aadconnectsync-whatis.md)
* [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md)

