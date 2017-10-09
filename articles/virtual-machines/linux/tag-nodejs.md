---
title: "aaaHow tootag Azure Linux 가상 컴퓨터 | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델을 사용 하 여 Azure에서 만든 Azure Linux 가상 컴퓨터는 태그를 지정 하는 방법을 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a>어떻게 tootag Azure에서 Linux 가상 컴퓨터
이 문서에서는 다양 한 방법 tootag hello 리소스 관리자 배포 모델을 통해 Azure에서 Linux 가상 컴퓨터를 설명 합니다. 태그는 리소스 또는 리소스 그룹에 직접 배치할 수 있는 사용자 정의 키/값 쌍입니다. 현재 azure 리소스 및 리소스 그룹 당 too15 태그를 지원합니다. 태그 생성 hello 시 리소스에 배치 될 수 있습니다 또는 tooan 기존 리소스를 추가 합니다. 하십시오 note, hello 리소스 관리자 배포 모델만을 통해 생성 된 리소스에 대 한 태그는 지원 합니다.

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a>Azure CLI를 사용하여 태그 지정
toobegin, [설치 및 구성 hello Azure CLI](../../xplat-cli-azure-resource-manager.md) 리소스 관리자 모드에 있는지 확인 하 고 (`azure config mode arm`).

Hello 태그를 포함 하 여,이 명령을 사용 하 여 지정 된 가상 컴퓨터에 대 한 모든 속성을 볼 수 있습니다.

        azure vm show -g MyResourceGroup -n MyTestVM

hello Azure CLI를 통해 새 VM 태그 tooadd hello를 사용할 수 있습니다 `azure vm set` hello 태그 매개 변수와 함께 명령 **-t**:

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

모든 tooremove 태그 hello를 사용할 수 있습니다 **– T** hello에 대 한 매개 변수 `azure vm set` 명령입니다.

        azure vm set – g MyResourceGroup –n MyTestVM -T


태그 tooour 리소스 Azure CLI 적용 하 고 포털 hello, 살펴보겠습니다는 hello 사용량 세부 정보 toosee hello 태그 hello 청구 포털에서입니다.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>다음 단계
* Azure 리소스 태그에 대 한 자세한 toolearn 참조 [Azure 리소스 관리자 개요] [ Azure Resource Manager Overview] 및 [tooorganize 태그를 사용 하 여 Azure 리소스] [ Using Tags tooorganize your Azure Resources].
* toosee 태그 수 Azure 리소스의 사용을 관리 하는 방법 참조 [Azure 청구서 이해] [ Understanding your Azure Bill] 및 [Microsoft Azure 리소스 소비량에 대 한 이해력] [Gain insights into your Microsoft Azure resource consumption].

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
