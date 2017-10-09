---
title: "CLI를 사용 하 여 Azure 키 자격 aaaManage | Microsoft Docs"
description: "키 자격 증명 모음에이 자습서 tooautomate 일반적인 작업을 사용 하 여 hello CLI 2.0을 사용 하 여"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a>CLI 2.0을 사용하여 Key Vault 관리
Azure 키 자격 증명 모음은 대부분 지역에서 사용할 수 있습니다. 자세한 내용은 참조 hello [키 자격 증명 모음 가격 책정 페이지](https://azure.microsoft.com/pricing/details/key-vault/)합니다.

## <a name="introduction"></a>소개
이 자습서 toohelp 얻게를 사용 하 여 toostore Azure에서 확정 된 컨테이너 (볼트)을 Azure 주요 자격 증명 모음 toocreate를 시작 하 고 암호화 키 및 Azure에서 암호 관리 합니다. 이 과정을 보여 줍니다 hello toocreate Azure 크로스 플랫폼 명령줄 인터페이스를 사용 하 여 키 또는 암호 Azure 응용 프로그램과 함께 사용할 수 있는 포함 된 자격 증명 모음입니다. 응용 프로그램이 수 해당 키 또는 암호를 사용할 수 있는 방법을 나타냅니다.

**예상 시간 toocomplete:** 20 분

> [!NOTE]
> 이 자습서는 toowrite Azure 응용 프로그램 hello 단계 중 하나를 포함 하는 방법을 tooauthorize 응용 프로그램 toouse 키 또는 암호에 hello 키 자격 증명 모음을 보여 주는 hello 하는 방법에 대 한 지침을 다루지 않습니다.
>
> 이 자습서에서는 최신 Azure CLI 2.0 hello 합니다.
>
>

Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)

## <a name="prerequisites"></a>필수 조건
toocomplete이이 자습서에서는 다음 hello 있어야 합니다.

* 구독 tooMicrosoft Azure 아직 구독하지 않은 경우 [무료 평가판](https://azure.microsoft.com/pricing/free-trial)에 등록할 수 있습니다.
* 명령줄 인터페이스 버전 2.0 이상. tooinstall 최신 버전을 hello 및 tooyour Azure 구독 연결 참조 [설치 및 구성 hello Azure 크로스 플랫폼 명령줄 인터페이스 2.0](/cli/azure/install-azure-cli)합니다.
* 응용 프로그램 구성된 toouse hello 키 또는 암호를이 자습서에서 만드는 됩니다입니다. 샘플 응용 프로그램은 hello에서 사용할 수 있는 [Microsoft 다운로드 센터](http://www.microsoft.com/download/details.aspx?id=45343)합니다. 추가 정보 파일을 함께 제공 된 hello를 참조 하십시오.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Azure 플랫폼 간 명령줄 인터페이스 도움말 보기
이 자습서에서는 hello 명령줄 인터페이스 (Bash, 터미널, 명령 프롬프트)에 익숙한 가정

hello-도움말 또는-h 매개 변수 수 특정 명령에 대 한 tooview 도움말을 사용 합니다. 또는 azure hello 도움말 [command] [옵션] 형식을 사용 하는 tooreturn 될 수도 있습니다 hello 동일한 정보입니다. 예를 들어 hello 다음 명령을 모두 반환 hello 동일한 정보:

```
az account set --help
az account set -h
```

명령에 필요한 hello 매개 변수에 대 한 의심 toohelp를 사용 하 여-참조 도움말,-h 또는 az help [명령].

Hello Azure 리소스 관리자의 Azure 플랫폼 간 명령줄 인터페이스와 친숙 한 자습서 tooget 다음 읽을 수 있습니다.

* [Azure CLI 설치](/cli/azure/install-azure-cli)
* [Azure CLI 2.0 시작](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a>Tooyour 구독 연결
다음 명령을 사용 하 여 hello 조직 계정을 사용 하 여 toolog:

```
az login -u username@domain.com -p password
```

대화형으로 입력 하 여에 toolog 포함 하려는 경우 또는

```
az login
```

구독이 여러 개 있고 Azure 키 자격 증명 모음에 대 한 특정 한 toouse toospecify 원하는 hello toosee hello 구독 계정에 대해 다음을 입력 합니다.

```
az account list
```

그런 다음 toospecify hello 구독 toouse, 유형:

```
az account set --subscription <subscription name or ID>
```

Azure 플랫폼 간 명령줄 인터페이스를 구성하는 방법에 대한 자세한 내용은 [Azure CLI 설치](/cli/azure/install-azure-cli)를 참조하세요.

## <a name="create-a-new-resource-group"></a>새 리소스 그룹 만들기
Azure 리소스 관리자를 사용하면 관련된 모든 리소스는 리소스 그룹의 내부에 만들어집니다. 이 자습서에서는 'ContosoResourceGroup'이라는 새 리소스 그룹을 만듭니다.

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

hello 첫 번째 매개 변수는 리소스 그룹 이름 및 hello 두 번째 매개 변수는 hello 위치 합니다. 위치에 대 한 hello 명령을 사용 하 여 `az account list-locations` tooidentify 어떻게 toospecify이 예에서 하나는 대체 위치 toohello 합니다. 자세한 정보가 필요한 경우 `az account list-locations -h`를 입력합니다.

## <a name="register-hello-key-vault-resource-provider"></a>Hello 주요 자격 증명 모음 리소스 공급자 등록
키 자격 증명 모음 리소스 공급자가 구독에 등록되어 있는지 확인합니다.

```
az provider register -n Microsoft.KeyVault
```

이 toobe 구독 당 한 번만 필요 합니다.

## <a name="create-a-key-vault"></a>키 자격 증명 모음 만들기
사용 하 여 hello `az keyvault create` 명령 toocreate 주요 자격 증명 모음입니다. 이 스크립트에 세 개의 필수 매개 변수: 리소스 그룹 이름, 주요 자격 증명 모음 이름 및 hello 지리적 위치입니다.

예를 들어 hello 자격 증명 모음 이름을 ContosoKeyVault, hello ContosoResourceGroup, 리소스 그룹 이름 및 동아시아의 hello 위치를 사용 하는 경우 입력 합니다.
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

이 명령의 출력 hello 방금 만든 hello 키 자격 증명 모음의 속성을 표시 합니다. hello 두 가장 중요 한 속성은 같습니다.

* **이름**: hello 예제 ContosoKeyVault입니다. 다른 Key Vault 명령에 이 이름을 사용합니다.
* **vaultUri**: hello 예제 https://contosokeyvault.vault.azure.net입니다. REST API를 통해 사용자 자격 증명 모음을 사용하는 응용 프로그램은 URI를 사용해야 합니다.

Azure 계정에 권한이 부여 된 tooperform이이 키에 대 한 모든 작업 자격 증명 모음에 이제입니다. 아직 다른 사람은 권한이 없습니다.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>키 또는 키 자격 증명 모음 보안 toohello 추가
Hello를 사용 하 여 Azure 키 자격 증명 모음 toocreate 소프트웨어 보호 키를 하려는 경우 `az key create` 명령을 실행 하 고 hello 다음을 입력 합니다.
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
그러나 softkey.pem tooupload tooAzure 주요 자격 증명 모음을 지정 하 라는 파일에 로컬 파일로 저장.pem 파일에 있는 기존 키가 있으면 hello hello에서 다음 tooimport hello 키를 입력 합니다. PEM 파일-hello 키 자격 증명 모음 서비스에에서는 소프트웨어에 의해 hello 키를 보호 합니다.
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
이제는 작성 되거나 해당 URI를 사용 하 여 tooAzure 주요 자격 증명을 업로드 한 hello 키를 참조할 수 있습니다. 사용 하 여 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways hello 현재 버전을 가져오고 **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget이 특정 버전입니다.

tooadd SQLPassword 라는 암호 되었으며 Pa$ $w0rd tooAzure 주요 자격 증명 유형 hello 뒤의 hello 값 비밀 toohello 자격:
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
이제 해당 URI를 사용 하 여 tooAzure 자격 증명 모음 키를 추가 하는이 암호를 참조할 수 있습니다. 사용 하 여 **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways hello 현재 버전을 가져오고 **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget이 특정 버전입니다.

Hello 키 또는 암호 방금 만든 보겠습니다.

* tooview 프로그램 키, 유형:`az keyvault key list --vault-name 'ContosoKeyVault'`
* tooview 비밀을 형식:`az keyvault secret list --vault-name 'ContosoKeyVault'`

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
2. Hello 왼쪽에서 클릭 **Azure Active Directory**, 한 다음 응용 프로그램을 등록 하는 hello 디렉터리를 선택 합니다. <br> <br> 

> [!Note] 
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
키 또는 암호 hello 자격 증명 모음을 사용 하 여 hello에 tooauthorize hello 응용 프로그램 tooaccess hello `az keyvault set-policy` 명령입니다.

예를 들어 자격 증명 모음 이름이 tooauthorize 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed의 클라이언트 ID가 중이 고 tooauthorize hello 응용 프로그램 toodecrypt 및 서명 키를 가진 자격 증명 모음에서 원하는 ContosoKeyVault 및 hello 응용 프로그램 이면 다음 실행 hello 다음:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

자격 증명 모음에는 동일한 응용 프로그램 tooread 비밀 tooauthorize 않으려면 hello 다음을 실행 합니다.
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>하드웨어 보안 모듈 (HSM) toouse 하려는 경우
추가 된 보증에 대 한 가져오기 또는 hello HSM 경계를 벗어날 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다. hello Hsm은 FIPS 140-2 수준 2 유효성을 검사 합니다. 이 요구 사항을 tooyou을 적용 하지 않는 경우이 섹션을 건너뛰고 이동 너무[hello 주요 자격 증명 모음 및 연결 된 키와 비밀 삭제](#delete-the-key-vault-and-associated-keys-and-secrets)합니다.

toocreate 이러한 HSM 보호 키를 지 원하는 HSM 보호 키 자격 증명 모음 구독이 있어야 합니다.

Hello keyvault를 만들 때 hello 'sku' 매개 변수를 추가 합니다.

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
(앞에서 보았듯이) 소프트웨어 보호 키를 추가 하 고 HSM 보호 키 toothis 자격 증명 모음 키를 누릅니다. toocreate는 HSM 보호 키 집합 hello 대상 매개 변수 too'HSM':

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

Hello 명령 tooimport 키.pem 파일을 컴퓨터에에서 다음을 사용할 수 있습니다. 이 명령은 hello 키 자격 증명 모음 서비스에서에서 Hsm에 hello 키를 가져옵니다.

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
다음 명령은 hello "bring your own key"을 가져옵니다 (BYOK) 패키지 합니다. 이렇게 하면 로컬 HSM의 키를 생성 하 여 hello HSM 경계를 종료 하는 hello 키 없이 tooHSMs hello 키 자격 증명 모음 서비스에에서 전송 합니다.

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
자세한 방법에 대 한 지침은 toogenerate이 BYOK 패키지 참조 [어떻게 toouse HSM-Protected 키는 Azure 키 자격 증명](key-vault-hsm-protected-keys.md)합니다.

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Hello 주요 자격 증명 모음 및 연결 된 키와 비밀 정보를 삭제 합니다.
Hello 주요 자격 증명 모음 및 hello 키 또는 암호에 포함 된 더 이상 필요 하면 hello를 사용 하 여 hello 주요 자격 증명 모음을 삭제할 수 없습니다 `az keyvault delete` 명령:

```
az keyvault delete --name 'ContosoKeyVault'
```

또는 hello 주요 자격 증명 모음 및 해당 그룹에 포함 된 다른 모든 리소스를 포함 하는 전체 Azure 리소스 그룹을 삭제할 수 있습니다.

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a>다른 Azure 플랫폼 간 명령줄 인터페이스 명령
Azure 키 자격 증명 모음을 관리하는 데 유용할 수 있는 다른 명령입니다.

이 명령은 모든 키와 선택한 속성을 테이블 형식으로 나열합니다.

az keyvault key list --vault-name 'ContosoKeyVault'

이 명령은 hello 지정 된 키에 대 한 속성의 전체 목록을 표시합니다.

az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

이 명령은 모든 비밀 이름과 선택한 속성을 테이블 형식으로 표시합니다.

az keyvault secret list --vault-name 'ContosoKeyVault'

방법의 예로 특정 키 tooremove:

az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

방법의 예로 특정 보안 tooremove:

az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'


## <a name="next-steps"></a>다음 단계
Key Vault 명령에 대한 전체 Azure CLI 참조에 대해서는 [Key Vault CLI 참조](/cli/azure/keyvault)를 참조하세요.

프로그래밍 참조에 대 한 참조 [Azure 키 자격 증명 모음 개발자 가이드 hello](key-vault-developers-guide.md)합니다.
