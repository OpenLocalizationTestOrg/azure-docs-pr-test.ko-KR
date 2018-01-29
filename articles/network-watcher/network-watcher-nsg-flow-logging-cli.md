---
title: "Azure Network Watcher를 사용하여 네트워크 보안 그룹 흐름 로그 관리 - Azure CLI | Microsoft Docs"
description: "이 페이지에서는 Azure CLI를 사용하여 Azure Network Watcher의 네트워크 보안 그룹 흐름 로그를 관리하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 51683e937b7985bb61671645f3e2e1be6d786201
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Azure CLI를 사용하여 네트워크 보안 그룹 흐름 로그 구성

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 수신 및 송신 IP 트래픽에 대한 정보를 볼 수 있는 Network Watcher의 기능입니다. 이러한 흐름 로그는 json 형식으로 작성되고 트래픽이 허용되거나 거부된 경우 각 규칙을 기준으로 아웃바운드 및 인바운드 흐름, 흐름이 적용되는 NIC, 흐름에 대한 5개의 튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)를 보여 줍니다.

이 문서에서는 Windows, Mac 및 Linux에서 사용할 수 있는 리소스 관리 배포 모델용 차세대 CLI인 Azure CLI 2.0을 사용합니다.

이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/cli/azure/install-az-cli2)해야 합니다.

## <a name="register-insights-provider"></a>Insights 공급자 등록

흐름 로깅이 성공적으로 작동하기 위해서 **Microsoft.Insights** 공급자를 등록해야 합니다. **Microsoft.Insights** 공급자가 등록되어 있는지 확실하지 않은 경우 다음 스크립트를 실행합니다.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>네트워크 보안 그룹 흐름 로그 사용

다음 예제에서는 흐름 로그를 사용하도록 설정하는 명령이 표시됩니다.

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>네트워크 보안 그룹 흐름 로그 사용 중지

다음 예제를 사용하여 흐름 로그를 사용하지 않도록 설정합니다.

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a>흐름 로그 다운로드

흐름 로그의 저장소 위치를 만들 때 정의합니다. 저장소 계정에 저장되는 이러한 흐름 로그에 액세스하는 편리한 도구는 Microsoft Azure Storage 탐색기이며 http://storageexplorer.com/에서 다운로드할 수 있습니다.

저장소 계정이 지정되어 있으면 패킷 캡처 파일은 다음 위치에서 저장소 계정에 저장됩니다.

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId=/SUBSCRIPTIONS/{subscriptionID}/RESOURCEGROUPS/{resourceGroupName}/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/{nsgName}/y={year}/m={month}/d={day}/h={hour}/m=00/macAddress={macAddress}/PT1H.json
```

로그의 구조에 대한 내용은 [네트워크 보안 그룹 흐름 로그 개요](network-watcher-nsg-flow-logging-overview.md)를 방문하세요.

## <a name="next-steps"></a>다음 단계

[PowerBI를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)하는 방법 알아보기

[오픈 소스 도구를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)하는 방법 알아보기
