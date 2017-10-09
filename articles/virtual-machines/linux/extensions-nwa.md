---
title: "Linux 용 네트워크 감시자 에이전트가 가상 컴퓨터 확장 aaaAzure | Microsoft Docs"
description: "가상 컴퓨터 확장을 사용 하 여 Linux 가상 컴퓨터에서 네트워크 감시자 에이전트 hello를 배포 합니다."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a>Linux용 Network Watcher 에이전트 가상 컴퓨터 확장

## <a name="overview"></a>개요

[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/)는 Azure 네트워크에 대한 모니터링을 허용하는 네트워크 성능 모니터링, 진단 및 분석 서비스입니다. 네트워크 감시자 에이전트가 가상 컴퓨터 확장 hello hello Azure 가상 컴퓨터 네트워크 감시자 기능 중 일부에 대 한 요구 사항입니다. 주문형 네트워크 트래픽을 캡처하는 기능 및 기타 고급 기능이 포함됩니다.

이 문서 정보 hello Linux 용 hello 네트워크 감시자 에이전트가 가상 컴퓨터 확장에 대 한 플랫폼 및 배포 옵션을 지원 합니다.

## <a name="prerequisites"></a>필수 조건

### <a name="operating-system"></a>운영 체제

네트워크 감시자 에이전트 확장 hello 이러한 Linux 배포에 대해 실행할 수 있습니다.

| 배포 | 버전 |
|---|---|
| Ubuntu | 16.04 LTS, 14.04 LTS 및 12.04 LTS |
| Debian | 7 및 8 |
| RedHat | 6.x 및 7.x |
| Oracle Linux | 7x |
| Suse | 11 및 12 |
| OpenSuse | 7.0 |
| CentOS | 7.0 |

CoreOS는 현재 지원되지 않습니다.

### <a name="internet-connectivity"></a>인터넷 연결

Hello 네트워크 감시자 에이전트 기능 중 일부에서는 해당 hello 대상 가상 컴퓨터 연결된 toohello 인터넷 이어야 합니다. Hello 기능 tooestablish 나가는 연결 되지 않은 오작동 하거나 사용할 수 없게 될 수 있습니다 hello 네트워크 감시자 에이전트 기능 중 일부입니다. 자세한 내용은 hello를 참조 하십시오 [네트워크 감시자 설명서](https://review.docs.microsoft.com/en-us/azure/network-watcher/)합니다.

## <a name="extension-schema"></a>확장 스키마

hello 다음 JSON 스키마를 보여 줍니다 hello hello 네트워크 감시자 Agent 확장에 대 한 합니다. hello 확장명 모두 필요 하거나 사용자가 제공한 설정을이 이번에는 지 원하는 기본 구성입니다.

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a>속성 값

| 이름 | 값/예제 |
| ---- | ---- |
| apiVersion | 2015-06-15 |
| publisher | Microsoft.Azure.NetworkWatcher |
| type | NetworkWatcherAgentLinux |
| typeHandlerVersion | 1.4 |

## <a name="template-deployment"></a>템플릿 배포

Azure Resource Manager 템플릿을 사용하여 Azure VM 확장을 배포할 수 있습니다. Azure 리소스 관리자 템플릿 배포 중에 Azure 리소스 관리자 템플릿 toorun hello 네트워크 감시자 Agent 확장 hello 이전 섹션에서 자세히 설명 하는 hello JSON 스키마를 사용할 수 있습니다.

## <a name="azure-cli-deployment"></a>Azure CLI 배포

hello Azure CLI 사용된 toodeploy hello 네트워크 감시자의 에이전트 VM 확장 tooan 기존 가상 컴퓨터를 수 있습니다.

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a>문제 해결 및 지원

### <a name="troubleshooting"></a>문제 해결

Hello Azure 포털에서에서 하 고 hello Azure CLI를 사용 하 여 확장 배포의 hello 상태에 대 한 데이터를 검색할 수 있습니다. hello 명령을 사용 하 여 다음을 실행 하는 특정된 VM에 대 한 확장의 toosee hello 배포 상태 hello Azure CLI 합니다.

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

확장 실행은 hello에 기록 된 toofiles 다음 디렉터리를 출력 합니다.

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a>지원

Toohello 네트워크 감시자 설명서를 참조 하거나 Azure hello에 게 문의 수를 언제 든 지가이 문서에서 자세한 도움이 필요 하면 경우 전문가의 hello [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/en-us/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/en-us/support/options/) 지원 받기를 선택 합니다. Azure 지원을 사용 하는 방법에 대 한 내용은 하세요 hello [Microsoft Azure 지원 FAQ](https://azure.microsoft.com/en-us/support/faq/)합니다.
