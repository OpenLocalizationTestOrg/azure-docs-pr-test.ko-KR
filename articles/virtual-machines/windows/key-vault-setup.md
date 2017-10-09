---
title: "키 자격 증명 모음에 대 한 Windows Vm이 Azure 리소스 관리자를 aaaSet | Microsoft Docs"
description: "어떻게 Azure 리소스 관리자 가상 컴퓨터와 함께 사용 하기 위해 키 자격 증명 모음을 tooset 합니다."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a>Azure Resource Manager에서 가상 컴퓨터에 대한 주요 자격 증명 모음 설정

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

Azure 리소스 관리자 스택의 비밀/인증서는 키 자격 증명 모음 hello 리소스 공급자가 제공 되는 리소스 그룹으로 모델링 됩니다. 주요 자격 증명에 대 한 자세한 toolearn 참조 [Azure 키 자격 증명 모음 이란?](../../key-vault/key-vault-whatis.md)

> [!NOTE]
> 1. Azure 리소스 관리자 가상 컴퓨터와 함께 사용 되는 주요 자격 증명 모음 toobe에 대 한 순서로 hello **EnabledForDeployment** tootrue 속성 주요 자격 증명 모음을 설정 해야 합니다. 다양한 클라이언트에서 이 작업을 수행할 수 있습니다.
> 2. 가상 컴퓨터를 hello 대로 toobe에서 만든 hello 주요 자격 증명 모음 요구 hello 동일한 구독 및 위치입니다.
>
>

## <a name="use-powershell-tooset-up-key-vault"></a>키 자격 증명 모음을 사용 하 여 PowerShell tooset
PowerShell을 사용 하 여 주요 자격 증명 모음 toocreate 참조 [Azure 키 자격 증명 모음 시작](../../key-vault/key-vault-get-started.md#vault)합니다.

새 주요 자격 증명의 경우 다음 PowerShell cmdlet을 사용할 수 있습니다.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

기존 주요 자격 증명의 경우 다음 PowerShell cmdlet을 사용할 수 있습니다.

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a>Us CLI tooset 키 자격 증명 모음을
hello CLI (명령줄 인터페이스)를 사용 하 여 주요 자격 증명 모음 toocreate 참조 [관리 키 자격 증명 모음 CLI를 사용 하 여](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)합니다.

CLI에 대 한 hello 배포 정책을 지정 하기 전에 toocreate hello 키 자격 증명 모음이 있는지 합니다. 다음 명령을 hello를 사용 하 여이 수행할 수 있습니다.

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a>키 자격 증명 모음을 사용 하 여 템플릿 tooset
Tooset hello 서식 파일을 사용 하는 동안 필요한 `enabledForDeployment` 속성 너무`true` hello 키 자격 증명 모음 리소스에 대 한 합니다.

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

템플릿을 사용하여 주요 자격 증명 모음을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.
