---
title: "Azure AD Domain Services: 암호 동기화 사용 | Microsoft Docs"
description: "Azure Active Directory Domain Services 시작"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a>암호 동기화 tooAzure Active Directory 도메인 서비스를 사용 하도록 설정
이전 작업에서 Azure AD(Azure Active Directory) 테넌트에 대해 Azure Active Directory Domain Services를 사용하도록 설정했습니다. hello 다음 작업은 관리자 NTLM (NT LAN) 및 Kerberos 인증 tooAzure에 필요한 자격 증명 해시의 tooenable 동기화 AD 도메인 서비스. 자격 증명 동기화를 설정한 후 사용자가 회사 자격 증명으로 관리 되는 도메인 toohello 로그인 수 있습니다.

Azure AD Connect를 사용 하 여 온-프레미스 디렉터리에서 동기화 되는 클라우드 전용 사용자 계정 및 사용자 계정에 대 한 관련 된 hello 단계 서로 다릅니다. Azure AD 테 넌 트의 조합은 하는 경우 사용자와 사용자가 온-프레미스에서 클라우드, AD tooperform 두 단계가 필요 합니다.

<br>

> [!div class="op_single_selector"]
> * **클라우드 전용 사용자 계정을**: [클라우드 전용 사용자 tooyour 관리 되는 도메인 계정에 대해 암호 동기화](active-directory-ds-getting-started-password-sync.md)
> * **온-프레미스 사용자 계정과**: [온-프레미스에서 동기화 된 사용자 계정에 대 한 암호 동기화 할 AD tooyour 도메인 관리](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a>태스크 5: 온-프레미스와 동기화 하는 사용자 계정에 대 한 암호 동기화 tooyour 관리 되는 도메인을 사용 하도록 설정 AD
동기화 Azure AD 테 넌 트와 Azure AD Connect를 사용 하 여 조직의 온-프레미스 디렉터리 toosynchronize 설정 됩니다. 기본적으로 Azure AD Connect에는 NTLM 및 Kerberos 자격 증명 해시 tooAzure AD 동기화 하지 않습니다. Azure AD 도메인 서비스 toouse tooconfigure Azure AD Connect toosynchronize 자격 증명 해시가 NTLM 및 Kerberos 인증에 필요한 필요 합니다. 온-프레미스 디렉터리 tooyour Azure AD 테 넌 트에서 hello 필요한 자격 증명 해시의 동기화를 사용 하는 hello 단계를 수행 합니다.

> [!NOTE]
> 조직에 해야 하는 온-프레미스 디렉터리에서 동기화 되는 사용자 계정이 있는 경우 동기화 순서 toouse hello에 대 한 관리 되는 도메인에서 NTLM 및 Kerberos 해시를 사용 합니다. 동기화 된 사용자 계정을 온-프레미스 디렉터리에 작성 되어 있으며 계정을 Azure AD Connect를 사용 하 여 Azure AD 테 넌 tooyour 동기화입니다.
>
>

### <a name="install-or-update-azure-ad-connect"></a>Azure AD Connect 설치 또는 업데이트
Hello 권장 최신 설치 버전 도메인에 Azure AD Connect의 컴퓨터를 가입 합니다. Tooupdate 해야 Azure AD Connect 설치의 기존 인스턴스를 설정한 경우 해당 toouse hello 최신 버전의 Azure AD Connect 합니다. 알려진 문제/버그 수 이미 수정 된, tooavoid hello 최신 버전의 Azure AD Connect 항상 사용을 확인 합니다.

**[Azure AD Connect 다운로드](http://www.microsoft.com/download/details.aspx?id=47594)**

권장 버전: **1.1.553.0** - 2017년 6월 27일 게시

> [!WARNING]
> Hello를 설치 해야 최신 버전의 Azure AD Connect tooenable hello 레거시 암호 자격 증명 (NTLM 및 Kerberos 인증에 필요) toosynchronize tooyour Azure AD 테 넌 트를 권장 합니다. 이 기능은 hello 레거시 디렉터리 동기화 도구 또는 Azure AD Connect의 이전 릴리스에서 사용할 수 없습니다.
>
>

Azure AD Connect에 대 한 설치 지침 hello 다음에 사용할 수 있는 문서- [Azure AD Connect 시작](../active-directory/active-directory-aadconnect.md)

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a>NTLM 및 Kerberos 자격 증명 해시 tooAzure AD의 동기화 사용
Hello에 나오는 각 AD 포리스트에 tooforce 전체 암호 동기화에 PowerShell 스크립트를 실행 하 고 모든 온-프레미스 사용자의 자격 증명 해시 toosync tooyour Azure AD 테 넌 트를 사용 하도록 설정 합니다. 이 스크립트는 NTLM/Kerberos 인증 toobe 동기화 된 tooyour Azure AD 테 넌 트에 대 한 필요한 hello 자격 증명 해시를 활성화 합니다.

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

디렉터리의 hello 크기에 따라 (사용자, 수 등 그룹화), AD 시간이 tooAzure을 해시 하는 자격 증명을 동기화 합니다. hello 암호는 사용할 수 hello Azure AD 도메인 서비스에 대 한 관리 되는 도메인에 hello 자격 증명 해시가 tooAzure AD를 동기화 한 후에 바로.

<br>

## <a name="related-content"></a>관련 콘텐츠
* [활성화 암호 동기화 tooAAD 도메인 서비스에서 클라우드 전용 Azure AD 디렉터리](active-directory-ds-getting-started-password-sync.md)
* [Azure AD 도메인 서비스 관리되는 도메인 관리](active-directory-ds-admin-guide-administer-domain.md)
* [Windows 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-windows-vm.md)
* [Red Hat Enterprise Linux 가상 컴퓨터 tooan Azure AD 도메인 서비스는 관리 되는 도메인에 가입](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
