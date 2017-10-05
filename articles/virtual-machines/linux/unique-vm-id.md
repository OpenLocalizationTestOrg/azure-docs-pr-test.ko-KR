---
title: "Azure Linux VM ID 가져오기 | Microsoft Docs"
description: "Azure Linux VM 고유 ID를 가져와 사용하는 방법을 설명합니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="ae559-103">Azure VM 고유 ID 액세스 및 사용</span><span class="sxs-lookup"><span data-stu-id="ae559-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="ae559-104">Azure VM 고유 ID는 128비트 식별자로 인코딩된 후 모든 Azure IaaS VM의 SMBIOS에 저장되며, 현재 플랫폼 BIOS 명령을 사용하여 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="ae559-105">Azure VM 고유 ID는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="ae559-106">Azure 고유 VM ID는 재부팅 종료(계획된 경우 또는 계획되지 않은 경우), 할당 해제 시작/중지, 서비스 복구 또는 위치로 복원 시 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="ae559-107">그러나 VM이 스냅숏이고 새 인스턴스를 만들기 위해 복사되면 새 Azure VM ID가 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="ae559-108">이 기능이 롤아웃된 이후(2014년 9월 18일) 이전 VM을 만들어 실행한 경우 VM을 다시 시작하여 Azure 고유 ID를 자동으로 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="ae559-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="ae559-109">VM 내에서 Azure 고유 VM ID에 액세스하려면</span><span class="sxs-lookup"><span data-stu-id="ae559-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="ae559-110">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ae559-110">Create a VM</span></span>
<span data-ttu-id="ae559-111">자세한 내용은 [가상 컴퓨터 만들기](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae559-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="ae559-112">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="ae559-112">Connect to the VM</span></span>
<span data-ttu-id="ae559-113">자세한 내용은 [Linux의 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ae559-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="ae559-114">VM 고유 ID 쿼리</span><span class="sxs-lookup"><span data-stu-id="ae559-114">Query VM Unique ID</span></span>
<span data-ttu-id="ae559-115">명령(예제에서는 **Ubuntu**사용):</span><span class="sxs-lookup"><span data-stu-id="ae559-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="ae559-116">예제의 예상 결과:</span><span class="sxs-lookup"><span data-stu-id="ae559-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="ae559-117">Big Endian 비트 순서 때문에, 이 경우의 실제 고유 VM ID는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="ae559-118">Azure VM 고유 ID는 VM이 Azure 또는 온-프레미스에서 실행되는 다양한 시나리오에서 사용될 수 있으며, Azure IaaS 배포에서 발생할 수 있는 라이선스, 보고 또는 일반 추적 요구 사항에도 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="ae559-119">응용 프로그램을 구축하고 Azure에서 인증을 받는 많은 독립 소프트웨어 공급업체는 전체 수명 주기 동안 Azure VM을 식별하고, VM이 Azure, 온-프레미스 또는 기타 클라우드 공급자 중 어디에서 실행되는지 파악해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="ae559-120">예를 들어 이 플랫폼 식별자는 소프트웨어의 사용이 제대로 허가되는지 여부를 감지하거나 VM 데이터와 원본 간 상관 관계를 파악하는 데 도움이 되므로 올바른 플랫폼에 대해 올바른 메트릭을 설정할 수 있도록 하고, 이러한 메트릭을 추적하고 다양한 경우에 상관 관계를 파악할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ae559-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>

