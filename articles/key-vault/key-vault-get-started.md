---
title: "Azure 키 자격 증명 모음 시작 aaaGet | Microsoft Docs"
description: "이 자습서 toohelp 얻게를 사용 하 여 azure에서 toostore 강화 된 컨테이너를 Azure 키 자격 증명 모음 toocreate와 시작 및 암호화 키 및 Azure에서 암호 관리 합니다."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Azure 주요 자격 증명 모음 시작
Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다. 자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.

## <a name="introduction"></a>소개
이 자습서 toohelp 얻게를 사용 하 여 toostore Azure에서 확정 된 컨테이너 (볼트)을 Azure 주요 자격 증명 모음 toocreate를 시작 하 고 암호화 키 및 Azure에서 암호 관리 합니다. 이 과정을 보여 줍니다 hello toocreate Azure PowerShell을 사용 하 여 키 또는 암호 Azure 응용 프로그램과 함께 사용할 수 있는 포함 된 자격 증명 모음입니다. 그런 다음 응용 프로그램이 해당 키 또는 암호를 사용할 수 있는 방법을 보여 줍니다.

**예상 시간 toocomplete:** 20 분

> [!NOTE]
> 이 자습서는 어떻게 toowrite hello hello 단계 중 하나를 포함 하는 Azure 응용 프로그램, 즉 어떻게 tooauthorize 응용 프로그램 toouse 키 또는 암호에 hello 키 자격 증명 모음에 대 한 지침을 다루지 않습니다.
>
> 이 자습서에서는 Azure PowerShell을 사용합니다. 플랫폼 간 명령줄 인터페이스 지침은 [이 해당 자습서](key-vault-manage-with-cli2.md)를 참조하세요.
>
>

Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 있어야 합니다.

* 구독 tooMicrosoft Azure 아직 구독이 없는 경우 [무료 계정](https://azure.microsoft.com/pricing/free-trial/)을 등록할 수 있습니다.
* Azure PowerShell, **최소 버전 1.1.0**. Azure PowerShell tooinstall Azure 구독과 연결을 참조 하세요 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다. Azure PowerShell을 이미 설치 되어 있는 hello Azure PowerShell 콘솔에서 hello 버전 알지 못할 경우 입력 `(Get-Module azure -ListAvailable).Version`합니다. Azure PowerShell 버전 0.9.1 ~ 0.9.8이 설치된 경우, 일부 약간의 변경이 있지만 이 자습서를 계속 사용할 수 있습니다. Hello를 사용 해야 하는 예를 들어 `Switch-AzureMode AzureResourceManager` 명령 및 hello Azure 키 자격 증명 모음 명령 중 일부 변경 되었습니다. 목록이 hello 버전 0.9.8 통해 0.9.1 키 자격 증명 모음 cmdlet에 대 한 참조 [Azure 키 자격 증명 모음 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)합니다.
* 응용 프로그램 구성된 toouse hello 키 또는 암호를이 자습서에서 만드는 됩니다입니다. 샘플 응용 프로그램은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/en-us/download/details.aspx?id=45343)합니다. 추가 정보 파일을 함께 제공 된 hello를 참조 하십시오.

이 자습서는 Azure PowerShell 초보자를 위한 만들어졌지만 모듈, cmdlet 및 세션 같은 hello 기본 개념을 이해 하는 것으로 가정 합니다. 자세한 내용은 [Windows PowerShell 시작](https://technet.microsoft.com/library/hh857337.aspx)을 참조하세요.

자세한이 자습서를 사용 하 여 hello에서 볼 수 있는 모든 cmdlet에 대 한 도움말을 tooget **Get-help** cmdlet.

    Get-Help <cmdlet-name> -Detailed

예를 들어 hello에 대 한 도움말을 tooget **로그인 AzureRmAccount** cmdlet, 유형:

    Get-Help Login-AzureRmAccount -Detailed

또한 다음 Azure PowerShell에서 Azure 리소스 관리자와 친숙 한 자습서 tooget hello를 읽을 수 있습니다.

* [어떻게 tooinstall Azure PowerShell 및 구성](/powershell/azure/overview)
* [리소스 관리자로 Azure PowerShell 사용](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Tooyour 구독 연결
Azure PowerShell 세션을 시작 하 고 다음 명령을 hello로 tooyour Azure 계정에에서 로그인 합니다.  

    Login-AzureRmAccount

예를 들어 Azure Government Azure의 특정 인스턴스를 사용 하는 경우 사용 하 여 hello-이 명령 사용 하 여 환경 매개 변수입니다. 예: `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

Hello 팝업 브라우저 창에서 Azure 계정 사용자 이름 및 암호를 입력 합니다. Azure PowerShell을이 계정 및 기본적으로 관련 된 모든 hello 등록이 사용 하 여 첫 번째 hello 됩니다.

구독이 여러 개 있고 Azure 키 자격 증명 모음에 대 한 특정 한 toouse toospecify 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.

    Get-AzureRmSubscription

그런 다음 toospecify hello 구독 toouse, 유형:

    Set-AzureRmContext -SubscriptionId <subscription ID>

Azure PowerShell을 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.

## <a id="resource"></a>새 리소스 그룹 만들기
Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다. 이 자습서에서는 **ContosoResourceGroup** 이라는 새 리소스 그룹을 만듭니다.

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>키 자격 증명 모음 만들기
사용 하 여 hello [새로 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate 주요 자격 증명 모음입니다. 이 cmdlet에는 세 가지 필수 매개 변수:는 **리소스 그룹 이름은**, **주요 자격 증명 모음 이름**, hello 및 **지리적 위치**합니다.

예를 들어, 자격 증명 모음 이름을 hello를 사용 하는 경우 **ContosoKeyVault**의 hello 리소스 그룹 이름은 **ContosoResourceGroup**, 및의 hello 위치 **동아시아**, 유형:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

이 cmdlet의 출력 hello 방금 만든 hello 키 자격 증명 모음의 속성을 보여 줍니다. hello 두 가장 중요 한 속성은 같습니다.

* **자격 증명 모음에 이름**: hello 예에서이 **ContosoKeyVault**합니다. 다른 키 자격 증명 모음 cmdlet에 대해 이 이름을 사용합니다.
* **자격 증명 모음 URI**: hello 예제 https://contosokeyvault.vault.azure.net/입니다. REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.

Azure 계정에 권한이 부여 된 tooperform이이 키에 대 한 모든 작업 자격 증명 모음에 이제입니다. 아직 다른 사람은 권한이 없습니다.

> [!NOTE]
> Hello 오류가 나타나는 경우 **hello 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 'Microsoft.KeyVault'** toocreate 시도 하 여 새 키 자격 증명 모음을 실행 `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` 후 새로 AzureRmKeyVault 명령을 다시 실행 합니다. 자세한 내용은 [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)를 참조하세요.
>
>

## <a id="add"></a>키 또는 키 자격 증명 모음 보안 toohello 추가
Hello를 사용 하 여 Azure 키 자격 증명 모음 toocreate 소프트웨어 보호 키를 하려는 경우 [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet hello 다음을 입력 합니다.

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

그러나에 기존 소프트웨어 보호 키 있으면는 합니다. PFX 파일을 저장 tooyour C:\ 드라이브 softkey.pfx tooupload tooAzure 형식 hello tooset hello 변수 다음 주요 자격 증명을 지정 하 라는 파일에 **securepfxpwd** 의 암호에 대 한 **123** hello에 대 한 합니다. PFX 파일:

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Hello hello에서 다음 tooimport hello 키를 입력 합니다. 소프트웨어 키 자격 증명 모음 서비스 hello에서 hello 키를 보호 하 PFX 파일:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


이제는 작성 되거나 해당 URI를 사용 하 여 tooAzure 주요 자격 증명을 업로드 한이 키를 참조할 수 있습니다. 사용 하 여 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget이 특정 버전입니다.  

이 키 형식에 대 한 toodisplay hello URI:

    $Key.key.kid

먼저 tooadd는 비밀 toohello 자격 증명 모음 SQLPassword 라는 암호 이며 Pa$ $w0rd tooAzure 주요 자격 증명 모음 hello 값 hello 다음을 입력 하 여 Pa$ $w0rd tooa 보안 문자열의 hello 값을 변환:

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

그런 다음 hello 다음을 입력 합니다.

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

이제 해당 URI를 사용 하 여 tooAzure 자격 증명 모음 키를 추가 하는이 암호를 참조할 수 있습니다. 사용 하 여 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget이 특정 버전입니다.

이 암호 형식에 대 한 toodisplay hello URI:

    $secret.Id

Hello 키 또는 암호 방금 만든 보겠습니다.

* tooview 프로그램 키, 유형:`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview 비밀을 형식:`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

이제 주요 자격 증명 모음 및 키 또는 암호 응용 프로그램 toouse 준비가 되었습니다. 응용 프로그램 toouse에 권한을 부여 해야 해당 합니다.  

## <a id="register"></a>Azure Active Directory에 응용 프로그램 등록
이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다. 특정 tooAzure 주요 자격 증명 되지만 여기서는 완전성을 위해.

> [!IMPORTANT]
> toocomplete hello 자습서, 계정, 자격 증명 모음 hello 및이 단계에서 등록 하는 hello 응용 프로그램 모두에 있어야 hello 같은 Azure 디렉터리입니다.
>
>

자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다. toodo이,이 hello hello 응용 프로그램의 소유자가 Azure Active Directory에서 먼저 hello 응용 프로그램을 등록 해야 합니다. 등록의 hello 끝 hello 응용 프로그램 소유자 hello를 다음 값을 가져옵니다.

* **응용 프로그램 ID** (클라이언트 ID) 및 **인증 키** (라고도 hello 공유 암호). hello 응용 프로그램 둘 다 이러한 값 tooAzure Active Directory tooget 토큰을 제시 해야 합니다. Hello 응용 프로그램은 어떻게 구성 toodo hello 응용 프로그램에 따라 다릅니다. Hello 키 자격 증명 모음 샘플 응용 프로그램에 대 한 응용 프로그램 소유자 hello hello app.config 파일에 이러한 값을 설정합니다.

Azure Active Directory에서 tooregister hello 응용 프로그램:

1. Azure 클래식 포털 toohello에 로그인 합니다.
2. Hello 왼쪽에서 클릭 **Active Directory**, 한 다음 응용 프로그램을 등록 하는 hello 디렉터리를 선택 합니다. <br> <br> **참고:** hello를 선택 해야 포함 된 같은 디렉터리 hello 주요 자격 증명 모음을 만들 때 사용한 Azure 구독. 알 수 없는 디렉터리가 인지, 클릭 **설정**, 주요 자격 증명 모음을 만들 때 사용한 hello 구독을 식별 하 고 hello 디렉터리의 참고 hello 이름이 hello 마지막 열에 표시 합니다.
3. **APPLICATIONS**를 클릭합니다. 앱이 없습니다. tooyour 디렉터리를 추가한 경우이 페이지만 hello를 표시 하는 **앱 추가** 링크 합니다. Hello 링크를 클릭 하거나 클릭 수 있습니다 **추가** hello 명령 모음에서 합니다.
4. Hello에 **응용 프로그램 추가** hello에서 마법사 **하 신 toodo 원하는?** 페이지에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.
5. Hello에 **응용 프로그램에 대해 알리기** 페이지, 응용 프로그램에 대 한 이름을 지정 하 고 다음 선택 **웹 응용 프로그램 및/또는 웹 API** (기본 hello). Hello 클릭 **다음** 아이콘입니다.
6. Hello에 **앱 속성** 페이지에서 지정 하는 hello **로그온 URL** 및 **앱 ID URI** 웹 응용 프로그램에 대 한 합니다. 응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음). 이러한 사이트가 존재하는 경우 중요하지 않습니다. 중요 한 것은 각 응용 프로그램에 대 한 hello 앱 ID URI는 디렉터리의 모든 응용 프로그램에 대 한 다릅니다. hello 디렉터리는이 문자열 tooidentify 응용 프로그램을 사용합니다.
7. Hello 클릭 **완료** 아이콘 toosave hello 마법사에서 변경 내용을 합니다.
8. Hello에 **빠른 시작** 페이지 **구성**합니다.
9. Toohello 스크롤하여 **키** 섹션 hello 기간, 선택한 다음 클릭 **저장**합니다. hello 페이지가 새로 고쳐지고 키 값을 표시 합니다. 이 키 값 및 hello 응용 프로그램을 구성 해야 **클라이언트 ID** 값입니다. (이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)
10. 다음 단계 tooset 권한을 hello에서 사용할 자격 증명 모음에 있는이 페이지에서 hello 클라이언트 ID 값을 복사 합니다.

## <a id="authorize"></a>Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여
키 또는 암호에 hello 자격 증명 모음을 사용 하 여 tooauthorize hello 응용 프로그램 tooaccess hello는 [Set-azurermkeyvaultaccesspolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet.

예를 들어 자격 증명 모음 이름이 **ContosoKeyVault** 및 tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 중이 고 tooauthorize hello 응용 프로그램 toodecrypt 및 서명 된 키의 원하는 hello 응용 프로그램 자격 증명 모음을 hello 다음 실행:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

자격 증명 모음에는 동일한 응용 프로그램 tooread 비밀 tooauthorize 않으려면 hello 다음을 실행 합니다.

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>하드웨어 보안 모듈 (HSM) toouse 하려는 경우
추가 된 보증에 대 한 가져오기 또는 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다. hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다. 이 요구 사항을 tooyou을 적용 하지 않는 경우이 섹션을 건너뛰고 이동 너무[hello 주요 자격 증명 모음 및 연결 된 키와 비밀 삭제](#delete)합니다.

toocreate 이러한 HSM 보호 키 hello를 사용 해야 [Azure 키 자격 증명 모음 Premium 서비스 계층 toosupport HSM 보호 키](https://azure.microsoft.com/pricing/free-trial/)합니다. 또한 이 기능은 Azure 중국에 사용할 수 없습니다.

Hello 주요 자격 증명 모음을 만들 때 추가 hello **-SKU** 매개 변수:

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



소프트웨어 보호 키 (같이 이전) 및 HSM 보호 키 toothis 자격 증명 모음 키를 추가할 수 있습니다. toocreate는 HSM 보호 키 집합 hello **-대상** 매개 변수 too'HSM':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

다음 명령은 tooimport hello에서 키를 사용할 수 있습니다는 합니다. PFX 파일을 컴퓨터에 있습니다. 이 명령은 hello 키 자격 증명 모음 서비스에서에서 Hsm에 hello 키를 가져옵니다.

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


다음 명령은 hello "bring your own key"을 가져옵니다 (BYOK) 패키지 합니다. 이 시나리오를 사용 하 여 로컬 HSM의 키를 생성 한 후 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송할 수 있습니다.

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

자세한 방법에 대 한 지침은 toogenerate이 BYOK 패키지 참조 [어떻게 toogenerate 및 전송 HSM 보호 키 Azure 키 자격 증명 모음에 대 한](key-vault-hsm-protected-keys.md)합니다.

## <a id="delete"></a>Hello 주요 자격 증명 모음 및 연결 된 키와 비밀 정보를 삭제 합니다.
Hello 주요 자격 증명 모음 및 hello 키 또는 암호에 포함 된 더 이상 필요 하면 hello를 사용 하 여 hello 주요 자격 증명 모음을 삭제할 수 없습니다 [제거 AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

또는 hello 주요 자격 증명 모음 및 해당 그룹에 포함 된 다른 모든 리소스를 포함 하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>기타 Azure PowerShell Cmdlet
Azure 주요 자격 증명 모음을 관리하는 데 유용한 기타 명령은 다음과 같습니다.

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: 이 명령은 모든 키와 선택한 속성을 테이블 형식으로 가져옵니다.
* `$Keys[0]`:이 명령은 hello 지정 된 키에 대 한 속성의 전체 목록을 표시합니다
* `Get-AzureKeyVaultSecret`: 이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: 예제 어떻게 tooremove 특정 키입니다.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: 예제 어떻게 tooremove 특정 암호입니다.

## <a id="next"></a>다음 단계
웹 응용 프로그램에서 Azure 주요 자격 증명 모음을 사용하는 후속 자습서는 [웹 응용 프로그램에서 Azure 주요 자격 증명 모음 사용](key-vault-use-from-web-application.md)을 참조하세요.

toosee 주요 자격 증명 모음 사용 중인 참조 [Azure 키 자격 증명 모음 로깅](key-vault-logging.md)합니다.

목록이 hello Azure 키 자격 증명 모음에 대 한 최신 Azure PowerShell cmdlet에 대 한 참조 [Azure 키 자격 증명 모음 Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)합니다.

프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.
