---
title: "CLI를 사용 하 여 Azure 키 자격 aaaManage | Microsoft Docs"
description: "키 자격 증명 모음에이 자습서 tooautomate 일반적인 작업을 사용 하 여 hello CLI를 사용 하 여"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>CLI를 사용하여 키 자격 증명 모음 관리

Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다. 자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.

## <a name="introduction"></a>소개

이 자습서 toohelp 얻게를 사용 하 여 toostore Azure에서 확정 된 컨테이너 (볼트)을 Azure 주요 자격 증명 모음 toocreate를 시작 하 고 암호화 키 및 Azure에서 암호 관리 합니다. 이 과정을 보여 줍니다 hello toocreate Azure 크로스 플랫폼 명령줄 인터페이스를 사용 하 여 키 또는 암호 Azure 응용 프로그램과 함께 사용할 수 있는 포함 된 자격 증명 모음입니다. 응용 프로그램이 수 해당 키 또는 암호를 사용할 수 있는 방법을 나타냅니다.

**예상 시간 toocomplete:** 20 분

> [!NOTE]
> 이 자습서는 toowrite Azure 응용 프로그램 hello 단계 중 하나를 포함 하는 방법을 tooauthorize 응용 프로그램 toouse 키 또는 암호에 hello 키 자격 증명 모음을 보여 주는 hello 하는 방법에 대 한 지침을 다루지 않습니다.
> 
> 현재 hello Azure 포털에서에서 Azure 키 자격 증명 모음을 구성할 수 없습니다. 대신 이러한 플랫폼 간 명령줄 인터페이스 지침을 사용합니다. 또는 Azure PowerShell 지침의 경우 [이 자습서](key-vault-get-started.md)를 참조합니다.
> 
> 

Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)

## <a name="prerequisites"></a>필수 조건

toocomplete이이 자습서에서는 다음 hello 있어야 합니다.

* 구독 tooMicrosoft Azure 아직 구독하지 않은 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.
* 명령줄 인터페이스 버전 0.9.1 이상. tooinstall 최신 버전을 hello 및 tooyour Azure 구독 연결 참조 [설치 및 구성 hello Azure 크로스 플랫폼 명령줄 인터페이스](../cli-install-nodejs.md)합니다.
* 응용 프로그램 구성된 toouse hello 키 또는 암호를이 자습서에서 만드는 됩니다입니다. 샘플 응용 프로그램은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=45343)합니다. 추가 정보 파일을 함께 제공 된 hello를 참조 하십시오.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Azure 플랫폼 간 명령줄 인터페이스 도움말 보기

이 자습서에서는 hello 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트)에 익숙한 가정

hello-도움말 또는-h 매개 변수 수 특정 명령에 대 한 tooview 도움말을 사용 합니다. 또는 azure hello 도움말 [command] [옵션] 형식을 사용 하는 tooreturn 될 수도 있습니다 hello 동일한 정보입니다. 예를 들어 hello 다음 명령을 모두 반환 hello 동일한 정보:

    azure account set --help

    azure account set -h

    azure help account set

명령에 필요한 hello 매개 변수에 대 한 의심 toohelp를 사용 하 여-참조 도움말,-h 또는 azure 도움말 [command].

Hello Azure 리소스 관리자의 Azure 플랫폼 간 명령줄 인터페이스와 친숙 한 자습서 tooget 다음 읽을 수 있습니다.

* [어떻게 tooinstall 및 Azure 플랫폼 간 명령줄 인터페이스를 구성 합니다.](../cli-install-nodejs.md)
* [Azure 리소스 관리자와 함께 Azure 플랫폼 간 명령줄 인터페이스 사용](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>Tooyour 구독 연결

다음 명령을 사용 하 여 hello 조직 계정을 사용 하 여 toolog:

    azure login -u username -p password

대화형으로 입력 하 여에 toolog 포함 하려는 경우 또는

    azure login

> [!NOTE]
> hello 로그인 메서드 조직 계정 에서만 작동합니다. 조직 계정은 조직에서 관리되고 조직 Azure Active Directory 테넌트에 정의된 사용자입니다.
> 
> 

현재 조직 계정이 없는 Microsoft 계정 toolog tooyour Azure 구독에서에서 사용 하는 경우 쉽게 만들 수 있습니다 하나를 사용 하 여 다음 단계 hello 합니다.

1. 로그인 toohello 로그인 toohello [Azure 관리 포털](https://manage.windowsazure.com/), Active Directory에서을 클릭 합니다.
2. 디렉터리가 있으면 디렉터리 만들기 하 고 제공 hello 요청 된 정보입니다.
3. 디렉터리를 선택하고 새 사용자를 추가합니다. 새 사용자는 조직 계정입니다. Hello 사용자의 hello 만드는 동안 hello 사용자에 대 한 전자 메일 주소 및 임시 암호를 모두 함께 제공 됩니다. 이 정보는 다른 단계에서 사용되므로 저장해 두십시오.
4. Hello 포털에서 설정을 선택 하 고 관리자를 선택 합니다. 추가 선택 하 고 공동 관리자로 hello 새 사용자를 추가 합니다. 이렇게 하면 hello 조직 계정 toomanage Azure 구독.
5. 마지막으로, 로그 아웃 hello Azure 포털 한 다음 다시 로그인 hello 새 조직 계정을 사용 하 여 합니다. 이이 계정 사용 하 여 처음 로그온 hello, 입력 정보 요청된 toochange hello 암호 됩니다.

Microsoft Azure의 조직 계정 사용에 대한 자세한 내용은 [조직으로 Microsoft Azure에 등록](../active-directory/sign-up-organization.md)을 참조하세요.

구독이 여러 개 있고 Azure 키 자격 증명 모음에 대 한 특정 한 toouse toospecify 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.

    azure account list

그런 다음 toospecify hello 구독 toouse, 유형:

    azure account set <subscription name>

Azure 플랫폼 간 명령줄 인터페이스를 구성 하는 방법에 대 한 자세한 내용은 참조 [어떻게 tooInstall Azure 크로스 플랫폼 명령줄 인터페이스를 구성 하 고](../cli-install-nodejs.md)합니다.

## <a name="switch-toousing-azure-resource-manager"></a>스위치 toousing Azure 리소스 관리자
hello 키 자격 증명 모음에 Azure 리소스 관리자가 필요 하므로 hello tooswitch tooAzure Resource Manager 모드를 다음을 입력 합니다.

    azure config mode arm

## <a name="create-a-new-resource-group"></a>새 리소스 그룹 만들기
Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다. 이 자습서에서는 'ContosoResourceGroup'이라는 새 리소스 그룹을 만듭니다.

    azure group create 'ContosoResourceGroup' 'East Asia'

hello 첫 번째 매개 변수는 리소스 그룹 이름 및 hello 두 번째 매개 변수는 hello 위치 합니다. 위치에 대 한 hello 명령을 사용 하 여 `azure location list` tooidentify 어떻게 toospecify이 예에서 하나는 대체 위치 toohello 합니다. 자세한 정보가 필요한 경우 `azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>Hello 주요 자격 증명 모음 리소스 공급자 등록
키 자격 증명 모음 리소스 공급자가 구독에 등록되어 있는지 확인합니다.

`azure provider register Microsoft.KeyVault`

이 toobe 구독 당 한 번만 필요 합니다.

## <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기

사용 하 여 hello `azure keyvault create` 명령 toocreate 주요 자격 증명 모음입니다. 이 스크립트에 세 개의 필수 매개 변수: 리소스 그룹 이름, 주요 자격 증명 모음 이름 및 hello 지리적 위치입니다.

예를 들어 hello 자격 증명 모음 이름을 ContosoKeyVault, hello ContosoResourceGroup, 리소스 그룹 이름 및 동아시아의 hello 위치를 사용 하는 경우 입력 합니다.

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

이 명령의 출력 hello 방금 만든 hello 키 자격 증명 모음의 속성을 표시 합니다. hello 두 가장 중요 한 속성은 같습니다.

* **이름**: hello 예제 ContosoKeyVault입니다. 다른 키 자격 증명 모음 cmdlet에 대해 이 이름을 사용합니다.
* **vaultUri**: hello 예제 https://contosokeyvault.vault.azure.net입니다. REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.

Azure 계정에 권한이 부여 된 tooperform이이 키에 대 한 모든 작업 자격 증명 모음에 이제입니다. 아직 다른 사람은 권한이 없습니다.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>키 또는 키 자격 증명 모음 보안 toohello 추가

Hello를 사용 하 여 Azure 키 자격 증명 모음 toocreate 소프트웨어 보호 키를 하려는 경우 `azure key create` 명령을 실행 하 고 hello 다음을 입력 합니다.

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

그러나 softkey.pem tooupload tooAzure 주요 자격 증명 모음을 지정 하 라는 파일에 로컬 파일로 저장.pem 파일에 있는 기존 키가 있으면 hello hello에서 다음 tooimport hello 키를 입력 합니다. PEM 파일-hello 키 자격 증명 모음 서비스에에서는 소프트웨어에 의해 hello 키를 보호 합니다.

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

이제는 작성 되거나 해당 URI를 사용 하 여 tooAzure 주요 자격 증명을 업로드 한 hello 키를 참조할 수 있습니다. 사용 하 여 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget이 특정 버전입니다.

tooadd SQLPassword 라는 암호 되었으며 Pa$ $w0rd tooAzure 주요 자격 증명 유형 hello 뒤의 hello 값 비밀 toohello 자격:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

이제 해당 URI를 사용 하 여 tooAzure 자격 증명 모음 키를 추가 하는이 암호를 참조할 수 있습니다. 사용 하 여 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget이 특정 버전입니다.

Hello 키 또는 암호 방금 만든 보겠습니다.

* tooview 프로그램 키, 유형:`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview 비밀을 형식:`azure keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Azure Active Directory에 응용 프로그램 등록

이 단계는 일반적으로 별도의 컴퓨터에서 개발자가 수행할 수 있습니다. 특정 tooAzure 주요 자격 증명 모음 되지만 완전성을 위해 여기에서 포함 됩니다.

> [!IMPORTANT]
> toocomplete hello 자습서, 계정, 자격 증명 모음 hello 및이 단계에서 등록 하는 hello 응용 프로그램 모두에 있어야 hello 같은 Azure 디렉터리입니다.
> 
> 

자격 증명 모음 키를 사용하는 응용 프로그램은 Azure Active Directory에서 토큰을 사용하여 인증해야 합니다. toodo이,이 hello hello 응용 프로그램의 소유자가 Azure Active Directory에서 먼저 hello 응용 프로그램을 등록 해야 합니다. 등록의 hello 끝 hello 응용 프로그램 소유자 hello를 다음 값을 가져옵니다.

* **응용 프로그램 ID** (클라이언트 ID) 및 **인증 키** (라고도 hello 공유 암호). hello 응용 프로그램에는 모두 이러한 값 tooAzure Active Directory tooget 토큰을 제시 해야 합니다. Hello 응용 프로그램은 어떻게 구성 toodo hello 응용 프로그램에 따라 다릅니다. Hello 키 자격 증명 모음 샘플 응용 프로그램에 대 한 응용 프로그램 소유자 hello hello app.config 파일에 이러한 값을 설정합니다.

Azure Active Directory에서 tooregister hello 응용 프로그램:

1. Azure 포털 toohello에 로그인 합니다.
2. Hello 왼쪽에서 클릭 **Active Directory**, 한 다음 응용 프로그램을 등록 하는 hello 디렉터리를 선택 합니다. <br> <br> 

>[!NOTE] 
> Hello를 선택 해야 포함 된 같은 디렉터리 hello 주요 자격 증명 모음을 만들 때 사용한 Azure 구독. 알 수 없는 디렉터리가 인지, 클릭 **설정**, 주요 자격 증명 모음을 만들 때 사용한 hello 구독을 식별 하 고 hello 디렉터리의 참고 hello 이름이 hello 마지막 열에 표시 합니다.

3. **APPLICATIONS**를 클릭합니다. 이 페이지 hello만 표시 됩니다 앱이 없습니다. tooyour 디렉터리를 추가한 경우 **앱 추가** 링크 합니다. Hello 링크를 클릭 하거나 hello 클릭 해도, **추가** hello 명령 모음에서 합니다.
4. Hello에 **응용 프로그램 추가** hello에서 마법사 **하 신 toodo 원하는?** 페이지에서 클릭 **조직에서 개발 중인 응용 프로그램 추가**합니다.
5. Hello에 **응용 프로그램에 대해 알리기** 페이지 응용 프로그램에 대 한 이름을 지정 하 고 선택 **웹 응용 프로그램 및/또는 웹 API** (기본 hello). Hello 다음 아이콘을 클릭 합니다.
6. Hello에 **앱 속성** 페이지에서 지정 하는 hello **로그온 URL** 및 **앱 ID URI** 웹 응용 프로그램에 대 한 합니다. 응용 프로그램에 이러한 값이 없는 경우 이 단계에서 만들 수 있습니다(예를 들어, 두 상자에 대해 http://test1.contoso.com을 지정할 수 있음). 이러한 사이트 존재 하는 경우 중요 하지 않습니다. 중요 한 것은 각 응용 프로그램에 대 한 hello 앱 ID URI는 디렉터리의 모든 응용 프로그램에 대 한 다릅니다. hello 디렉터리는이 문자열 tooidentify 응용 프로그램을 사용합니다.
7. Hello 완료 아이콘 toosave hello 마법사에서 변경 내용을 클릭 합니다.
8. Hello 빠른 시작 페이지에서 클릭 **구성**합니다.
9. Toohello 스크롤하여 **키** 섹션 hello 기간, 선택한 다음 클릭 **저장**합니다. hello 페이지가 새로 고쳐지고 키 값을 표시 합니다. 이 키 값 및 hello 응용 프로그램을 구성 해야 **클라이언트 ID** 값입니다. (이 구성에 대한 지침은 응용 프로그램에 특정된 것입니다.)
10. 다음 단계 tooset 권한을 hello에서 사용할 자격 증명 모음에 있는이 페이지에서 hello 클라이언트 ID 값을 복사 합니다.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Hello 응용 프로그램 toouse hello 키 또는 암호를 권한 부여
키 또는 암호 hello 자격 증명 모음을 사용 하 여 hello에 tooauthorize hello 응용 프로그램 tooaccess hello `azure keyvault set-policy` 명령입니다.

예를 들어 자격 증명 모음 이름이 tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 중이 고 tooauthorize hello 응용 프로그램 toodecrypt 및 서명 키를 가진 자격 증명 모음에서 원하는 ContosoKeyVault 및 hello 응용 프로그램 이면 다음 실행 hello 다음:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> Windows 명령 프롬프트에서 실행 하는 경우에 큰따옴표를 작은따옴표로 바꿉니다 고도 hello 내부 큰따옴표를 이스케이프 해야 합니다. 예: "[\"해독\",\"기호\"]"
> 
> 

자격 증명 모음에는 동일한 응용 프로그램 tooread 비밀 tooauthorize 않으려면 hello 다음을 실행 합니다.

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>하드웨어 보안 모듈 (HSM) toouse 하려는 경우
추가 된 보증에 대 한 가져오기 또는 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다. hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다. 이 요구 사항을 tooyou을 적용 하지 않는 경우이 섹션을 건너뛰고 이동 너무[hello 주요 자격 증명 모음 및 연결 된 키와 비밀 삭제](#delete-the-key-vault-and-associated-keys-and-secrets)합니다.

toocreate 이러한 HSM 보호 키를 지 원하는 HSM 보호 키 자격 증명 모음 구독이 있어야 합니다.

Hello keyvault를 만들 때 hello 'sku' 매개 변수를 추가 합니다.

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

(앞에서 보았듯이) 소프트웨어 보호 키를 추가 하 고 HSM 보호 키 toothis 자격 증명 모음 키를 누릅니다. toocreate는 HSM 보호 키 집합 hello 대상 매개 변수 too'HSM':

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

Hello 명령 tooimport 키.pem 파일을 컴퓨터에에서 다음을 사용할 수 있습니다. 이 명령은 hello 키 자격 증명 모음 서비스에서에서 Hsm에 hello 키를 가져옵니다.

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

다음 명령은 hello "bring your own key"을 가져옵니다 (BYOK) 패키지 합니다. 이렇게 하면 로컬 HSM의 키를 생성 하 여 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송 합니다.

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

자세한 방법에 대 한 지침은 toogenerate이 BYOK 패키지 참조 [어떻게 toouse HSM-Protected 키는 Azure 키 자격 증명](key-vault-hsm-protected-keys.md)합니다.

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Hello 주요 자격 증명 모음 및 연결 된 키와 비밀 정보를 삭제 합니다.
Hello 주요 자격 증명 모음 및 hello 키 또는 암호에 포함 된 더 이상 필요 하면 azure hello keyvault delete 명령을 사용 하 여 hello 주요 자격 증명 모음을 삭제할 수 없습니다.

    azure keyvault delete --vault-name 'ContosoKeyVault'

또는 hello 주요 자격 증명 모음 및 해당 그룹에 포함 된 다른 모든 리소스를 포함 하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>다른 Azure 플랫폼 간 명령줄 인터페이스 명령
Azure 키 자격 증명 모음을 관리하는 데 유용할 수 있는 다른 명령입니다.

이 명령은 모든 키와 선택한 속성을 테이블 형식으로 나열합니다.

    azure keyvault key list --vault-name 'ContosoKeyVault'

이 명령은 hello 지정 된 키에 대 한 속성의 전체 목록을 표시합니다.

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.

    azure keyvault secret list --vault-name 'ContosoKeyVault'

방법의 예로 특정 키 tooremove:

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

방법의 예로 특정 보안 tooremove:

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>다음 단계
프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.

