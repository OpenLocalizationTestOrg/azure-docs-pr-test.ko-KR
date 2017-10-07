---
title: "aaaManage Azure 네트워크 감시자-Azure CLI 1.0을 사용 하 여 기록 네트워크 보안 그룹 흐름 | Microsoft Docs"
description: "이 페이지에서는 네트워크 보안 그룹 흐름 toomanage Azure CLI 1.0과 함께 Azure 네트워크 감시자 로그인 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="5e32a-103">Azure CLI 1.0을 사용하여 네트워크 보안 그룹 흐름 로그 구성</span><span class="sxs-lookup"><span data-stu-id="5e32a-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5e32a-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="5e32a-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="5e32a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e32a-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="5e32a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5e32a-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="5e32a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5e32a-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="5e32a-108">REST API</span><span class="sxs-lookup"><span data-stu-id="5e32a-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="5e32a-109">네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보 수 있는 네트워크 감시자의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="5e32a-110">이러한 흐름 로그 json 형식으로 작성 되 고 아웃 바운드 표시 및 hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 5-튜플 정보에 각 규칙 별로 인바운드 흐름 hello NIC hello 흐름 적용 하 고 트래픽이 허용 된 경우 hello 또는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="5e32a-111">이 문서에서는 Windows, Mac 및 Linux에 사용할 수 있는 플랫폼 간 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="5e32a-112">Network Watcher는 현재 CLI 지원을 위한 Azure CLI 1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="5e32a-113">Insights 공급자 등록</span><span class="sxs-lookup"><span data-stu-id="5e32a-113">Register Insights provider</span></span>

<span data-ttu-id="5e32a-114">흐름에 대 한 순서 대로 로깅 toowork 성공적으로 hello **Microsoft.Insights** 공급자를 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="5e32a-115">경우 hello 확실 하지 않은 경우 **Microsoft.Insights** 공급자가 등록 된, 실행 hello 다음 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="5e32a-116">네트워크 보안 그룹 흐름 로그 사용</span><span class="sxs-lookup"><span data-stu-id="5e32a-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="5e32a-117">다음 예제는 hello hello 명령 tooenable 흐름 로그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="5e32a-118">네트워크 보안 그룹 흐름 로그 사용 중지</span><span class="sxs-lookup"><span data-stu-id="5e32a-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="5e32a-119">다음 예에서는 toodisable 흐름 로그 사용 하 여 hello:</span><span class="sxs-lookup"><span data-stu-id="5e32a-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="5e32a-120">흐름 로그 다운로드</span><span class="sxs-lookup"><span data-stu-id="5e32a-120">Download a Flow log</span></span>

<span data-ttu-id="5e32a-121">흐름 로그의 hello 저장소 위치를 만들 때 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="5e32a-122">이러한 흐름 저장 된 로그 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 편리한 도구 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="5e32a-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="5e32a-123">저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e32a-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="5e32a-124">Hello 로그의 hello 구조에 대 한 내용은 [로그 네트워크 보안 그룹 흐름 개요](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="5e32a-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e32a-125">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5e32a-125">Next Steps</span></span>

<span data-ttu-id="5e32a-126">너무 방법에 대해 알아봅니다[PowerBI와 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="5e32a-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="5e32a-127">너무 방법에 대해 알아봅니다[오픈 소스 도구와 함께 NSG 흐름 로그를 시각화 합니다.](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="5e32a-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
