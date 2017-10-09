---
title: "aaaUsing 관리 되는 디스크와 Azure 가상 컴퓨터 크기 집합 | Microsoft Docs"
description: "관리 되는 디스크를 가상 컴퓨터 크기 집합 toouse 근거, 방법에 대해 알아봅니다"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/01/2017
ms.author: negat
ms.openlocfilehash: 0e2a21e9f8b114ae1c8b81e1e6124621366f5643
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-vm-scale-sets-and-managed-disks"></a>Azure VM 확장 집합 및 관리 디스크

Azure [가상 컴퓨터 확장 집합](/azure/virtual-machine-scale-sets/)에서는 관리 디스크가 있는 가상 컴퓨터를 지원합니다. 확장 집합이 있는 관리 디스크를 사용하면 다음과 같은 여러 가지 이점이 있습니다.

* Toopre 더 이상 필요-만들고 hello 크기 집합 Vm에 대 한 저장소 계정을 toostore hello OS 디스크를 관리 합니다.

* 관리 되는 데이터 디스크 toohello 크기 집합을 연결할 수 있습니다.

* 관리 디스크를 사용하면 확장 집합이 플랫폼 이미지 기반인 경우 VM 1,000대, 사용자 지정 이미지 기반인 경우 VM 100대의 용량을 확보할 수 있습니다.

## <a name="get-started"></a>시작

간단한 방법을 관리 되는 디스크 크기 집합 시작 tooget는 hello Azure 포털에서에서 toodeploy 하나 있습니다. 자세한 내용은 [이 문서](./virtual-machine-scale-sets-portal-create.md)(영문)를 읽어보세요. 또 다른 간단한 방법은 tooget 시작은 toouse [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) toodeploy 소수 자릿수를 설정 합니다. hello 다음 보여 주는 예제는 Ubuntu toocreate 된 50GB 및 100GB 데이터 디스크를 각각 10 개의 Vm 크기 집합을 따라 하는 방법:

```azurecli
az group create -l southcentralus -n dsktest
az vmss create -g dsktest -n dskvmss --image ubuntults --instance-count 10 --data-disk-sizes-gb 50 100
```

Hello에 표시 될 수 있습니다 또는 [Azure 빠른 시작 템플릿 GitHub 리포지토리](https://github.com/Azure/azure-quickstart-templates) 포함 하는 폴더에 대 한 `vmss` toosee 미리 만들어진 크기 집합을 배포 하는 템플릿의 예입니다. 서식 파일에서 관리 하는 디스크를 이미 사용 중인 tootell를 참조할 수 있습니다 너무[이 목록](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)합니다.

## <a name="next-steps"></a>다음 단계

일반적인 관리 디스크에 대한 자세한 내용은 [이 문서](../virtual-machines/windows/managed-disks-overview.md)를 참조하세요.

toosee tooconvert 사용 하 여 리소스 관리자 템플릿 tooprovision 눈금 집합에 디스크를 관리 하는 방법은 참조 [이 여기서](./virtual-machine-scale-sets-convert-template-to-md.md)합니다. hello 동일한 수정 toohello 리소스 관리자 템플릿 적용 toohello Azure REST API도 합니다.

관리 되는 데이터 디스크를 사용 하 여 눈금 집합에 대해 자세히 toolearn 참조 [이 여기서](./virtual-machine-scale-sets-attached-disks.md)합니다.

규모가 큰 집합으로 작업할 toobegin 너무 참조[이 여기서](./virtual-machine-scale-sets-placement-groups.md)합니다.


