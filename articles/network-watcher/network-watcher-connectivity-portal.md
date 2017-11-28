---
title: "Azure 네트워크 감시자-Azure 포털의 aaaCheck 연결 | Microsoft Docs"
description: "이 페이지에서는 toouse 연결 hello Azure 포털을 사용 하 여 네트워크 감시자를 확인 하는 방법을 설명 합니다."
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
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="40033-103">Hello Azure 포털을 사용 하 여 Azure 네트워크 감시자를 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="40033-104">포털</span><span class="sxs-lookup"><span data-stu-id="40033-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="40033-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="40033-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="40033-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="40033-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="40033-107">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="40033-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="40033-108">Toouse 연결 tooverify 경우 끝점에 지정 된 가상 컴퓨터 tooa의 직접 TCP 연결 수 설정 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40033-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="40033-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="40033-109">Before you begin</span></span>

<span data-ttu-id="40033-110">이 문서에서는 다음 리소스는 hello 있는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="40033-111">인스턴스 toocheck 연결 hello 지역에 대 한 네트워크 감시자의 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="40033-112">가상 컴퓨터와 toocheck 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="40033-113">연결 확인에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="40033-114">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="40033-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="40033-115">연결 tooa 가상 컴퓨터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="40033-116">이 예제에서는 포트 80 통한 연결 tooa 대상 가상 컴퓨터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="40033-117">네트워크 감시자 tooyour 이동한 클릭 **연결성 확인 (미리 보기)**합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="40033-118">가상 컴퓨터 toocheck hello 연결을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="40033-119">Hello에 **대상** 섹션 선택 **가상 컴퓨터를 선택** hello 올바른 가상 컴퓨터와 포트 tootest를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="40033-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="40033-120">클릭 한 후 **확인**, 지정 된 hello 포트에 hello 가상 컴퓨터 간의 hello 연결 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40033-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="40033-121">Hello 예에서 hello 대상 VM에 연결할 수 없습니다, 홉 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="40033-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![가상 컴퓨터에 대한 연결 결과 확인][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="40033-123">원격 끝점 연결 확인</span><span class="sxs-lookup"><span data-stu-id="40033-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="40033-124">toocheck hello 연결 및 대기 시간 tooa 원격 끝점 선택 hello **수동으로 지정** hello에서 라디오 단추 **대상** 섹션에서 hello url 및 hello 포트를 입력 하 고 클릭 **확인** .</span><span class="sxs-lookup"><span data-stu-id="40033-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="40033-125">이 방법은 웹 사이트 및 저장소 끝점과 같은 원격 끝점에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40033-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![웹 사이트에 대한 연결 확인 결과][2]

## <a name="next-steps"></a><span data-ttu-id="40033-127">다음 단계</span><span class="sxs-lookup"><span data-stu-id="40033-127">Next steps</span></span>

<span data-ttu-id="40033-128">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="40033-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="40033-129">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="40033-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
