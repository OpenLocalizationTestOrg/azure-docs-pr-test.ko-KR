---
title: Azure Linux VM ID aaaGet | Microsoft Docs
description: "설명 방법을 사용 하 여 tooget Azure Linux VM 고유 id입니다."
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
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="182e6-103">Azure VM 고유 ID 액세스 및 사용</span><span class="sxs-lookup"><span data-stu-id="182e6-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="182e6-104">Azure VM 고유 ID는 128비트 식별자로 인코딩된 후 모든 Azure IaaS VM의 SMBIOS에 저장되며, 현재 플랫폼 BIOS 명령을 사용하여 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="182e6-105">Azure VM 고유 ID는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="182e6-106">Azure 고유 VM ID는 재부팅 종료(계획된 경우 또는 계획되지 않은 경우), 할당 해제 시작/중지, 서비스 복구 또는 위치로 복원 시 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="182e6-107">그러나 VM hello 스냅숏 형식과 복사 toocreate 새 인스턴스를 새 Azure VM ID 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="182e6-108">VM tooautomatically Azure는 고유 ID를 가져올 이전 vm이 생성 하 고 다시 시작 하십시오이 새로운 기능 (를) 가져왔습니다 (2014 년 9 월 18 일)에 전달 하므로 실행 하는 경우</span><span class="sxs-lookup"><span data-stu-id="182e6-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="182e6-109">tooaccess Azure에서 고유한 VM ID hello VM 내:</span><span class="sxs-lookup"><span data-stu-id="182e6-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="182e6-110">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="182e6-110">Create a VM</span></span>
<span data-ttu-id="182e6-111">자세한 내용은 [가상 컴퓨터 만들기](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="182e6-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="182e6-112">Toohello VM 연결</span><span class="sxs-lookup"><span data-stu-id="182e6-112">Connect toohello VM</span></span>
<span data-ttu-id="182e6-113">자세한 내용은 [Linux의 SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="182e6-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="182e6-114">VM 고유 ID 쿼리</span><span class="sxs-lookup"><span data-stu-id="182e6-114">Query VM Unique ID</span></span>
<span data-ttu-id="182e6-115">명령(예제에서는 **Ubuntu**사용):</span><span class="sxs-lookup"><span data-stu-id="182e6-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="182e6-116">예제의 예상 결과:</span><span class="sxs-lookup"><span data-stu-id="182e6-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="182e6-117">TooBig Endian 비트 순서 인해 hello 실제 고유 VM ID이 경우 됩니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="182e6-118">Hello VM Azure에서 실행 되 고 또는 온-프레미스 및 라이선스 보고 또는 일반 추적 요구 사항을 Azure IaaS 배포에 있을 수 있습니다 수 있는지 여부를 다양 한 시나리오에서 azure VM의 고유 ID는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="182e6-119">많은 독립 소프트웨어 공급 업체 응용 프로그램을 구축 하 고 azure에 인증할 hello VM 다른 클라우드 공급자 또는 Azure에서 온-프레미스에서 실행 중인 경우 Azure VM의 수명 주기 및 tootell 전체 tooidentify가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="182e6-120">Hello 소프트웨어 올바르게 사용이 허가 하는 경우 검색 또는 toocorrelate tooassist hello 오른쪽 플랫폼과 tootrack에 대 한 hello 오른쪽 메트릭을 설정 등 모든 VM 데이터 tooits 소스 도움말과 이러한 메트릭 간에 상관 관계를 지정의 예를 들어이 플랫폼 식별자 활용 다른 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="182e6-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>

