---
title: "aaaManage 패킷 캡처를 Azure 네트워크 감시자-Azure 포털 | Microsoft Docs"
description: "이 페이지에서는 방법을 toomanage hello Azure 포털을 사용 하 여 네트워크 감시자의 패킷 캡처 기능을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="fd537-103">Hello 포털을 사용 하 여 Azure 네트워크 감시자를 사용 하 여 패킷 캡처를 관리</span><span class="sxs-lookup"><span data-stu-id="fd537-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="fd537-104">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="fd537-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="fd537-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd537-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="fd537-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="fd537-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="fd537-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="fd537-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="fd537-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="fd537-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="fd537-109">네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="fd537-110">필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="fd537-111">패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="fd537-112">통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="fd537-113">이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="fd537-114">이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="fd537-115">**패킷 캡처 시작**</span><span class="sxs-lookup"><span data-stu-id="fd537-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="fd537-116">**패킷 캡처 중지**</span><span class="sxs-lookup"><span data-stu-id="fd537-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="fd537-117">**패킷 캡처 삭제**</span><span class="sxs-lookup"><span data-stu-id="fd537-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="fd537-118">**패킷 캡처 다운로드**</span><span class="sxs-lookup"><span data-stu-id="fd537-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="fd537-119">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="fd537-119">Before you begin</span></span>

<span data-ttu-id="fd537-120">이 문서의 다음 리소스는 hello 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="fd537-121">인스턴스 hello 지역에 대 한 네트워크 감시자의 원하는 toocreate 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="fd537-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="fd537-122">Hello 패킷 사용 하 여 가상 컴퓨터 캡처 확장을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd537-123">패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="fd537-124">Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="fd537-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="fd537-125">Hello 포털을 통해 패킷 캡처 agent 확장</span><span class="sxs-lookup"><span data-stu-id="fd537-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="fd537-126">tooinstall hello 패킷 캡처 hello 포털을 통해 VM 에이전트 tooyour 가상 컴퓨터를 탐색, 클릭 **확장** > **추가** 검색 한 **에 대 한 네트워크 감시자 에이전트 Windows**</span><span class="sxs-lookup"><span data-stu-id="fd537-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![에이전트 보기][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="fd537-128">패킷 캡처 개요</span><span class="sxs-lookup"><span data-stu-id="fd537-128">Packet Capture overview</span></span>

<span data-ttu-id="fd537-129">Toohello 이동 [Azure 포털](https://portal.azure.com) 클릭 **네트워킹** > **네트워크 감시자** > **패킷 캡처**</span><span class="sxs-lookup"><span data-stu-id="fd537-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="fd537-130">hello 개요 페이지 hello 상태에 관계 없이 존재 하는 모든 패킷 목록이 캡처합니다 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="fd537-131">패킷 캡처 포트 443 통해 연결 toohello 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![패킷 캡처 개요 화면][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="fd537-133">패킷 캡처 시작</span><span class="sxs-lookup"><span data-stu-id="fd537-133">Start a packet capture</span></span>

<span data-ttu-id="fd537-134">클릭 **추가** toocreate 패킷 캡처.</span><span class="sxs-lookup"><span data-stu-id="fd537-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="fd537-135">패킷 캡처에 정의할 수 있는 hello 속성은 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="fd537-136">**기본 설정**</span><span class="sxs-lookup"><span data-stu-id="fd537-136">**Main settings**</span></span>

- <span data-ttu-id="fd537-137">**구독** -이 값은 사용 되는 hello 구독, 각 구독에서 네트워크 감시자 인스턴스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="fd537-138">**리소스 그룹** -대상이 되는 hello 가상 컴퓨터의 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="fd537-139">**가상 컴퓨터를 대상** -hello 패킷 캡처를 실행 하는 hello 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="fd537-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="fd537-140">**패킷 캡처 name** -이 값은 hello 패킷 캡처의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="fd537-141">**캡처 구성**</span><span class="sxs-lookup"><span data-stu-id="fd537-141">**Capture configuration**</span></span>

- <span data-ttu-id="fd537-142">**저장소 계정** - 패킷 캡처를 저장소 계정에 저장할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="fd537-143">**파일** -패킷 캡처 hello 가상 컴퓨터에 로컬로 저장 하는 경우를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="fd537-144">**저장소 계정** -hello에 저장소 계정 toosave hello 패킷 캡처를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="fd537-145">기본 위치는 https://{저장소 계정 이름}.blob.core.windows.net/network-watcher-logs/subscriptions/{구독 ID}/resourcegroups/{리소스 그룹 이름}/providers/microsoft.compute/virtualmachines/{가상 컴퓨터 이름}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap입니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="fd537-146">(**저장소**를 선택한 경우에만 사용됨)</span><span class="sxs-lookup"><span data-stu-id="fd537-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="fd537-147">**로컬 파일 경로** -가상 컴퓨터 toosave hello 패킷 캡처 hello 로컬 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="fd537-148">(**파일**을 선택한 경우에만 사용됨).</span><span class="sxs-lookup"><span data-stu-id="fd537-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="fd537-149">유효한 경로를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="fd537-150">**패킷 당 최대 바이트** -수 hello 바이트를 모두 비워 두면 캡처되는 각 패킷의 바이트 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="fd537-151">**세션 마다 최대 바이트** -총의 hello 값 hello 패킷 캡처 중지에 도달 하면 캡처되는 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="fd537-152">**제한 시간 (초)** -패킷 캡처 toostop hello에 대 한 시간 제한 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="fd537-153">기본값은 18000초입니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="fd537-154">Premium Storage 계정에서는 패킷 캡처 저장이 현재 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="fd537-155">**필터링(선택 사항)**</span><span class="sxs-lookup"><span data-stu-id="fd537-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="fd537-156">**프로토콜** -hello 패킷 캡처에 대 한 프로토콜 toofilter hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="fd537-157">hello 사용 가능한 값에는 TCP, UDP 및은 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="fd537-158">**로컬 IP 주소** -이 값이 필터 값 hello 로컬 IP 주소와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="fd537-159">**로컬 포트** -이 값이 필터 값 hello 로컬 포트와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="fd537-160">**원격 IP 주소** -이 값이 필터 값 hello 원격 IP와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="fd537-161">**원격 포트** -이 값이 필터 값 hello 원격 포트와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="fd537-162">포트 및 IP 주소 값은 단일 값이거나 값 범위이거나 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="fd537-163">(즉, 포트의 경우 80-1024) 원하는 만큼 많은 필터를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="fd537-164">Hello 값 입력 된 후 클릭 **확인** toocreate hello 패킷 캡처.</span><span class="sxs-lookup"><span data-stu-id="fd537-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![패킷 캡처 만들기][2]

<span data-ttu-id="fd537-166">Hello 시간 제한에 설정 hello 패킷 캡처 만료, hello 패킷 캡처 중지 되 고 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="fd537-167">수동으로 hello 패킷 캡처 세션을 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="fd537-168">패킷 캡처 삭제</span><span class="sxs-lookup"><span data-stu-id="fd537-168">Delete a packet capture</span></span>

<span data-ttu-id="fd537-169">Hello 패킷에 보기를 캡처, hello 클릭 **상황에 맞는 메뉴** (...) 또는 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제** toostop hello 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="fd537-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![패킷 캡처 삭제][3]

> [!NOTE]
> <span data-ttu-id="fd537-171">패킷 캡처를 삭제 하는 경우에 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="fd537-172">요청 toodelete hello 패킷 캡처를 원하는 tooconfirm 클릭 **예**</span><span class="sxs-lookup"><span data-stu-id="fd537-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![확인][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="fd537-174">패킷 캡처 중지</span><span class="sxs-lookup"><span data-stu-id="fd537-174">Stop a packet capture</span></span>

<span data-ttu-id="fd537-175">Hello 패킷에 보기를 캡처, hello 클릭 **상황에 맞는 메뉴** (...) 또는 마우스 오른쪽 단추로 클릭 하 고 클릭 **중지** toostop hello 패킷 캡처</span><span class="sxs-lookup"><span data-stu-id="fd537-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="fd537-176">패킷 캡처 다운로드</span><span class="sxs-lookup"><span data-stu-id="fd537-176">Download a packet capture</span></span>

<span data-ttu-id="fd537-177">패킷 캡처 세션이 완료 되 면 hello 캡처 파일은 업로드 tooblob 저장소나 tooa 로컬 파일 hello VM에서.</span><span class="sxs-lookup"><span data-stu-id="fd537-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="fd537-178">hello 패킷 캡처의 hello 저장소 위치는 hello 세션의 작성 시 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="fd537-179">저장 된 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 파일을 캡처하기 이러한 편리한 도구 tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="fd537-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="fd537-180">저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="fd537-181">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fd537-181">Next steps</span></span>

<span data-ttu-id="fd537-182">어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="fd537-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="fd537-183">[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="fd537-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













