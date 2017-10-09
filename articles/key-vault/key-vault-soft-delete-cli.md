---
ms.assetid: 
title: "키 자격 증명 모음 aaaAzure-CLI와 toouse 소프트 삭제 하는 방법"
description: "CLI 코드 캡처를 통한 일시 삭제의 사용 사례 예제"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a>CLI 키 자격 증명 모음 toouse 소프트-삭제 방법

Azure Key Vault의 일시 삭제 기능을 사용하면 삭제된 자격 증명 모음 및 자격 증명 모음 개체를 복구할 수 있습니다. 특히, 소프트 삭제 주소 hello 다음 시나리오:

- Key Vault의 복구 가능한 삭제 지원
- Key Vault 개체(예: 키, 비밀 및 인증서)의 복구 가능한 삭제를 지원

## <a name="prerequisites"></a>필수 조건

- Azure CLI 2.0 - 사용자 환경에 이 단계가 없는 경우 [CLI 2.0을 사용한 Key Vault 관리](key-vault-manage-with-cli2.md)를 참조하세요.

CLI에 대한 Key Vault 관련 특정 참조 정보는 [Azure CLI 2.0 Key Vault 참조](https://docs.microsoft.com/cli/azure/keyvault)를 참조하세요.

## <a name="required-permissions"></a>필요한 사용 권한

Key Vault 작업은 RBAC(역할 기반 액세스 제어) 권한을 통해 다음과 같이 별도로 관리됩니다.

| 작업 | 설명 | 사용자 권한 |
|:--|:--|:--|
|나열|삭제된 Key Vault를 나열합니다.|Microsoft.KeyVault/deletedVaults/read|
|복구|삭제된 Key Vault를 복구합니다.|Microsoft.KeyVault/vaults/write|
|제거|삭제된 Key Vault 및 모든 콘텐츠를 영구적으로 제거합니다.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

권한 및 액세스 제어에 대한 자세한 내용은 [Key Vault 보안](key-vault-secure-your-key-vault.md)을 참조하세요.

## <a name="enabling-soft-delete"></a>일시 삭제를 사용하도록 설정

toobe 수 toorecover 키에 저장 된 개체 또는 삭제 된 키 자격 증명 모음 자격 증명 모음, 해당 키 자격 증명 모음에 대 한 일시 삭제를 먼저 활성화 해야 합니다.

### <a name="existing-key-vault"></a>기존 Key Vault 사용

ContosoVault라는 기존 Key Vault의 경우 다음과 같이 일시 삭제를 사용하도록 설정합니다. 

>[!NOTE]
>Toouse Azure 리소스 관리자 리소스 조작 toodirectly 쓰기 hello 필요한 현재 *enableSoftDelete* 속성 toohello 주요 자격 증명 모음 리소스입니다.

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a>새로운 Key Vault

새 키 자격 증명 모음에 대 한 일시 삭제를 사용 하도록 설정 이루어집니다 hello 소프트 삭제 사용 플래그를 추가 하 여 생성 시 tooyour 만들기 명령입니다.

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a>일시 삭제 사용 확인

실행된 hello 주요 자격 증명 모음에 소프트 삭제가 활성화 tooverify *표시* ' 소프트 삭제 됨 ' hello에 대 한 찾은 명령 특성과 해당 설정(true 또는 false)을 찾습니다.

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>일시 삭제로 보호되는 Key Vault 삭제

hello 명령 toodelete (또는 제거) hello 동일 하지만 해당 동작 변경 내용 설정 여부에 따라 소프트 삭제 여부 주요 자격 증명 모음에 유지 됩니다.

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
>소프트 삭제 사용 하도록 설정 하지 않은 키 자격 증명 모음에 대 한 hello 이전 명령을 실행 하면이 주요 자격 증명 모음 및 복구에 대 한 옵션 없이 모든 내용이 영구적으로 삭제 됩니다.

### <a name="how-soft-delete-protects-your-key-vaults"></a>일시 삭제가 Key Vault를 보호하는 방식

활성화된 일시 삭제 사용:

- 키 자격 증명 모음 삭제 되 면 리소스 그룹에서 제거 하 고만 예약된 된 네임 스페이스에 배치 되는 만들어진 hello 위치와 연결 된입니다. 
- 개체 삭제 된 키에 액세스할 수 없는 키, 암호, 인증서, 같은 자격 증명 모음 및가 포함 된 주요 자격 증명 모음 삭제 hello 상태인 동안 서 항상 합니다. 
- 주요 자격 증명 모음 삭제 된 상태에서에 대 한 hello DNS 이름 이므로 계속 예약 되어, 동일한 이름 가진는 새 주요 자격 증명 모음을 만들 수 없습니다.  

다음 명령을 hello를 사용 하 여 삭제 된 상태 키 자격 증명 모음에 연결 된 구독을 볼 수 있습니다.

```azurecli
az keyvault list-deleted
```

hello *리소스 ID* 출력 hello에서이 자격 증명 모음의 toohello 원래 리소스 ID를 나타냅니다. 이제 이 Key Vault가 삭제된 상태로 있으므로 해당 리소스 ID를 사용하는 리소스가 없습니다. hello *Id* 필드에는 사용 되는 tooidentify hello 리소스, 복구 또는 제거 하는 경우 사용할 수 있습니다. hello *제거 날짜 예약* 필드 나타냅니다 경우 hello 자격 증명 모음 영구적으로 삭제 됩니다 (삭제) 아무 작업도이 삭제 된 자격 증명 모음에 대 한 합니다. hello 기본 보존 기간으로 사용 하는 toocalculate hello *제거 날짜 예약*, 90 일입니다.

## <a name="recovering-a-key-vault"></a>Key Vault 복구

주요 자격 증명 모음 toorecover toospecify hello 주요 자격 증명 모음 이름, 리소스 그룹 및 위치 해야합니다. 주요 자격 증명 모음 복구 프로세스에 대 한 이러한 필요에 따라 키 자격 증명 모음 삭제 하는 hello의 참고 hello 위치와 hello 리소스 그룹.

```azurecli
az keyvault recover --location westus --name ContosoVault
```

Hello 결과 hello 주요 자격 증명 모음의 원래 리소스 ID 사용 하 여 새 리소스는 주요 자격 증명 모음을 복구 하는 경우 Hello 주요 자격 증명 모음 존재 했던 hello 리소스 그룹을 제거한 경우 같은 이름의 새 리소스 그룹 만들어야 hello 주요 자격 증명 모음을 복구할 수 있습니다.

## <a name="key-vault-objects-and-soft-delete"></a>Key Vault 개체 및 일시 삭제

일시 삭제가 활성화되어 있는 ‘ContosoVault’라는 Key Vault의 ‘ContosoFirstKey’ 키의 경우 여기에 어떻게 해당 키를 삭제하는지가 나와 있습니다.

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

일시 삭제가 활성화되어 있는 Key Vault를 사용하면 삭제된 키를 명시적으로 나열하거나 검색할 때 외에는 삭제된 키가 여전히 삭제된 것으로 표시됩니다. Hello 삭제 된 상태에서 키에서 대부분의 작업은 삭제 된 키를 나열, 복구 또는 제거 하는 제외 하 고 실패 합니다. 

예를 들어, 주요 자격 증명 모음에 있는 toorequest 삭제 toolist 키 hello 다음 명령을 사용 합니다.

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a>전환 상태 

소프트 삭제 사용 하도록 설정 된 키 자격 증명 모음에 키를 삭제 하면 hello 전환 toocomplete 몇 초 정도 걸립니다. 이 전환 상태 hello 활성 상태 또는 삭제 하는 hello 상태에 해당 hello 키가이 나타납니다. 이 명령은 ‘ContosoVault’라는 Key Vault에 있는 모든 삭제된 키를 나열합니다.

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Key Vault 개체를 통해 일시 삭제 사용

키 자격 증명 모음 키를 삭제 된 처럼 암호 또는 인증서에에서 유지 됩니다 too90 (일) 삭제 된 상태에 대 한 복구 하거나 제거 하지 않으면. 

#### <a name="keys"></a>구성

toorecover 삭제 된 키:

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

toopermanently 키 삭제:

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
>키 제거는 키를 영구적으로 삭제하며 복구할 수 없습니다.

hello **복구** 및 **제거** 동작 사용 권한이 자신의 주요 자격 증명 모음 액세스 정책에 연결 합니다. 사용자 또는 서비스 보안 주체 toobe 수 tooexecute에 대 한 한 **복구** 또는 **제거** 작업 hello 주요 자격 증명 모음 액세스 정책에서 해당 개체 (키 또는 암호)에 대 한 해당 권한을 hello을 가져야 합니다. 기본적으로 hello **제거** hello 'all' 바로 가기는 사용 되는 toogrant 때 권한이 tooa 주요 자격 증명 모음의 액세스 정책 추가 되지 않습니다 모든 사용 권한 tooa 사용자입니다. **제거** 권한을 명시적으로 부여해야 합니다. 예를 들어 다음 명령은 부여 hello user@contoso.com 권한 tooperform 키에 대 한 여러 작업 *ContosoVault* 포함 하 여 **제거**합니다.

#### <a name="set-a-key-vault-access-policy"></a>Key Vault 액세스 정책 설정

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> 이제 막 일시 삭제 활성화되도록 기존 Key Vault를 설정한 경우 **복구** 및 **제거** 권한이 없을 수도 있습니다.

#### <a name="secrets"></a>비밀

키와 마찬가지로 Key Vault의 비밀도 자체 명령으로 작동됩니다. 다음, 삭제, 나열, 복구 및 암호의 한 제거에 대 한 hello 명령을 합니다.

- SQLPassword라는 비밀 삭제: 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- Key Vault의 모든 삭제된 비밀 나열: 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- Hello 삭제 상태에 암호 복구: 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- 삭제된 상태의 비밀 제거: 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
>비밀 제거는 비밀을 영구적으로 삭제하며 복구할 수 없습니다.

## <a name="purging-and-key-vaults"></a>제거 및 Key Vault

### <a name="key-vault-objects"></a>Key Vault 개체

키, 비밀 또는 인증서 제거는 해당 항목을 영구적으로 삭제하며 복구할 수 없습니다. 그러나 다른 모든 개체에 hello 주요 자격 증명 모음 됩니다에 hello 주요 자격 증명 모음 삭제 hello 개체를 포함 하는 그대로 유지 됩니다. 

### <a name="key-vaults-as-containers"></a>컨테이너로써의 Key Vault
Key Vault를 제거하면 키, 비밀 및 인증서를 포함한 모든 콘텐츠가 영구적으로 삭제됩니다. hello를 사용 하 여 주요 자격 증명 모음 toopurge `az keyvault purge` 명령입니다. 구독 삭제 된 키 자격 증명 모음 hello 명령을 사용 하 여 hello 위치를 찾을 수 있습니다 `az keyvault list-deleted`합니다.

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
>Key Vault 제거는 영구적으로 삭제하며 복구할 수 없습니다.

### <a name="purge-permissions-required"></a>제거 권한 필요
- 삭제 된 키 자격 증명 모음 toopurge hello 자격 증명 모음 및 모든 내용이 영구적으로 제거 되도록 hello 사용자에 게 필요한 권한이 tooperform RBAC는 *Microsoft.KeyVault/locations/deletedVaults/purge/action* 작업 합니다. 
- toolist 삭제 hello 키 hello 사용자 자격 증명 모음 필요한 RBAC 사용 권한을 tooperform *Microsoft.KeyVault/deletedVaults/read* 권한. 
- 기본적으로 구독 관리자만 이러한 권한을 갖습니다. 

### <a name="scheduled-purge"></a>예약된 제거

키 자격 증명 모음을 삭제 된 개체가 나열 schedled toobe 키 자격 증명 모음에서 제거 되 면 보여 줍니다. hello *제거 날짜 예약* 필드 이면 경우 키 자격 증명 모음 개체를 영구적으로 삭제 됩니다, 아무 작업도 수행 합니다. 기본적으로 키 자격 증명 모음을 삭제 된 개체에 대 한 보존 기간 hello은 90 일입니다.

>[!NOTE]
>해당 *예약된 제거 날짜* 필드에 의해 트리거되는 제거된 자격 증명 모음 개체가 영구적으로 삭제됩니다. 복구할 수는 없습니다.

## <a name="other-resources"></a>기타 리소스

- Key Vault의 일시 삭제 기능에 대한 자세한 내용은 [Azure Key Vault 일시 삭제 개요](key-vault-ovw-soft-delete.md)를 참조하세요.
- Azure Key Vault 사용의 일반적인 개요는 [Azure Key Vault 시작](key-vault-get-started.md)을 참조하세요.

