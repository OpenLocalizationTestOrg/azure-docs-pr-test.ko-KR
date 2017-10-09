---
title: "Azure에서 Linux VM aaaMove | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 Linux VM tooanother Azure 구독 또는 리소스 그룹을 이동 합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Linux VM tooanother 구독 또는 리소스 그룹 이동
이 문서는 방법을 단계별로 설명 toomove 리소스 그룹 또는 구독 간에 Linux VM입니다. 개인 구독에서 VM을 만든 경우에 유용 수 있고 toomove 할 구독 간에 VM 이동 것 tooyour 회사의 구독입니다.

> [!IMPORTANT]
>지금은 Managed Disks를 이동할 수 없습니다. 
>
>새 리소스 Id는 hello 이동의 일부로 생성 됩니다. Hello VM 이동 되었거나, 해야 tooupdate 도구 및 스크립트 toouse hello 새 리소스 Id입니다. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Hello Azure CLI toomove VM을 사용 하 여
toosuccessfully VM 이동 toomove hello VM 및 해당 관련 리소스를 모두 사용 해야 합니다. 사용 하 여 hello **으로 azure 그룹 표시** 리소스 그룹 및 Id의 모든 hello 리소스 toolist 명령입니다. 이 명령은 tooa 파일의 toopipe hello 출력을 복사 하 고 hello Id 이후 명령에 붙여 넣을 수 있도록 도와줍니다.

    azure group show <resourceGroupName>

toomove VM 및 해당 리소스 tooanother 리소스 그룹을 사용 하 여 hello **azure 리소스 이동** CLI 명령입니다. 다음 예제는 hello 방법을 toomove VM 및 hello 가장 일반적인 리소스 필요한 보여 줍니다. 사용 하 여 hello **-i** 매개 변수 및는 쉼표로 구분 된 목록 (공백) Id의 리소스 toomove hello에 대 한 전달 합니다.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Toomove 하려는 경우 VM과 해당 리소스 tooa 다른 구독 hello, hello 추가 **-대상 subscriptionId &#60; destinationSubscriptionID &#62;** toospecify hello 대상 구독 매개 변수입니다.

Tooadd 해야 Windows 컴퓨터에 hello 명령 프롬프트에서에서 작업 하는 경우는  **$**  hello 선언할 때 변수 이름 앞에 있습니다. Linux에서는 필요하지 않습니다.

요청 tooconfirm toomove hello 원하는 리소스를 지정 합니다. 형식 **Y** tooconfirm toomove hello 리소스 되도록 합니다.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>다음 단계
리소스 그룹 및 구독 간의 다양한 유형의 리소스를 이동할 수 있습니다. 자세한 내용은 참조 [리소스 toonew 리소스 그룹이 나 구독 이동](../../resource-group-move-resources.md)합니다.    

