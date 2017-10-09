---
title: "Linux 가상 컴퓨터에서 SAP aaaUsing | Microsoft Docs"
description: "Microsoft Azure의 Linux VM(가상 컴퓨터)에서 SAP를 사용하는 방법을 알아봅니다."
services: virtual-machines-linux,virtual-network,storage
documentationcenter: saponazure
author: MSSedusch
manager: timlt
editor: 
tags: azure-service-management
keywords: 
ms.assetid: f9cd93dc-71ad-48a4-8778-4e48aec484a6
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: campaign-page
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 10/04/2016
ms.author: sedusch
ms.openlocfilehash: fd4aad83d99ef5286488aaab6552fd67a5e35a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="36af2-103">Azure의 Linux 가상 컴퓨터에서 SAP 사용</span><span class="sxs-lookup"><span data-stu-id="36af2-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="36af2-104">클라우드 컴퓨팅은 toolarge 및 다국적 회사를 중소 기업에서 점점 더 많은 중요도 hello IT 업계 내에서 취소 하는 널리 사용 되는 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-104">Cloud Computing is a widely used term which is gaining more and more importance within hello IT industry, from small companies up toolarge and multinational corporations.</span></span> <span data-ttu-id="36af2-105">Microsoft Azure는 hello 새로운 작업 방식을 폭넓게 제공 된 microsoft에서 클라우드 서비스 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-105">Microsoft Azure is hello Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="36af2-106">이제 고객은 수 toorapidly 프로 비전 및 프로 비전 해제 응용 프로그램 클라우드 서비스로 제한 된 tootechnical 또는 예산 제한 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-106">Now customers are able toorapidly provision and de-provision applications as Cloud-Services, so they are not limited tootechnical or budgeting restrictions.</span></span> <span data-ttu-id="36af2-107">하드웨어 인프라에 시간과 예산을 투자를 하는 대신 고객 및 사용자에 대 한 회사는 hello 응용 프로그램 및 비즈니스 프로세스의 장점에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-107">Instead of investing time and budget into hardware infrastructure, companies can focus on hello application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="36af2-108">Microsoft는 Microsoft Azure 가상 컴퓨터와 함께 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="36af2-109">SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="36af2-110">아래 hello 백서 tooplan 및 구현 SAP NetWeaver 기반 Azure에서 Windows 가상 컴퓨터에 응용 프로그램에 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-110">hello whitepapers below describe how tooplan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="36af2-111">[Windows 가상 컴퓨터](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에서 SAP NetWeaver 기반 응용 프로그램을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../virtual-machines-windows-classic-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="36af2-112">Azure SUSE Linux 가상 컴퓨터에서 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="36af2-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="36af2-113">제목: Microsoft Azure SUSE Linux Vm에서의 SAP NetWeaver aaaTesting</span><span class="sxs-lookup"><span data-stu-id="36af2-113">title: aaaTesting SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="36af2-114">요약: 현 시점에는 Azure Linux VM에서의 SAP NetWeaver 실행에 대해 SAP에서 공식적으로 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="36af2-115">그럼에도 불구 하 고 고객 toodo 일부 테스트 하거나 것을 고려할 수 toorun Azure Linux Vm에서 SAP 데모 또는 학습 시스템으로 SAP 지원 팀에 연락 하는 것에 대 한 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-115">Nevertheless customers might want toodo some testing or might consider toorun SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="36af2-116">이 문서는 Azure SUSE Linux Vm 설정 SAP를 실행 하는 데 도움이 됩니다 하 고 tooavoid 일반적인 잠재적인 문제 순서로 일부 기본적인 힌트를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order tooavoid common potential pitfalls.</span></span>

<span data-ttu-id="36af2-117">업데이트한 날짜: 2015년 12월</span><span class="sxs-lookup"><span data-stu-id="36af2-117">Updated: December 2015</span></span>

[<span data-ttu-id="36af2-118">이 문서는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="36af2-118">This article can be found here</span></span>](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

