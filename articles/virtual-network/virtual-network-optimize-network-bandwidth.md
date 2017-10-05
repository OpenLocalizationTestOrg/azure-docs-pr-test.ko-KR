---
title: "VM 네트워크 처리량 최적화 | Microsoft Docs"
description: "Azure Virtual Machine 네트워크 처리량을 최적화하는 방법을 알아봅니다."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a><span data-ttu-id="da83e-103">Azure Virtual Machine에 대한 네트워크 처리량 최적화</span><span class="sxs-lookup"><span data-stu-id="da83e-103">Optimize network throughput for Azure virtual machines</span></span>

<span data-ttu-id="da83e-104">Azure VM(Virtual Machine)에는 네트워크 처리량에 대해 추가로 최적화할 수 있는 기본 네트워크 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-104">Azure virtual machines (VM) have default network settings that can be further optimized for network throughput.</span></span> <span data-ttu-id="da83e-105">이 문서에서는 Ubuntu, CentOS 및 Red Hat과 같은 주요 배포판을 비롯한 Microsoft Azure Windows 및 Linux VM에 대해 네트워크 처리량을 최적화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-105">This article describes how to optimize network throughput for Microsoft Azure Windows and Linux VMs, including major distributions such as Ubuntu, CentOS and Red Hat.</span></span>

## <a name="windows-vm"></a><span data-ttu-id="da83e-106">Windows VM</span><span class="sxs-lookup"><span data-stu-id="da83e-106">Windows VM</span></span>

<span data-ttu-id="da83e-107">Windows VM이 [가속화된 네트워킹](virtual-network-create-vm-accelerated-networking.md)으로 지원되는 경우 해당 기능을 사용하도록 설정하는 것이 최적의 처리량을 얻기 위한 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-107">If your Windows VM is supported with [Accelerated Networking](virtual-network-create-vm-accelerated-networking.md), enabling that feature would be the optimal configuration for throughput.</span></span> <span data-ttu-id="da83e-108">RSS(수신측 배율)를 사용하는 다른 모든 Windows VM은 RSS 없는 VM보다 더 높은 최대 처리량에 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-108">For all other Windows VMs, using Receive Side Scaling (RSS) can reach higher maximal throughput than a VM without RSS.</span></span> <span data-ttu-id="da83e-109">RSS는 Windows VM에서 기본적으로 사용되지 않도록 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-109">RSS may be disabled by default in a Windows VM.</span></span> <span data-ttu-id="da83e-110">다음 단계를 완료하여 RSS가 사용되도록 설정되어 있는지 여부를 확인하고 사용되지 않도록 설정되어 있으면 사용되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-110">Complete the following steps to determine whether RSS is enabled and to enable it if it's disabled.</span></span>

1. <span data-ttu-id="da83e-111">`Get-NetAdapterRss` PowerShell 명령을 입력하여 RSS가 네트워크 어댑터에 대해 사용되도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-111">Enter the `Get-NetAdapterRss` PowerShell command to see if RSS is enabled for a network adapter.</span></span> <span data-ttu-id="da83e-112">`Get-NetAdapterRss`에서 반환된 다음 예제 출력에서 RSS는 사용되도록 설정되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-112">In the following example output returned from the `Get-NetAdapterRss`, RSS is not enabled.</span></span>

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. <span data-ttu-id="da83e-113">다음 명령을 입력하여 RSS를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-113">Enter the following command to enable RSS:</span></span>

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    <span data-ttu-id="da83e-114">이전 명령에는 출력이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-114">The previous command does not have an output.</span></span> <span data-ttu-id="da83e-115">이 명령은 NIC 설정을 변경했으므로 약 1분 동안 일시적으로 연결이 끊겼습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-115">The command changed NIC settings, causing temporary connectivity loss for about one minute.</span></span> <span data-ttu-id="da83e-116">연결이 끊긴 동안 다시 연결 중 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-116">A Reconnecting dialog box appears during the connectivity loss.</span></span> <span data-ttu-id="da83e-117">일반적으로 세 번째 시도 후 연결이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-117">Connectivity is typically restored after the third attempt.</span></span>
3. <span data-ttu-id="da83e-118">`Get-NetAdapterRss` 명령을 다시 입력하여 VM에서 RSS가 사용되도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-118">Confirm that RSS is enabled in the VM by entering the `Get-NetAdapterRss` command again.</span></span> <span data-ttu-id="da83e-119">성공하면 다음 예제 출력이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-119">If successful, the following example output is returned:</span></span>

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a><span data-ttu-id="da83e-120">Linux VM</span><span class="sxs-lookup"><span data-stu-id="da83e-120">Linux VM</span></span>

<span data-ttu-id="da83e-121">RSS는 Azure Linux VM에 기본적으로 항상 사용되도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-121">RSS is always enabled by default in an Azure Linux VM.</span></span> <span data-ttu-id="da83e-122">2017년 1월 이후에 출시된 Linux 커널에는 Linux VM이 더 높은 네트워크 처리량을 얻도록 하는 새로운 네트워크 최적화 옵션이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-122">Linux kernels released since January, 2017 include new network optimization options that enable a Linux VM to achieve higher network throughput.</span></span>

### <a name="ubuntu"></a><span data-ttu-id="da83e-123">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="da83e-123">Ubuntu</span></span>

<span data-ttu-id="da83e-124">최적화를 얻으려면 먼저 지원되는 최신 버전으로 업데이트합니다. 예를 들어 2017년 6월이면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-124">In order to get the optimization, first update to the latest supported version, as of June 2017, which is:</span></span>
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
<span data-ttu-id="da83e-125">업데이트가 완료되면 다음 명령을 입력하여 최신 커널을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-125">After the update is complete, enter the following commands to get the latest kernel:</span></span>

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

<span data-ttu-id="da83e-126">선택적 명령:</span><span class="sxs-lookup"><span data-stu-id="da83e-126">Optional command:</span></span>

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a><span data-ttu-id="da83e-127">Ubuntu Azure Preview 커널</span><span class="sxs-lookup"><span data-stu-id="da83e-127">Ubuntu Azure Preview kernel</span></span>
> [!WARNING]
> <span data-ttu-id="da83e-128">이 Azure Linux Preview 커널은 일반 공급 릴리스 상태의 커널 및 Marketplace 이미지와 가용성 및 안정성 수준이 다를 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-128">This Azure Linux Preview kernel may not have the same level of availability and reliability as Marketplace images and kernels that are in general availability release.</span></span> <span data-ttu-id="da83e-129">기능이 지원되지 않거나 제한될 수도 있으며, 기본 커널에 비해 안정성이 떨어질 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-129">The feature is not supported, may have constrained capabilities, and may not be as reliable as the default kernel.</span></span> <span data-ttu-id="da83e-130">따라서 프로덕션 작업에는 이 커널을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="da83e-130">Do not use this kernel for production workloads.</span></span>

<span data-ttu-id="da83e-131">여기서 제안하는 Azure Linux 커널을 설치하면 처리량 성능을 대폭 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-131">Significant throughput performance can be achieved by installing the proposed Azure Linux kernel.</span></span> <span data-ttu-id="da83e-132">이 커널을 사용해 보려면 /etc/apt/sources.list에 아래 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-132">To try this kernel, add this line to /etc/apt/sources.list</span></span>

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

<span data-ttu-id="da83e-133">그런 다음 아래 명령을 루트로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-133">Then run these commands as root.</span></span>
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a><span data-ttu-id="da83e-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="da83e-134">CentOS</span></span>

<span data-ttu-id="da83e-135">처리량을 최적화하려면 먼저 지원되는 최신 버전으로 업데이트합니다. 2017년 7월 현재 최신 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-135">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
<span data-ttu-id="da83e-136">업데이트가 완료되면 최신 LIS(Linux Integration Services)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-136">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="da83e-137">처리량 최적화 기능은 LIS 4.2.2-2부터 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-137">The throughput optimization is in LIS, starting from 4.2.2-2.</span></span> <span data-ttu-id="da83e-138">다음 명령을 입력하여 LIS를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-138">Enter the following commands to install LIS:</span></span>

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a><span data-ttu-id="da83e-139">Red Hat</span><span class="sxs-lookup"><span data-stu-id="da83e-139">Red Hat</span></span>

<span data-ttu-id="da83e-140">처리량을 최적화하려면 먼저 지원되는 최신 버전으로 업데이트합니다. 2017년 7월 현재 최신 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-140">In order to get the optimization, first update to the latest supported version, as of July 2017, which is:</span></span>
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
<span data-ttu-id="da83e-141">업데이트가 완료되면 최신 LIS(Linux Integration Services)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-141">After the update is complete, install the latest Linux Integration Services (LIS).</span></span>
<span data-ttu-id="da83e-142">처리량 최적화 기능은 LIS 4.2부터 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-142">The throughput optimization is in LIS, starting from 4.2.</span></span> <span data-ttu-id="da83e-143">다음 명령을 입력하여 LIS를 다운로드한 후 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="da83e-143">Enter the following commands to download and install LIS:</span></span>

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

<span data-ttu-id="da83e-144">[다운로드 페이지](https://www.microsoft.com/download/details.aspx?id=55106)를 확인하여 Hyper-V용 Linux Integration Services 버전 4.2에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="da83e-144">Learn more about Linux Integration Services Version 4.2 for Hyper-V by viewing the [download page](https://www.microsoft.com/download/details.aspx?id=55106).</span></span>

## <a name="next-steps"></a><span data-ttu-id="da83e-145">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da83e-145">Next steps</span></span>
* <span data-ttu-id="da83e-146">이제 VM이 최적화되었으므로 [Azure VM 대역폭/처리량 테스트](virtual-network-bandwidth-testing.md)를 통해 시나리오에 대한 결과를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="da83e-146">Now that the VM is optimized, see the result with [Bandwidth/Throughput testing Azure VM](virtual-network-bandwidth-testing.md) for your scenario.</span></span>
* <span data-ttu-id="da83e-147">[Azure Virtual Network FAQ(질문과 대답)](virtual-networks-faq.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="da83e-147">Learn more with [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
