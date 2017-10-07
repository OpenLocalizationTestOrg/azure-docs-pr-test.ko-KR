---
title: "Azure Active Directory Domain Services: 문제 해결 가이드 | Microsoft Docs"
description: "Azure AD 도메인 서비스에 대한 문제 해결 가이드"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 4bc8c604-f57c-4f28-9dac-8b9164a0cf0b
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 86eb3513b7bc921c59287600b1b76eeda20c1356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-domain-services---troubleshooting-guide"></a>Azure AD Domain Services - 문제 해결 가이드
이 문서는 Azure AD(Active Directory) 도메인 서비스를 설치하거나 관리할 때 발생할 수 있는 문제에 대한 문제 해결 힌트를 제공합니다.

## <a name="you-cannot-enable-azure-ad-domain-services-for-your-azure-ad-directory"></a>Azure AD 디렉터리에 대해 Azure AD Domain Services를 사용할 수 없습니다.
Tooenable 디렉터리에 대 한 Azure AD 도메인 서비스를 시도 하 고 실패 하거나 가져옵니다 때 오류를 해결 하는이 섹션 사용 하면 뒤로 too'Disabled 설정/해제 '.

Hello toohello 오류 메시지가 발생 하면 해당 하는 문제 해결 단계를 선택 합니다.

| **오류 메시지** | **해결 방법** |
| --- |:--- |
| *hello 이름 contoso100.com 이미이 네트워크에서 사용 중입니다. 사용하지 않는 이름을 지정하십시오.* |[Hello 가상 네트워크의 도메인 이름 충돌](active-directory-ds-troubleshooting.md#domain-name-conflict) |
| *이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 서비스에는 적절 한 사용 권한이 toohello 응용 프로그램 'Azure AD 도메인 서비스 Sync' 라는 없습니다. 'Azure AD 도메인 서비스 Sync'를 호출 하는 hello 응용 프로그램을 삭제 하 고 tooenable 도메인 서비스에서 Azure AD 테 넌 트를 시도 하십시오.* |[도메인 서비스에 적절 한 사용 권한이 toohello Azure AD 도메인 서비스 동기화 응용 프로그램이 없는](active-directory-ds-troubleshooting.md#inadequate-permissions) |
| *이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 도메인 서비스에서 Azure AD 테 넌 트 응용 프로그램을 hello 가지 않습니다 권한 tooenable 도메인 서비스를 필요 합니다. 응용 프로그램 식별자 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello와 hello 응용 프로그램을 삭제 한 후 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.* |[테 넌 트에 도메인 서비스 응용 프로그램 hello 제대로 구성 되지 않았습니다.](active-directory-ds-troubleshooting.md#invalid-configuration) |
| *이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello Microsoft Azure AD 응용 프로그램은 Azure AD 테 넌 트에 사용할 수 없습니다. 응용 프로그램 식별자 00000002-0000-0000-c000-000000000000 hello와 hello 응용 프로그램을 사용 하도록 설정 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.* |[hello Microsoft Graph 응용 프로그램은 Azure AD 테 넌 트에 사용할 수 없습니다.](active-directory-ds-troubleshooting.md#microsoft-graph-disabled) |

### <a name="domain-name-conflict"></a>도메인 이름 충돌
**오류 메시지:**

*hello 이름 contoso100.com 이미이 네트워크에서 사용 중입니다. 사용하지 않는 이름을 지정하십시오.*

**재구성:**

Hello로 기존 도메인 가졌는지 확인 동일한 도메인 이름을 해당 가상 네트워크에서 사용할 수 있습니다. 예를 들어 hello 선택한 가상 네트워크에서 이미 사용할 수 있는 ' contoso.com' 이라는 도메인을 사용 한다고 가정 합니다. 나중 tooenable hello로 사용 되는 Azure AD 도메인 서비스는 관리 되는 도메인을 시도 하면 해당 가상 네트워크에 동일한 도메인 이름 (즉, ' contoso.com'). Tooenable Azure AD 도메인 서비스는 동안 오류가 발생 하면 합니다.

이 오류는 해당 가상 네트워크에서 도메인 이름 hello에 대 한 tooname 충돌 때문입니다. 이 경우 Azure AD 도메인 서비스는 관리 되는 도메인을 다른 이름 tooset를 사용 해야 합니다. 또는 기존 도메인 hello를 프로 비전 해제할 수 있으며 tooenable Azure AD 도메인 서비스를 진행할 수 있습니다.

### <a name="inadequate-permissions"></a>부적절한 권한
**오류 메시지:**

*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 서비스에는 적절 한 사용 권한이 toohello 응용 프로그램 'Azure AD 도메인 서비스 Sync' 라는 없습니다. 'Azure AD 도메인 서비스 Sync'를 호출 하는 hello 응용 프로그램을 삭제 하 고 tooenable 도메인 서비스에서 Azure AD 테 넌 트를 시도 하십시오.*

**재구성:**

Azure AD 디렉터리에서 'Azure AD 도메인 서비스 Sync' hello 이름의 응용 프로그램인 경우 toosee를 확인 합니다. 이 응용 프로그램이 있으면 삭제한 다음 Azure AD Domain Services를 사용하도록 다시 설정해야 합니다.

수행 hello 단계 toocheck hello 응용 프로그램 및 toodelete hello 있는지에 대 한 다음, hello 응용 프로그램이 있는 경우:

1. Toohello 이동 **Azure 클래식 포털** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).
2. 선택 hello **Active Directory** hello 왼쪽된 창에서 노드.
3. Azure AD 도메인 서비스 선택 hello Azure AD 테 넌 트 (디렉터리) tooenable 방식입니다.
4. Toohello 이동 **응용 프로그램** 탭 합니다.
5. 선택 hello **회사가 보유 한 응용 프로그램** hello 드롭다운에서 옵션입니다.
6. **Azure AD Domain Services 동기화**라는 응용 프로그램이 있는지 확인합니다. Hello 응용 프로그램에서 볼 수 있으면 계속 toodelete 것입니다.
7. Hello 응용 프로그램을 삭제 한 후 tooenable Azure AD 도메인 서비스를 다시 한 번 시도 합니다.

### <a name="invalid-configuration"></a>유효하지 않은 구성
**오류 메시지:**

*이 Azure AD 테 넌 트에 도메인 서비스를 사용할 수 없습니다. hello 도메인 서비스에서 Azure AD 테 넌 트 응용 프로그램을 hello 가지 않습니다 권한 tooenable 도메인 서비스를 필요 합니다. 응용 프로그램 식별자 d87dcbc6-a371-462e-88e3-28ad15ec4e64 hello와 hello 응용 프로그램을 삭제 한 후 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.*

**재구성:**

(D87dcbc6-a371-462e-88e3-28ad15ec4e64의 응용 프로그램 식별자)를 가진 ' AzureActiveDirectoryDomainControllerServices' hello 이름의 응용 프로그램이 Azure AD 디렉터리에 있는 경우 toosee를 확인 합니다. 이 응용 프로그램이 있으면 하 고 다시 활성화 한 다음 Azure AD 도메인 서비스 toodelete 필요 합니다.

다음 PowerShell 스크립트 toofind hello 응용 프로그램 hello를 사용 하 여 삭제.

> [!NOTE]
> 이 스크립트는 **Azure AD PowerShell 버전 2** cmdlet을 사용합니다. 모든 사용 가능한 cmdlet 및 toodownload hello 모듈의 전체 목록에 대 한 읽기 hello [azure Ad PowerShell 참조 설명서](https://msdn.microsoft.com/library/azure/mt757189.aspx)합니다.
>
>

```
$InformationPreference = "Continue"
$WarningPreference = "Continue"

$aadDsSp = Get-AzureADServicePrincipal -Filter "AppId eq 'd87dcbc6-a371-462e-88e3-28ad15ec4e64'" -ErrorAction Ignore
if ($aadDsSp -ne $null)
{
    Write-Information "Found Azure AD Domain Services application. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $aadDsSp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services application."
}

$identifierUri = "https://sync.aaddc.activedirectory.windowsazure.com"
$appFilter = "IdentifierUris eq '" + $identifierUri + "'"
$app = Get-AzureADApplication -Filter $appFilter
if ($app -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync application. Deleting it ..."
    Remove-AzureADApplication -ObjectId $app.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync application."
}

$spFilter = "ServicePrincipalNames eq '" + $identifierUri + "'"
$sp = Get-AzureADServicePrincipal -Filter $spFilter
if ($sp -ne $null)
{
    Write-Information "Found Azure AD Domain Services Sync service principal. Deleting it ..."
    Remove-AzureADServicePrincipal -ObjectId $sp.ObjectId
    Write-Information "Deleted hello Azure AD Domain Services Sync service principal."
}
```
<br>

### <a name="microsoft-graph-disabled"></a>Microsoft Graph 사용 안 함
**오류 메시지:**

이 Azure AD 테넌트에서는 Domain Services를 사용할 수 없습니다. hello Microsoft Azure AD 응용 프로그램은 Azure AD 테 넌 트에 사용할 수 없습니다. 응용 프로그램 식별자 00000002-0000-0000-c000-000000000000 hello와 hello 응용 프로그램을 사용 하도록 설정 시도 tooenable Azure AD 테 넌 트에 대 한 도메인 서비스.

**재구성:**

Hello 식별자 00000002-0000-0000-c000-000000000000으로 응용 프로그램을 사용 하지 않도록 설정한 경우 toosee를 확인 합니다. 이 응용 프로그램은 Microsoft Azure AD 응용 프로그램 hello 고 Graph API 액세스 tooyour Azure AD 테 넌 트를 제공 합니다. Azure AD 도메인 서비스에 Azure AD 테 넌 트 tooyour 관리 되는이 응용 프로그램 활성화 toobe toosynchronize 필요한 도메인입니다.

tooresolve이이 오류를이 응용 프로그램을 사용 하도록 설정 하 고 다음 tooenable 도메인 서비스에서 Azure AD 테 넌 트를 시도 하십시오.

## <a name="users-are-unable-toosign-in-toohello-azure-ad-domain-services-managed-domain"></a>사용자가 없습니다 toosign toohello 관리 되는 Azure AD 도메인 서비스 도메인에서
하나 이상의 사용자가 Azure AD 테 넌 트에 없습니다 toosign toohello 새로 만든 관리 되는 도메인의 인 hello 문제 해결 단계를 수행 합니다.

* **로그인 UPN 형식을 사용 하 여:** toosign hello UPN 형식을 사용 하 여 시도 하세요 (예를 들어 'joeuser@contoso.com') hello SAMAccountName 형식 ('CONTOSO\joeuser') 대신. SAMAccountName hello hello 관리 되는 도메인에 있는 다른 사용자와 동일한 hello은 너무 긴 UPN 접두사를 가진 되었거나 사용자에 대해 자동으로 생성 될 수 있습니다. hello UPN 형식 toobe Azure AD 테 넌 트 내에서 고유 보장 됩니다.

> [!NOTE]
> Toohello Azure AD 도메인 서비스에 대 한 관리 되는 도메인에서 UPN 형식 toosign hello를 사용 하는 것이 좋습니다.
>
>

* 갖추어야 할 [암호 동기화를 사용 하도록 설정](active-directory-ds-getting-started-password-sync.md) hello 시작 가이드에 설명 된 hello 단계에 따라 합니다.
* **외부 계정:** hello 영향을 받는 사용자 계정을 hello Azure AD 테 넌 트에 외부 계정이 아닌지 확인 합니다. 외부 계정의 예는 Microsoft 계정(예: 'joe@live.com') 또는 외부 Azure AD 디렉터리에서 사용자 계정을 포함합니다. Azure AD 도메인 서비스에 이러한 사용자 계정에 대 한 자격 증명이 없기 때문에 이러한 사용자 toohello 관리 되는 도메인에 서명할 수 없습니다.
* **계정 동기화:** hello 영향을 받는 사용자 계정이 온-프레미스 디렉터리에서 동기화를 확인 합니다.

  * 배포 했거나 toohello 업데이트 [최신 버전의 Azure AD Connect 권장](https://www.microsoft.com/en-us/download/details.aspx?id=47594)합니다.
  * Azure AD Connect를 너무 구성한[전체 동기화를 수행](active-directory-ds-getting-started-password-sync.md)합니다.
  * 디렉터리의 hello 크기에 따라 수는 사용자 계정에 대 한 시간이 걸릴 하 고 해시 toobe Azure AD 도메인 서비스에서 사용할 수 있는 자격 증명 합니다. 인증 (hello의 크기에 따라 몇 시간 tooa 일 또는 큰 디렉터리에 대 한 두 디렉터리-)을 다시 시도 하기 전에 충분 한 시간 동안 대기를 확인 합니다.
  * Hello 이전 단계를 확인 한 후 hello 문제가 지속 되 면 hello Microsoft Azure AD Sync Service를 다시 시작 하십시오. 동기화 시스템에서 명령 프롬프트를 시작 하 고 다음 명령을 hello를 실행 합니다.

    1. net stop 'Microsoft Azure AD Sync'
    2. net start 'Microsoft Azure AD Sync'
* **클라우드 전용 계정을**: hello 영향을 받는 사용자 계정을 클라우드 전용 사용자 계정이 확인 Azure AD 도메인 서비스를 사용 하도록 설정한 후 해당 hello 사용자가 자신의 암호를 변경 합니다. 이 단계를 수행 하면 hello 자격 증명 생성 된 Azure AD 도메인 서비스 toobe 필요한 해시 합니다.

## <a name="users-removed-from-your-azure-ad-tenant-are-not-removed-from-your-managed-domain"></a>Azure AD 테넌트에서는 제거되지만 관리되는 도메인에서는 제거되지 않는 사용자
Azure AD에서는 사용자 개체를 실수로 삭제하지 못하도록 보호합니다. Azure AD 테 넌 트 로부터 사용자 계정을 삭제 하면 hello 해당 하는 사용자 개체는 이동된 toohello 휴지통을 활성화 합니다. 이 삭제 작업은 동기화 된 tooyour 관리 되는 도메인을 하면 hello 사용 안 함을 표시 하는 사용자 계정 toobe에 해당 합니다. 이 기능을 사용 하면 복구 하거나 나중에 hello 사용자 계정 삭제 취소할 수 있습니다.

hello hello에 남아 있는 관리 되는 도메인의 상태를 사용 하지 않도록 설정 하는 사용자 계정, 가진 사용자 계정을 다시 만드는 경우에 hello Azure AD 디렉터리에서 동일한 UPN입니다. tooforce 필요한 관리 되는 도메인에서 tooremove hello 사용자 계정에 Azure AD 테 넌 트에서 삭제 합니다.

tooremove hello 사용자 계정을 통해 관리 되는 도메인에서 완벽 하 게 Azure AD 테 넌 트에서 hello 사용자를 영구적으로 삭제 합니다. Hello Remove-msoluser PowerShell cmdlet을 사용 하 여 hello로 '-RemoveFromRecycleBin' 옵션을이에 설명 된 대로 [MSDN 문서](https://msdn.microsoft.com/library/azure/dn194132.aspx)합니다.

## <a name="contact-us"></a>문의처
너무 hello Azure Active Directory 도메인 서비스 제품 팀에 문의[의견 공유 또는 지원을 위해](active-directory-ds-contact-us.md)합니다.
