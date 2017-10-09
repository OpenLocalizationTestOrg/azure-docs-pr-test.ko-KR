---
title: "aaaEnable 또는 Azure VM 모니터링 사용 안 함"
description: "설명 방법을 tooEnable 또는 Azure VM 모니터링 사용 안 함"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Azure VM 모니터링을 사용하거나 사용하지 않도록 설정

이 섹션에서는 어떻게 tooenable 또는 사용 안 함 모니터링에서 가상 컴퓨터가 Azure에서 실행 되 설명 합니다. Hello 포털 또는 Azure 명령줄 인터페이스를 사용 하 여 Mac, Linux 및 Windows (hello Azure CLI)에 대 한 모니터링을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.

> [!IMPORTANT]
> 이 문서에서는 버전 2.3의 hello Linux 진단 확장을 사용 되지 않습니다. 버전 2.3은 2018년 6월 30일까지 지원됩니다.
>
> Hello Linux 진단 확장의 버전 3.0을 대신 사용할 수 있습니다. 자세한 내용은 참조 [설명서 hello](./diagnostic-extension.md)합니다.

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Azure 포털을 통해 hello 모니터링 사용 안 함/설정

1분 동안 인스턴스에 대한 데이터를 제공하는 Azure VM의 모니터링을 사용하도록 설정할 수 있습니다. (저장소 변경 적용). 자세한 진단 데이터는 hello 포털 그래프 또는 hello API 통해 hello VM에 사용할 수 있는 다음입니다. 기본적으로 Azure Portal은 제한된 메트릭 집합의 호스트 기반 모니터링을 사용하도록 설정할 수 있습니다. 중지 상태에서 또는 hello VM 실행 하는 동안 VM 내에서 메트릭을 모니터링 하는 것이 가능 합니다.

* 열기 hello Azure 포털에서 [https://portal.azure.com](https://portal.azure.com)합니다.
* 왼쪽 탐색 hello, 가상 컴퓨터를 클릭 합니다.
* Hello 목록 가상 컴퓨터에서 실행 중이거나 중지 된 인스턴스를 선택 합니다. hello "가상 컴퓨터" 블레이드를 엽니다.
* 모든 설정을 클릭합니다
* 진단을 클릭합니다.
* 상태 tooOn 변경 또는 해제 합니다. 이 블레이드 hello 수준의 모니터링 원하는 tooenable 가상 컴퓨터에 대 한 세부 정보에서 선택할 수 있습니다.

![Enable/hello Azure 포털을 통해 모니터링을 사용 하지 않도록 설정 합니다.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Azure CLI를 사용하는 모니터링 사용/사용 안 함

Azure VM에 대 한 tooenable 모니터링 합니다.

* PrivateConfig.json과 같은 파일을 만듭니다.

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Azure CLI를 통해 hello 확장을 사용 하도록 설정 합니다.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

자세한 내용은 참조 [를 사용 하 여 Linux 진단 확장 tooMonitor Linux VM의 성능 및 진단 데이터](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
