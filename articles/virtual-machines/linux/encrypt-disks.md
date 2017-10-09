---
title: "Azure에서 Linux VM의 디스크 aaaEncrypt | Microsoft Docs"
description: "Tooencrypt 가상 디스크를 사용 하 여 향상 된 보안에 대 한 Linux VM에 Azure CLI 2.0 hello 하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>어떻게 tooencrypt Linux VM의 가상 디스크
VM(가상 컴퓨터)의 보안과 규정 준수 상태를 향상시키기 위해 Azure에서 가상 디스크를 암호화할 수 있습니다. 디스크는 Azure Key Vault에 안전하게 보관되는 암호화 키를 사용하여 암호화됩니다. 이러한 암호화 키를 제어하고 용도를 감사할 수 있습니다. 이 문서 tooencrypt 가상 디스크를 사용 하 여 Linux VM에 Azure CLI 2.0 hello 하는 방법을 설명 합니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

## <a name="quick-commands"></a>빠른 명령
Hello 작업을 수행 tooquickly 해야 할 경우에 다음 섹션의 세부 정보 hello 기본 hello tooencrypt 가상 디스크를 VM에 명령, 합니다. 각 단계를 찾을 수 있습니다 hello 나머지 hello 문서에 대 한 정보와 컨텍스트 상세 [여기 시작](#overview-of-disk-encryption)합니다.

최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다. Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myKey*, *myVM*이 포함됩니다.

먼저, hello Azure 키 자격 증명 모음 공급자와 Azure 구독 내에서 사용할 수 있도록 [az 리소스 공급자 등록](/cli/azure/provider#register) 리소스 그룹을 만들고 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 *myResourceGroup* hello에 *eastus* 위치:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Azure 키 자격 증명 모음 만들기와 [az keyvault 만들](/cli/azure/keyvault#create) 디스크 암호화와 함께 사용 하기 위해 주요 자격 증명 모음 hello를 사용 하도록 설정 합니다. *keyvault_name*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

[az keyvault key create](/cli/azure/keyvault/key#create)를 사용하여 Key Vault에 암호화 키를 만듭니다. hello 다음 예제에서는 라는 키 *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)에서 Azure Active Directory를 사용하여 서비스 사용자를 만듭니다. hello 서비스 보안 주체 핸들에는 인증 및 자격 증명 모음 키에서에서 암호화 키의 교환을 hello 합니다. 다음 예제는 hello Id와 암호 이후 명령에서 사용 하도록 hello 서비스 사용자에 대 한 hello 값 읽습니다.

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

hello 암호 hello 서비스 주체를 만들 때에 출력 됩니다. 뷰와 레코드 hello 암호 필요 (`echo $sp_password`). [az ad sp list](/cli/azure/ad/sp#list)를 사용하여 서비스 사용자를 나열하고 [az ad sp show](/cli/azure/ad/sp#show)를 사용하여 특정 서비스 사용자에 대한 추가 정보를 볼 수 있습니다.

[az keyvault set-policy](/cli/azure/keyvault#set-policy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다. 다음 예제는 hello에서 hello 서비스 보안 주체 ID에서에서 공급 되는 명령 앞 hello:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

[az vm create](/cli/azure/vm#create)를 사용하여 VM을 만들고 5GB 데이터 디스크를 연결합니다. 특정 Marketplace 이미지만 디스크 암호화를 지원합니다. hello 다음 예제에서는 V `myVM` 를 사용 하는 **CentOS 7.2n** 이미지:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello 출력의 hello 명령 앞에 표시 합니다. 파티션 및 파일 시스템 만듭니다 다음 hello 데이터 디스크를 탑재 합니다. 자세한 내용은 참조 [tooa Linux VM toomount hello에 대 한 새 디스크를 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)합니다. SSH 세션을 닫습니다.

[az vm encryption enable](/cli/azure/vm/encryption#enable)을 사용하여 VM을 암호화합니다. hello 다음 예제에서는 hello `$sp_id` 및 `$sp_password` hello 앞에서 변수 `ad sp create-for-rbac` 명령:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

디스크 암호화 프로세스 toocomplete hello에 대 한 몇 시간이 걸립니다. 사용 하 여 hello 프로세스의 hello 상태를 모니터링 [az vm 암호화 표시](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

상태 표시 hello **EncryptionInProgress**합니다. Hello OS 디스크 보고서에 대 한 hello 상태가 될 때까지 대기 **VMRestartPending**, 다시 시작 된 VM [az vm 다시 시작](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

hello 디스크 암호화 프로세스가 완료 된 hello 부팅 프로세스 중, 따라서 사용 하 여 다시 암호화의 hello 상태를 확인 하기 전에 잠시 기다린 후 **az vm 암호화 표시**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello 운영 체제 디스크와 같은 데이터 디스크를 모두 hello 상태를 보고 이제 해야 **암호화**합니다.

## <a name="overview-of-disk-encryption"></a>디스크 암호화 개요
Linux VM의 가상 디스크는 미사용 시 [dm-crypt](https://wikipedia.org/wiki/Dm-crypt)를 사용하여 암호화됩니다. Azure에서 가상 디스크 암호화는 무료입니다. 암호화 키가 소프트웨어 보호를 사용 하 여 Azure 키 자격 증명 모음에 저장 하거나 가져오거나 140-2 수준 2 표준 tooFIPS 인증 된 하드웨어 보안 모듈 (Hsm)의 키를 생성할 수 있습니다. 이러한 암호화 키에 대한 제어를 유지하고 그 사용을 감사할 수 있습니다. 이러한 암호화 한 키를 사용 하는 tooencrypt 가상 디스크 연결 된 tooyour VM의 암호를 해독 합니다. Azure Active Directory 서비스 사용자는 VM이 켜지고 꺼지는 경우 이러한 암호화 키 발급을 위한 보안 메커니즘을 제공합니다.

VM을 암호화 하기 위한 hello 프로세스는 다음과 같습니다.

1. Azure Key Vault에서 암호화 키를 만듭니다.
2. 암호화 키 toobe hello 디스크를 암호화 하는 데 사용할 수 있는 구성 합니다.
3. hello Azure 키 자격 증명 모음에서에서 tooread hello 암호화 키 hello 적절 한 권한이 있는 사용자는 Azure Active Directory 서비스를 만듭니다.
4. Hello 명령 tooencrypt hello Azure Active Directory 서비스 사용자 및 사용 되는 적절 한 암호화 키 toobe 지정 하 여 가상 디스크를 실행 합니다.
5. hello Azure Active Directory 서비스 보안 주체 요청 hello Azure 키 자격 증명 모음에서 필요한 암호화 키입니다.
6. hello 가상 디스크는 암호화 키를 제공 하는 hello를 사용 하 여 암호화 됩니다.

## <a name="encryption-process"></a>암호화 프로세스
다음과 같은 추가 구성 요소가 hello 디스크 암호화를 사용 합니다.

* **Azure 키 자격 증명 모음** -toosafeguard 암호화 키 및 hello 디스크 암호화/암호 해독 프로세스에 사용 되는 암호를 사용 합니다.
  * 이미 존재하는 경우 기존 Azure Key Vault를 사용할 수 있습니다. 없는 toodedicate 주요 자격 증명 모음 tooencrypting 디스크.
  * tooseparate 관리 범위 및 키 가시성 전용된 키 자격 증명 모음을 만들 수 있습니다.
* **Azure Active Directory** -핸들 hello 필요한 암호화 키의 보안 교환 및 인증에 대 한 작업을 요청 합니다.
  * 일반적으로 응용 프로그램 보유를 위해 Azure Active Directory 인스턴스를 사용할 수 있습니다.
  * hello 서비스 사용자는 보안 메커니즘 toorequest 제공 하 고 hello 적절 한 암호화 키를 실행할 수 있습니다. Azure Active Directory와 통합되는 실제 응용 프로그램을 개발하지는 않습니다.

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

## <a name="create-azure-key-vault-and-keys"></a>Azure Key Vault 및 키 만들기
최신 hello 필요한 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 사용 하 여 Azure 계정 tooan [az 로그인](/cli/azure/#login)합니다. Hello 다음 예제에서는 고유한 값으로 매개 변수 이름 예를 대체 합니다. 예제 매개 변수 이름에는 *myResourceGroup*, *myKey*, *myVM*이 포함됩니다.

hello 첫 번째 단계는 Azure 키 자격 증명 모음 toostore toocreate 암호화 키입니다. Azure 주요 자격 증명, 비밀 키를 저장할 수 있습니다 또는 암호 toosecurely를 허용 하는 응용 프로그램 및 서비스에 구현 합니다. 가상 디스크 암호화에 대 한 주요 자격 증명 모음 toostore tooencrypt 사용된 되는 암호화 키를 사용 하거나 가상 디스크의 암호를 해독 합니다.

Hello Azure 키 자격 증명 모음 공급자와 Azure 구독 내에서 사용 하도록 설정 [az 리소스 공급자 등록](/cli/azure/provider#register) 리소스 그룹을 만들고 [az 그룹 만들기](/cli/azure/group#create)합니다. hello 다음 예제에서는 리소스 그룹 이름을 만듭니다 *myResourceGroup* hello에 `eastus` 위치:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

hello Azure 키 자격 증명 모음 포함 hello 암호화 키와 연결 된 계산 hello VM 자체 저장소 같은 리소스에 있어야 합니다. 동일한 지역을 hello 합니다. Azure 키 자격 증명 모음 만들기와 [az keyvault 만들](/cli/azure/keyvault#create) 디스크 암호화와 함께 사용 하기 위해 주요 자격 증명 모음 hello를 사용 하도록 설정 합니다. *keyvault_name*에 대한 고유한 Key Vault 이름을 다음과 같이 지정합니다.

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

소프트웨어 또는 HSM(하드웨어 보안 모델) 보호를 사용하여 암호화 키를 저장할 수 있습니다. HSM을 사용하려면 프리미엄 Key Vault가 필요합니다. 소프트웨어 보호 키를 저장 하는 표준 주요 자격 증명 모음 보다는 주요 자격 증명 모음 프리미엄은 추가 비용 toocreating 합니다. hello 앞 단계에서에서 프리미엄 주요 자격 증명 추가 toocreate `--sku Premium` toohello 명령입니다. hello 다음 예제에서는 소프트웨어 보호 키 이후 표준 주요 자격 증명 모음을 만들었습니다.

두 보호 모델에 대 한 hello Azure 플랫폼 toobe hello VM toodecrypt hello 가상 디스크를 부팅 될 때 액세스 toorequest hello에 대 한 암호화 키에 부여 해야 합니다. [az keyvault key create](/cli/azure/keyvault/key#create)를 사용하여 Key Vault에 암호화 키를 만듭니다. hello 다음 예제에서는 라는 키 *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Hello Azure Active Directory 서비스 사용자 만들기
가상 디스크를 암호화 하거나 암호를 해독할 때 계정 toohandle hello 인증 및 자격 증명 모음 키에서에서 암호화 키의 교환 지정 합니다. 이 계정에는 Azure Active Directory 서비스 사용자 hello Azure 플랫폼 toorequest hello VM hello 대신 하 여 적절 한 암호화 키를 수 있습니다. 기본 Azure Active Directory 인스턴스를 구독 내에서 사용할 수 있지만 많은 조직이 전용 Azure Active Directory 디렉터리를 두고 있습니다.

[az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac)에서 Azure Active Directory를 사용하여 서비스 사용자를 만듭니다. 다음 예제는 hello Id와 암호 이후 명령에서 사용 하도록 hello 서비스 사용자에 대 한 hello 값 읽습니다.

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

hello 암호 hello 서비스 보안 주체를 만들 때에 표시 됩니다. 뷰와 레코드 hello 암호 필요 (`echo $sp_password`). [az ad sp list](/cli/azure/ad/sp#list)를 사용하여 서비스 사용자를 나열하고 [az ad sp show](/cli/azure/ad/sp#show)를 사용하여 특정 서비스 사용자에 대한 추가 정보를 볼 수 있습니다.

toosuccessfully 암호화 또는 가상 디스크를 암호 해독, 키 자격 증명 모음에 저장 된 hello 암호화 키에 대 한 권한 집합 toopermit hello Azure Active Directory 서비스 보안 주체 tooread hello 키 여야 합니다. [az keyvault set-policy](/cli/azure/keyvault#set-policy)를 사용하여 Key Vault에 대한 사용 권한을 설정합니다. 다음 예제는 hello에서 hello 서비스 보안 주체 ID에서에서 공급 되는 명령 앞 hello:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>가상 컴퓨터 만들기
tooactually 일부 가상 디스크가 암호화, VM을 만들고 데이터 디스크를 추가할 수 있습니다. 만들기와 VM tooencrypt [az vm 만들기](/cli/azure/vm#create) 5gb 데이터 디스크를 연결 합니다. 특정 Marketplace 이미지만 디스크 암호화를 지원합니다. hello 다음 예제에서는 V *myVM* 를 사용 하는 **CentOS 7.2n** 이미지:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour VM를 사용 하 여 hello `publicIpAddress` hello 출력의 hello 명령 앞에 표시 합니다. 파티션 및 파일 시스템 만듭니다 다음 hello 데이터 디스크를 탑재 합니다. 자세한 내용은 참조 [tooa Linux VM toomount hello에 대 한 새 디스크를 연결](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk)합니다. SSH 세션을 닫습니다.


## <a name="encrypt-virtual-machine"></a>가상 컴퓨터 암호화
tooencrypt hello 가상 디스크를 모아 놓은 모든 hello 이전 구성 요소:

1. Hello Azure Active Directory 서비스 사용자 및 암호를 지정 합니다.
2. Hello 주요 자격 증명 모음 toostore hello 메타 데이터에 대 한 암호화 된 디스크를 지정 합니다.
3. Hello 실제 암호화 및 암호 해독에 대 한 암호화 키 toouse hello를 지정 합니다.
4. Tooencrypt hello OS 디스크, hello 데이터 디스크 또는 모두 사용할지를 지정 합니다.

[az vm encryption enable](/cli/azure/vm/encryption#enable)을 사용하여 VM을 암호화합니다. hello 다음 예제에서는 hello `$sp_id` 및 `$sp_password` hello 앞에서 변수 `ad sp create-for-rbac` 명령:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

디스크 암호화 프로세스 toocomplete hello에 대 한 몇 시간이 걸립니다. 사용 하 여 hello 프로세스의 hello 상태를 모니터링 [az vm 암호화 표시](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello는 비슷한 toohello 다음 잘린된 예제 출력:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Hello OS 디스크 보고서에 대 한 hello 상태가 될 때까지 대기 **VMRestartPending**, 다시 시작 된 VM [az vm 다시 시작](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

hello 디스크 암호화 프로세스가 완료 된 hello 부팅 프로세스 중, 따라서 사용 하 여 다시 암호화의 hello 상태를 확인 하기 전에 잠시 기다린 후 **az vm 암호화 표시**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

hello 운영 체제 디스크와 같은 데이터 디스크를 모두 hello 상태를 보고 이제 해야 **암호화**합니다.


## <a name="add-additional-data-disks"></a>데이터 디스크 더 추가하기
데이터 디스크를 암호화 한 후 나중에 추가로 가상 디스크 tooyour VM을 추가할 수 있으며도 암호화할 수 있습니다. 예를 들어 다음과 같이 두 번째 가상 디스크 tooyour VM을 추가할 수 있습니다.

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

다시 hello 명령 tooencrypt hello 가상 디스크를 다음과 같이 실행:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>다음 단계
* 암호화 키 및 Key Vault 삭제를 비롯한 Azure Key Vault 관리에 대한 자세한 내용은 [CLI를 사용하여 Key Vault 관리](../../key-vault/key-vault-manage-with-cli2.md)를 참조하세요.
* 암호화 된 사용자 지정 VM tooupload tooAzure를 준비 하 고 같은 디스크 암호화에 대 한 자세한 내용은 참조 하십시오. [Azure 디스크 암호화](../../security/azure-security-disk-encryption.md)합니다.
