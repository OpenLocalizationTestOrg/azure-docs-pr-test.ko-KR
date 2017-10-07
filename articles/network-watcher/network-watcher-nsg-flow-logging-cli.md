---
title: "aaaManage Azure 네트워크 감시자-Azure CLI를 사용 하 여 기록 네트워크 보안 그룹 흐름 | Microsoft Docs"
description: "이 페이지에서는 Azure CLI와 Azure 네트워크 감시자에서 toomanage 네트워크 보안 그룹 흐름을 로깅할 방법 설명"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Azure CLI를 사용하여 네트워크 보안 그룹 흐름 로그 구성

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다. 이러한 흐름 로그 json 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.

이 문서에서는 Windows, Mac 및 Linux에 대 한 사용 하지 않는 hello 리소스 관리 배포 모델, Azure CLI 2.0에 대 한 우리의 차세대 CLI 합니다.

이 문서의 단계를 tooperform hello, 너무 필요한[Mac, Linux 및 Windows Azure CLI ()에 대 한 hello Azure 명령줄 인터페이스 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)합니다.

## <a name="register-insights-provider"></a>Insights 공급자 등록

흐름에 대 한 순서 대로 로깅 toowork 성공적으로 hello **Microsoft.Insights** 공급자를 등록 해야 합니다. 경우 hello 확실 하지 않은 경우 **Microsoft.Insights** 공급자가 등록 된, 실행 hello 다음 스크립트입니다.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>네트워크 보안 그룹 흐름 로그 사용

다음 예제는 hello hello 명령 tooenable 흐름 로그를 보여 줍니다.

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>네트워크 보안 그룹 흐름 로그 사용 중지

다음 예에서는 toodisable 흐름 로그 사용 하 여 hello:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a>흐름 로그 다운로드

흐름 로그의 hello 저장소 위치를 만들 때 정의 됩니다. 이러한 흐름 저장 된 로그 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 편리한 도구 tooaccess: http://storageexplorer.com/

저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Hello 로그의 hello 구조에 대 한 내용은 [로그 네트워크 보안 그룹 흐름 개요](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[PowerBI와 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-power-bi.md)

너무 방법에 대해 알아봅니다[오픈 소스 도구와 함께 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
