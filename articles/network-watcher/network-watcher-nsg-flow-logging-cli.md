---
title: "Azure Network Watcher를 사용하여 네트워크 보안 그룹 흐름 로그 관리 - Azure CLI | Microsoft Docs"
description: "이 페이지에서는 Azure CLI를 사용하여 Azure Network Watcher의 네트워크 보안 그룹 흐름 로그를 관리하는 방법을 설명합니다."
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
ms.openlocfilehash: d5a8aa0cd274132798a0d8484a950926761dae7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="1e569-103">Azure CLI를 사용하여 네트워크 보안 그룹 흐름 로그 구성</span><span class="sxs-lookup"><span data-stu-id="1e569-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1e569-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1e569-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="1e569-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e569-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="1e569-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1e569-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="1e569-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1e569-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="1e569-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1e569-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="1e569-109">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 수신 및 송신 IP 트래픽에 대한 정보를 볼 수 있는 Network Watcher의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="1e569-110">이러한 흐름 로그는 json 형식으로 작성되고 트래픽이 허용되거나 거부된 경우 각 규칙을 기준으로 아웃바운드 및 인바운드 흐름, 흐름이 적용되는 NIC, 흐름에 대한 5개의 튜플 정보(원본/대상 IP, 원본/대상 포트, 프로토콜)를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="1e569-111">이 문서에서는 Windows, Mac 및 Linux에서 사용할 수 있는 리소스 관리 배포 모델용 차세대 CLI인 Azure CLI 2.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="1e569-112">이 문서의 단계를 수행하려면 [Mac, Linux 및 Windows용 Azure 명령줄 인터페이스(Azure CLI)를 설치](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="1e569-113">Insights 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="1e569-113">Register Insights provider</span></span>

<span data-ttu-id="1e569-114">흐름 로깅이 성공적으로 작동하기 위해서 **Microsoft.Insights** 공급자를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="1e569-115">**Microsoft.Insights** 공급자가 등록되어 있는지 확실하지 않은 경우 다음 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="1e569-116">네트워크 보안 그룹 흐름 로그 사용</span><span class="sxs-lookup"><span data-stu-id="1e569-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="1e569-117">다음 예제에서는 흐름 로그를 사용하도록 설정하는 명령이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="1e569-118">네트워크 보안 그룹 흐름 로그 사용 중지</span><span class="sxs-lookup"><span data-stu-id="1e569-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="1e569-119">다음 예제를 사용하여 흐름 로그를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-119">Use the following example to disable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="1e569-120">흐름 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="1e569-120">Download a Flow log</span></span>

<span data-ttu-id="1e569-121">흐름 로그의 저장소 위치를 만들 때 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="1e569-122">저장소 계정에 저장되는 이러한 흐름 로그에 액세스하는 편리한 도구는 Microsoft Azure Storage 탐색기이며 http://storageexplorer.com/에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="1e569-123">저장소 계정이 지정되어 있으면 패킷 캡처 파일은 다음 위치에서 저장소 계정에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e569-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="1e569-124">로그의 구조에 대한 내용은 [네트워크 보안 그룹 흐름 로그 개요](network-watcher-nsg-flow-logging-overview.md)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="1e569-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e569-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e569-125">Next Steps</span></span>

<span data-ttu-id="1e569-126">[PowerBI를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="1e569-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="1e569-127">[오픈 소스 도구를 사용하여 NSG 흐름 로그를 시각화](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="1e569-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
