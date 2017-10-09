---
title: "hello Azure CLI 1.0을 사용 하 여 Linux VM에서 aaaEncrypt 디스크 | Microsoft Docs"
description: "Tooencrypt 디스크를 사용 하 여 Linux VM에 Azure CLI 1.0 및 hello 리소스 관리자 배포 모델을 hello 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0을 사용 하 여 Linux VM에서 디스크를 암호화 합니다.
가상 컴퓨터(VM)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 미사용 시 암호화할 수 있습니다. 디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다. 이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다. 이 문서 tooencrypt 가상 디스크를 사용 하 여 Linux VM에 Azure CLI 1.0 및 hello 리소스 관리자 배포 모델을 hello 하는 방법을 설명 합니다.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 버전 toocomplete hello 작업
Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 수행할 수 있습니다.

- [Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한

## <a name="quick-commands"></a>빠른 명령
Hello 작업을 수행 tooquickly 해야 할 경우에 다음 섹션의 세부 정보 hello 기본 hello tooencrypt 가상 디스크를 VM에 명령, 합니다. 각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#overview-of-disk-encryption)합니다.

Hello 필요한 [최신 Azure CLI 1.0](../../xplat-cli-install.md) 설치 하 고 다음과 같이 hello Resource Manager 모드를 사용 하 여 로그인 합니다.

```azurecli
azure config mode arm
```

Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에 `myResourceGroup`, `myKeyVault` 및 `myVM`이 포함됩니다.

먼저, Azure 구독 내 hello Azure 키 자격 증명 모음 공급자를 사용 하도록 설정 하 고 리소스 그룹을 만듭니다. hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 `myResourceGroup` hello에 `WestUS` 위치:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Azure Key Vault를 만듭니다. hello 다음 예제에서는 키 자격 증명 모음 이름이 `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Key Vault에 암호화 키를 만들고 디스크 암호화에 사용하도록 설정합니다. hello 다음 예제에서는 라는 키 `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Azure Active Directory를 사용 하 여 hello 인증을 처리 하 고 주요 자격 증명 모음에서 암호화 키를 교환 하 고 끝점을 만듭니다. hello `--home-page` 및 `--identifier-uris` toobe 실제 라우팅할 수 있는 주소가 필요는 없습니다. Hello 가장 높은 수준의 보안을 위해 암호 대신 클라이언트 암호를 사용 해야 합니다. hello Azure CLI 클라이언트 암호를 현재 생성할 수 없습니다. 클라이언트 암호 hello Azure 포털에에서만 생성할 수 있습니다. hello 다음 예제에서는 끝점을 만들고 Azure Active Directory 라는 `myAADApp` 의 암호를 사용 하 여 `myPassword`합니다. 다음과 같이 사용자 고유의 암호를 지정합니다.

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

참고 hello `applicationId` hello 명령 앞의 hello 출력에 표시 된 것입니다. 이 응용 프로그램 ID는 단계를 수행 하는 hello에 사용 됩니다.

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

기존 VM 데이터 디스크 tooan를 추가 합니다. hello 다음 예제에서는 추가 데이터 디스크 tooa 라는 VM `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

만든 키 자격 증명 모음과 hello 키에 대해 hello 세부 정보를 검토 합니다. 키 자격 증명 모음 ID, URI 및 키 hello 필요 hello 마지막 단계에 대 한 URL입니다. hello 다음 예제에서는 검토 hello 세부 정보 라는 키 자격 증명 모음에 대 한 `myKeyVault` 및 라는 키 `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

사용자 고유의 매개 변수 이름을 입력하여 다음과 같이 디스크를 암호화합니다.

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

hello Azure CLI hello 암호화 프로세스 동안 자세한 오류가 제공 하지 않습니다. 추가적인 문제 해결 정보는 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`를 참조하세요. 에 여러 변수를 명령 앞으로 hello 및 많은 표시 as toowhy hello 프로세스 실패를 얻지 못할 수도 있습니다, 전체 명령 예는 다음과 같은 것:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello 암호화 상태를 검토 하는 마지막으로, 가상 디스크 암호화 이제 tooconfirm 다시 합니다. hello 다음 예제에서는 상태를 검사 hello 라는 VM의 `myVM` hello에 `myResourceGroup` 리소스 그룹:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>디스크 암호화 개요
Linux VM의 가상 디스크는 미사용 시 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt)를 사용하여 암호화됩니다. Azure에서 가상 디스크 암호화는 무료입니다. 암호화 키가 소프트웨어 보호를 사용 하 여 Azure 키 자격 증명 모음에 저장 하거나 가져오거나 140-2 수준 2 표준 tooFIPS 인증 된 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다. 이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다. 이러한 암호화 한 키를 사용 하는 tooencrypt 가상 디스크 연결 된 tooyour VM의 암호를 해독 합니다. Azure Active Directory 끝점은 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.

VM을 암호화 하기 위한 hello 프로세스는 다음과 같습니다.

1. Azure Key Vault에서 암호화 키를 만듭니다.
2. 암호화 키 toobe hello 디스크를 암호화 하는 데 사용할 수 있는 구성 합니다.
3. hello Azure 키 자격 증명 모음에서에서 tooread hello 암호화 키 hello 적절 한 권한이 있는 Azure Active Directory를 사용 하 여 끝점을 만듭니다.
4. Hello 명령 tooencrypt hello Azure Active Directory 끝점 및 적절 한 암호화 키 toobe 사용을 지정 하 여 가상 디스크를 실행 합니다.
5. Azure Active Directory 끝점 hello Azure 키 자격 증명 모음에서 hello 필요한 암호화 키를 요청합니다.
6. hello 가상 디스크는 암호화 키를 제공 하는 hello를 사용 하 여 암호화 됩니다.

## <a name="supporting-services-and-encryption-process"></a>지원 서비스 및 암호화 프로세스
다음과 같은 추가 구성 요소가 hello 디스크 암호화를 사용 합니다.

* **Azure 키 자격 증명 모음** -toosafeguard 암호화 키 및 hello 디스크 암호화/암호 해독 프로세스에 사용 되는 암호를 사용 합니다.
  * 이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다. 없는 toodedicate 주요 자격 증명 모음 tooencrypting 디스크.
  * tooseparate 관리 범위 및 키 가시성 전용된 키 자격 증명 모음을 만들 수 있습니다.
* **Azure Active Directory** -핸들 hello 필요한 암호화 키의 보안 교환 및 인증에 대 한 작업을 요청 합니다.
  * 일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.
  * hello 응용 프로그램이 이상의 hello 주요 자격 증명 모음에 대 한 끝점 및 가상 컴퓨터 서비스 toorequest 및 get hello 적절 한 암호화 키를 발급 합니다. Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.

## <a name="requirements-and-limitations"></a>요구 사항 및 제한 사항
디스크 암호화에 대해 지원되는 시나리오 및 요구 사항은 다음과 같습니다.

* Linux 서버 Sku-Ubuntu, CentOS, SUSE 및 SUSE Linux Enterprise Server (SLES), 및 Red Hat Enterprise Linux 다음 번호입니다.
* 모든 리소스 (예: 키 자격 증명 모음, 저장소 계정 및 VM) hello에 있어야 합니다. 같은 Azure 지역 및 구독 합니다.
* 표준 A, D, DS, G 및 GS 시리즈 VM.

디스크 암호화 hello 다음 시나리오에서에서 현재 지원 되지 않습니다.

* 기본 계층 VM.
* Hello 클래식 배포 모델을 사용 하 여 만든 Vm입니다.
* Linux VM에서 OS 디스크 암호화 비활성화.
* Hello 이미 암호화 된 Linux VM에서 암호화 키를 업데이트합니다.

## <a name="create-hello-azure-key-vault-and-keys"></a>만들 hello Azure 키 자격 증명 모음 및 키
hello 해야 toocomplete hello이이 가이드의 나머지 부분을 [최신 Azure CLI 1.0](../../xplat-cli-install.md) 설치 하 고 다음과 같이 hello Resource Manager 모드를 사용 하 여 로그인 합니다.

```azurecli
azure config mode arm
```

Hello 명령 예에서는 전체에서 고유한 이름, 위치 및 키 값으로 모든 예제에서는 매개 변수를 대체 합니다. hello 다음 예에서는 사용의 규칙 `myResourceGroup`, `myKeyVault`, `myAADApp`등입니다.

hello 첫 번째 단계는 Azure 키 자격 증명 모음 toostore toocreate 암호화 키입니다. Azure 주요 자격 증명, 비밀 키를 저장할 수 있습니다 또는 암호 toosecurely를 허용 하는 응용 프로그램 및 서비스에 구현 합니다. 가상 디스크 암호화에 대 한 주요 자격 증명 모음 toostore tooencrypt 사용된 되는 암호화 키를 사용 하거나 가상 디스크의 암호를 해독 합니다.

Azure 구독에서 hello Azure 키 자격 증명 모음 공급자 사용 후 리소스 그룹을 만듭니다. hello 다음 예제에서는 명명 된 리소스 그룹 `myResourceGroup` hello에 `WestUS` 위치:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

hello Azure 키 자격 증명 모음 포함 hello 암호화 키와 연결 된 계산 hello VM 자체 저장소 같은 리소스에 있어야 합니다. 동일한 지역을 hello 합니다. hello 다음 만드는 예제는 Azure 키 자격 증명 모음 이름이 `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다. HSM을 사용하려면 프리미엄 Key Vault가 필요합니다. 소프트웨어 보호 키를 저장 하는 표준 주요 자격 증명 모음 보다는 주요 자격 증명 모음 프리미엄은 추가 비용 toocreating 합니다. hello 앞 단계에서에서 프리미엄 주요 자격 증명 추가 toocreate `--sku Premium` toohello 명령입니다. hello 다음 예제에서는 소프트웨어 보호 키 이후 표준 주요 자격 증명 모음을 만들었습니다.

두 보호 모델에 대 한 hello Azure 플랫폼 toobe hello VM toodecrypt hello 가상 디스크를 부팅 될 때 액세스 toorequest hello에 대 한 암호화 키에 부여 해야 합니다. Key Vault 내에서 암호화 키를 만든 후 가상 디스크 암호화에 사용할 수 있도록 설정합니다. hello 다음 예제에서는 라는 키 `myKey` 다음 디스크 암호화를 사용 하도록 설정 하 고 있습니다.

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Hello Azure Active Directory 응용 프로그램 만들기
가상 디스크를 암호화 하거나 암호를 해독할 때 toohandle hello 인증 끝점 및 키 자격 증명 모음에서 암호화 키의 교환 사용 합니다. 이 끝점으로 Azure Active Directory 응용 프로그램 hello Azure 플랫폼 toorequest hello VM hello 대신 하 여 적절 한 암호화 키를 수 있습니다. 기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.

전체 Azure Active Directory 응용 프로그램을 만들지 않고 대로 hello `--home-page` 및 `--identifier-uris` hello 다음 예제에서에서 매개 변수 toobe 실제 라우팅할 수 있는 주소가 필요는 없습니다. hello 다음 예제에서는 또한 암호 기반 보안 대신 지정 hello Azure 포털 내에서 키를 생성 합니다. 이 시간으로 Azure CLI hello에서 키 생성을 수행할 수 없습니다.

Azure Active Directory 응용 프로그램을 만듭니다. hello 다음 예제에서는 응용 프로그램을 만듭니다 라는 `myAADApp` 의 암호를 사용 하 여 `myPassword`합니다. 다음과 같이 사용자 고유의 암호를 지정합니다.

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Hello 메모 `applicationId` hello 명령 앞에서 hello 출력에 반환 되는 합니다. 이 응용 프로그램 ID는 hello 나머지 단계 중 일부에 사용 됩니다. 다음으로 hello 응용 프로그램은 사용자 환경 내에서 액세스할 수 있도록 서비스 사용자 이름 (SPN)을 만듭니다. toosuccessfully 암호화 또는 가상 디스크를 암호 해독, 키 자격 증명 모음에 저장 된 hello 암호화 키에 대 한 권한 집합 toopermit hello Azure Active Directory 응용 프로그램 tooread hello 키 여야 합니다.

Hello SPN 만들고 hello 적절 한 권한을 다음과 같이 설정 합니다.

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>가상 디스크를 추가하고 암호화 상태를 검토
tooactually 일부 가상 디스크가 암호화, 기존 VM 디스크 tooan를 추가할 수 있습니다. VM을 다음과 같이 기존는 5gb 데이터 디스크 tooan를 추가 합니다.

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

가상 디스크 hello 현재 암호화 되지 않습니다. 다음과 같이 VM의 hello 현재 암호화 상태를 검토 합니다.

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>가상 디스크 암호화
toonow hello 가상 디스크를 암호화, 모든 hello 이전 구성 요소로 모읍니다.

1. Hello Azure Active Directory 응용 프로그램 및 암호를 지정 합니다.
2. Hello 주요 자격 증명 모음 toostore hello 메타 데이터에 대 한 암호화 된 디스크를 지정 합니다.
3. Hello 실제 암호화 및 암호 해독에 대 한 암호화 키 toouse hello를 지정 합니다.
4. Tooencrypt hello OS 디스크, hello 데이터 디스크 또는 모두 사용할지를 지정 합니다.

다음 hello 최종 단계에서 URL을 키 및 키 자격 증명 모음 ID, URI, hello 필요한 대로 만든 사용자의 Azure 키 자격 증명 모음과 hello 키에 대 한 hello 세부 정보를 검토 수 있습니다.

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Hello hello 출력을 사용 하 여 가상 디스크를 암호화 `azure keyvault show` 및 `azure keyvault key show` 다음과 같이 명령:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello 이전 명령에 여러 변수가, hello 다음 예제는 hello 전체 명령 참조에 대 한.

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

hello Azure CLI hello 암호화 프로세스 동안 자세한 오류가 제공 하지 않습니다. 추가 문제 해결 정보를 검토 `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` hello 암호화 하는 VM에 있습니다.

마지막으로, hello 암호화 상태를 검토를 통해 가상 디스크 암호화 이제 tooconfirm 다시:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>데이터 디스크 더 추가하기
데이터 디스크를 암호화 한 후 나중에 추가로 가상 디스크 tooyour VM을 추가할 수 있으며도 암호화할 수 있습니다. Hello를 실행 하는 경우 `azure vm enable-disk-encryption` 명령, hello를 사용 하 여 hello 시퀀스 버전 증가 `--sequence-version` 매개 변수입니다. 이 시퀀스 버전 매개 변수 있습니다 tooperform에서 반복된 하 여 연산 hello 동일한 VM입니다.

예를 들어 다음과 같이 두 번째 가상 디스크 tooyour VM을 추가할 수 있습니다.

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Hello 추가이 이번 hello 명령 tooencrypt hello 가상 디스크를 다시 실행 `--sequence-version` 매개 변수 및 증분 hello 값 첫에서 다음과 같이 실행:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>다음 단계
* 암호화 키 및 Key Vault 삭제를 비롯한 Azure Key Vault 관리에 대한 자세한 내용은 [CLI를 사용하여 Key Vault 관리](../../key-vault/key-vault-manage-with-cli2.md)를 참조하세요.
* 암호화 된 사용자 지정 VM tooupload tooAzure를 준비 하 고 같은 디스크 암호화에 대 한 자세한 내용은 참조 하십시오. [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다.
