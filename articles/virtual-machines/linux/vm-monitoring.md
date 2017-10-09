---
title: "aaaEnable 또는 Azure VM 모니터링 사용 안 함"
description: "설명 방법을 tooEnable 또는 Azure VM 모니터링 사용 안 함"
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
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="969bd-103">Azure VM 모니터링을 사용하거나 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="969bd-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="969bd-104">이 섹션에서는 어떻게 tooenable 또는 사용 안 함 모니터링에서 가상 컴퓨터가 Azure에서 실행 되 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="969bd-105">Hello 포털 또는 Azure 명령줄 인터페이스를 사용 하 여 Mac, Linux 및 Windows (hello Azure CLI)에 대 한 모니터링을 사용 하지 않도록 설정 하거나 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="969bd-106">이 문서에서는 버전 2.3의 hello Linux 진단 확장을 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="969bd-107">버전 2.3은 2018년 6월 30일까지 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="969bd-108">Hello Linux 진단 확장의 버전 3.0을 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="969bd-109">자세한 내용은 참조 [설명서 hello](./diagnostic-extension.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="969bd-110">Azure 포털을 통해 hello 모니터링 사용 안 함/설정</span><span class="sxs-lookup"><span data-stu-id="969bd-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="969bd-111">1분 동안 인스턴스에 대한 데이터를 제공하는 Azure VM의 모니터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="969bd-112">(저장소 변경 적용).</span><span class="sxs-lookup"><span data-stu-id="969bd-112">(storage changes apply).</span></span> <span data-ttu-id="969bd-113">자세한 진단 데이터는 hello 포털 그래프 또는 hello API 통해 hello VM에 사용할 수 있는 다음입니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="969bd-114">기본적으로 Azure Portal은 제한된 메트릭 집합의 호스트 기반 모니터링을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="969bd-115">중지 상태에서 또는 hello VM 실행 하는 동안 VM 내에서 메트릭을 모니터링 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="969bd-116">열기 hello Azure 포털에서 [https://portal.azure.com](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="969bd-117">왼쪽 탐색 hello, 가상 컴퓨터를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="969bd-118">Hello 목록 가상 컴퓨터에서 실행 중이거나 중지 된 인스턴스를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="969bd-119">hello "가상 컴퓨터" 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="969bd-120">모든 설정을 클릭합니다</span><span class="sxs-lookup"><span data-stu-id="969bd-120">Click All settings.</span></span>
* <span data-ttu-id="969bd-121">진단을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-121">Click Diagnostics.</span></span>
* <span data-ttu-id="969bd-122">상태 tooOn 변경 또는 해제 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-122">Change status tooOn or Off.</span></span> <span data-ttu-id="969bd-123">이 블레이드 hello 수준의 모니터링 원하는 tooenable 가상 컴퓨터에 대 한 세부 정보에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Enable/hello Azure 포털을 통해 모니터링을 사용 하지 않도록 설정 합니다.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="969bd-125">Azure CLI를 사용하는 모니터링 사용/사용 안 함</span><span class="sxs-lookup"><span data-stu-id="969bd-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="969bd-126">Azure VM에 대 한 tooenable 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="969bd-127">PrivateConfig.json과 같은 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="969bd-128">Azure CLI를 통해 hello 확장을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="969bd-129">자세한 내용은 참조 [를 사용 하 여 Linux 진단 확장 tooMonitor Linux VM의 성능 및 진단 데이터](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="969bd-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
