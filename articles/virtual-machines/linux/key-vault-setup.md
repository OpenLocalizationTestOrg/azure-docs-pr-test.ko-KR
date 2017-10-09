---
title: "Linux Vm에 대 한 Azure 키 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "어떻게 키 자격 증명 모음을 사용 하는 Azure 리소스 관리자 가상 컴퓨터와 함께 사용할 tooset hello CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a>키 자격 증명 모음을 사용 하 여 가상 컴퓨터 tooset Azure CLI 2.0 hello 하는 방법

Hello Azure 리소스 관리자 스택의 비밀/인증서는 키 자격 증명 모음에서 제공 되는 리소스 그룹으로 모델링 됩니다. Azure 키 자격 증명 모음에 대 한 자세한 toolearn 참조 [Azure 키 자격 증명 모음 이란?](../../key-vault/key-vault-whatis.md) 주요 자격 증명 모음 toobe vm이 Azure 리소스 관리자 사용에 대 한 순서로 hello *EnabledForDeployment* tootrue 속성 주요 자격 증명 모음을 설정 해야 합니다. 이 문서에서는 키 자격 증명 모음을 사용 하 여 Azure 가상 컴퓨터 (Vm)를 사용 하기 위해 tooset Azure CLI 2.0 hello 하는 방법입니다. Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

이 단계는 tooperform, 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.

## <a name="create-a-key-vault"></a>주요 자격 증명 모음 만들기
키 자격 증명 모음 만들기 및 할당 된 hello 배포 정책을 [az keyvault 만들](/cli/azure/keyvault#create)합니다. hello 다음 예제에서는 키 자격 증명 모음 이름이 `myKeyVault` hello에 `myResourceGroup` 리소스 그룹:

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a>VM과 함께 사용할 Key Vault를 업데이트합니다.
기존 키 자격 증명 모음에 hello 배포 정책 설정 [az keyvault 업데이트](/cli/azure/keyvault#update)합니다. hello 다음 업데이트 hello 라는 주요 자격 증명 모음 `myKeyVault` hello에 `myResourceGroup` 리소스 그룹:

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a>키 자격 증명 모음을 사용 하 여 템플릿 tooset
Tooset hello 템플릿을 사용 하는 경우 해야 `enabledForDeployment` 속성 너무`true` 다음과 같이 hello 키 자격 증명 모음 리소스에 대 한:

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a>다음 단계
템플릿을 사용하여 Key Vault을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.
