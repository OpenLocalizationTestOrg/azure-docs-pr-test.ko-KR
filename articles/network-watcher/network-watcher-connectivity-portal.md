---
title: "Azure Network Watcher를 사용하여 연결 확인 - Azure Portal | Microsoft Docs"
description: "이 페이지에서는 Azure Portal을 사용하여 Network Watcher를 통해 연결 확인을 사용하는 방법을 설명합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="ccf8c-103">Azure Portal을 사용하여 Azure Network Watcher를 통해 연결 확인</span><span class="sxs-lookup"><span data-stu-id="ccf8c-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ccf8c-104">포털</span><span class="sxs-lookup"><span data-stu-id="ccf8c-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="ccf8c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccf8c-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="ccf8c-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ccf8c-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="ccf8c-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="ccf8c-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="ccf8c-108">연결을 사용하여 가상 컴퓨터에서 지정된 끝점으로의 직접 TCP 연결을 설정할 수 있는지를 확인하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ccf8c-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="ccf8c-109">Before you begin</span></span>

<span data-ttu-id="ccf8c-110">이 문서에서는 사용자에게 다음 리소스가 있는 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="ccf8c-111">연결을 확인하려는 영역의 Network Watcher 인스턴스</span><span class="sxs-lookup"><span data-stu-id="ccf8c-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="ccf8c-112">연결을 확인하는 데 사용할 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="ccf8c-112">Virtual machines to check connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccf8c-113">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="ccf8c-114">Windows VM에서 확장을 설치하려면 [Windows용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md)을 방문하고 Linux VM인 경우 [Linux용 Azure Network Watcher 에이전트 가상 컴퓨터 확장](../virtual-machines/linux/extensions-nwa.md)을 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="ccf8c-115">가상 컴퓨터에 대한 연결 확인</span><span class="sxs-lookup"><span data-stu-id="ccf8c-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="ccf8c-116">이 예제에서는 포트 80을 통해 대상 가상 컴퓨터에 대한 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-116">This example checks connectivity to a destination virtual machine over port 80.</span></span>

<span data-ttu-id="ccf8c-117">Network Watcher로 이동하고 **연결 확인(미리 보기)**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-117">Navigate to your Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="ccf8c-118">가상 컴퓨터를 선택하여 연결을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-118">Select the virtual machine to check connectivity from.</span></span> <span data-ttu-id="ccf8c-119">**대상** 섹션에서 **가상 컴퓨터 선택**을 선택하고 테스트할 가상 컴퓨터와 포트를 정확히 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-119">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span></span>

<span data-ttu-id="ccf8c-120">**확인**을 클릭하면 지정한 포트의 가상 컴퓨터 간 연결이 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-120">Once you click **Check**, the connectivity between the virtual machines on the port specified are checked.</span></span> <span data-ttu-id="ccf8c-121">이 예에서는 대상 VM이 연결될 수 없으며 홉 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-121">In the example, the destination VM is unreachable, a listing of hops are shown.</span></span>

![가상 컴퓨터에 대한 연결 결과 확인][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="ccf8c-123">원격 끝점 연결 확인</span><span class="sxs-lookup"><span data-stu-id="ccf8c-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="ccf8c-124">원격 끝점에 대한 연결 및 대기 시간을 확인하려면 **대상** 섹션에서 **수동으로 지정** 라디오 단추를 선택하고 URL 및 포트를 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-124">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span></span>  <span data-ttu-id="ccf8c-125">이 방법은 웹 사이트 및 저장소 끝점과 같은 원격 끝점에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![웹 사이트에 대한 연결 확인 결과][2]

## <a name="next-steps"></a><span data-ttu-id="ccf8c-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ccf8c-127">Next steps</span></span>

<span data-ttu-id="ccf8c-128">[경고로 트리거된 패킷 캡처 만들기](network-watcher-alert-triggered-packet-capture.md)를 확인하여 가상 컴퓨터 경고로 패킷 캡처를 자동화하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-128">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="ccf8c-129">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="ccf8c-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
