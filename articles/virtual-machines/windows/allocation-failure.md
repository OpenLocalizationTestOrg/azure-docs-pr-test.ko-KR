---
title: "Windows VM 할당 오류 aaaTroubleshooting | Microsoft Docs"
description: "Azure에서 Windows VM을 만들거나 재시작하거나 크기를 조정하는 경우 할당 오류 해결"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: d0cc75ac60d952d8e4310cebc37654dc4f80857f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="aa5a9-103">Azure에서 Windows VM을 만들거나 재시작하거나 크기를 조정하는 경우 할당 오류 해결</span><span class="sxs-lookup"><span data-stu-id="aa5a9-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="aa5a9-104">VM 만들기, 중지 (할당 취소) Vm을 다시 시작 하거나 VM의 크기를 조정 하는 경우 Microsoft Azure 계산 리소스 할당 tooyour 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa5a9-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="aa5a9-105">Hello Azure 구독 제한에 도달 하기 전에도-이러한 작업을 수행 하는 경우에 가끔 오류가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa5a9-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="aa5a9-106">이 문서는 hello 원인을 hello 일반적인 할당 오류 중 일부에 대해 설명 하 고 해결할 수를 제안 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa5a9-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="aa5a9-107">서비스의 hello 배포를 계획 하는 경우에 hello 정보 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa5a9-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="aa5a9-108">[Azure에서 Linux VM을 만들거나 재시작하거나 크기를 조정하는 경우 할당 오류를 해결](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa5a9-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

