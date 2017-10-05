---
title: "Azure VM 모니터링 사용 또는 사용 안 함"
description: "Azure VM 모니터링을 사용하거나 사용하지 않도록 설정하는 방법을 설명합니다."
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
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="4a41a-103">Azure VM 모니터링을 사용하거나 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="4a41a-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="4a41a-104">이 섹션에서는 Azure에서 실행 중인 가상 컴퓨터에서 모니터링을 사용하거나 사용하지 않도록 설정하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="4a41a-105">포털 또는 Mac, Linux 및 Windows(Azure CLI)용 Azure 명령줄 인터페이스를 사용하여 모니터링을 사용하거나 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4a41a-106">이 문서에서는 사용되지 않는 Linux 진단 확장 2.3 버전에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="4a41a-107">버전 2.3은 2018년 6월 30일까지 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="4a41a-108">대신 Linux 진단 확장 3.0 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="4a41a-109">자세한 내용은 [문서](./diagnostic-extension.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a41a-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="4a41a-110">Azure Portal을 통해 모니터링 사용/사용 안 함</span><span class="sxs-lookup"><span data-stu-id="4a41a-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="4a41a-111">1분 동안 인스턴스에 대한 데이터를 제공하는 Azure VM의 모니터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="4a41a-112">(저장소 변경 적용).</span><span class="sxs-lookup"><span data-stu-id="4a41a-112">(storage changes apply).</span></span> <span data-ttu-id="4a41a-113">그러면 포털 그래프 또는 API를 통해 VM에 대한 자세한 진단 데이터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="4a41a-114">기본적으로 Azure Portal은 제한된 메트릭 집합의 호스트 기반 모니터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="4a41a-115">VM이 실행 중이거나 중지된 상태일 때 VM 내에서 메트릭 모니터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="4a41a-116">[https://portal.azure.com](https://portal.azure.com)에서 Azure Portal을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="4a41a-117">왼쪽 탐색 모음에서 가상 컴퓨터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="4a41a-118">가상 컴퓨터 목록에서 실행 중이거나 중지된 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="4a41a-119">"가상 컴퓨터" 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="4a41a-120">모든 설정을 클릭합니다</span><span class="sxs-lookup"><span data-stu-id="4a41a-120">Click All settings.</span></span>
* <span data-ttu-id="4a41a-121">진단을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-121">Click Diagnostics.</span></span>
* <span data-ttu-id="4a41a-122">상태를 켜짐 또는 꺼짐으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-122">Change status to On or Off.</span></span> <span data-ttu-id="4a41a-123">가상 컴퓨터에 대해 사용하도록 설정할 모니터링 세부 수준을 이 블레이드에서 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![Azure Portal을 통해 모니터링 사용/사용 안 함][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="4a41a-125">Azure CLI를 사용하는 모니터링 사용/사용 안 함</span><span class="sxs-lookup"><span data-stu-id="4a41a-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="4a41a-126">Azure VM에 대한 모니터링을 사용하도록 설정하려면</span><span class="sxs-lookup"><span data-stu-id="4a41a-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="4a41a-127">PrivateConfig.json과 같은 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="4a41a-128">Azure CLI를 통해 확장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4a41a-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="4a41a-129">자세한 내용은 [Linux 진단 확장을 사용하여 Linux VM의 성능 및 진단 데이터 모니터링](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4a41a-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
