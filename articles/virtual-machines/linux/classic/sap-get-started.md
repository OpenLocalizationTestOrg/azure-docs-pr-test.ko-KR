---
title: "Linux 가상 컴퓨터에서 SAP 사용 | Microsoft Docs"
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
ms.openlocfilehash: 078865245989578d17b6eb0b59b379aa2056f31c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="using-sap-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="d6518-103">Azure의 Linux 가상 컴퓨터에서 SAP 사용</span><span class="sxs-lookup"><span data-stu-id="d6518-103">Using SAP on Linux virtual machines in Azure</span></span>
<span data-ttu-id="d6518-104">클라우드 컴퓨팅은 중소 기업에서 대기업 및 다국적 기업까지 IT 업계 내에서 점점 더 중요해지는 널리 사용되는 용어입니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-104">Cloud Computing is a widely used term which is gaining more and more importance within the IT industry, from small companies up to large and multinational corporations.</span></span> <span data-ttu-id="d6518-105">Microsoft Azure는 다양한 새로운 가능성을 제공하는 Microsoft의 클라우드 서비스 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-105">Microsoft Azure is the Cloud Services Platform from Microsoft which offers a wide spectrum of new possibilities.</span></span> <span data-ttu-id="d6518-106">이제 고객은 클라우드 서비스로 응용 프로그램을 신속하게 프로비전 및 프로비전 해제할 수 있으므로 기술 또는 예산 제한에 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-106">Now customers are able to rapidly provision and de-provision applications as Cloud-Services, so they are not limited to technical or budgeting restrictions.</span></span> <span data-ttu-id="d6518-107">하드웨어 인프라에 시간과 예산을 투자하는 대신 기업은 고객 및 사용자를 위한 응용 프로그램, 비즈니스 프로세스 및 그 이점에 집중할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-107">Instead of investing time and budget into hardware infrastructure, companies can focus on the application, business processes and its benefits for customers and users.</span></span>

<span data-ttu-id="d6518-108">Microsoft는 Microsoft Azure 가상 컴퓨터와 함께 포괄적인 IaaS(Infrastructure as a Service) 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-108">With Microsoft Azure virtual machines, Microsoft offers a comprehensive Infrastructure as a Service (IaaS) platform.</span></span> <span data-ttu-id="d6518-109">SAP NetWeaver 기반 응용 프로그램은 Azure 가상 컴퓨터(IaaS)에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-109">SAP NetWeaver based applications are supported on Azure Virtual Machines (IaaS).</span></span> <span data-ttu-id="d6518-110">아래 백서는 Azure의 Windows 가상 컴퓨터에서 SAP NetWeaver 기반 응용 프로그램을 계획하고 구현하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-110">The whitepapers below describe how to plan and implement SAP NetWeaver based applications on Windows virtual machines in Azure.</span></span> <span data-ttu-id="d6518-111">[Windows 가상 컴퓨터](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)에서 SAP NetWeaver 기반 응용 프로그램을 구현할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-111">You can also implement SAP NetWeaver based applications on [Windows virtual machines](../../windows/classic/sap-get-started.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-sap-get-started](../../../../includes/virtual-machines-common-classic-sap-get-started.md)]

## <a name="sap-netweaver-on-azure-suse-linux-virtual-machines"></a><span data-ttu-id="d6518-112">Azure SUSE Linux 가상 컴퓨터에서 SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="d6518-112">SAP NetWeaver on Azure SUSE Linux Virtual Machines</span></span>
<span data-ttu-id="d6518-113">제목: Microsoft Azure SUSE Linux VM에서 SAP NetWeaver 테스트</span><span class="sxs-lookup"><span data-stu-id="d6518-113">Title: Testing SAP NetWeaver on Microsoft Azure SUSE Linux VMs</span></span>

<span data-ttu-id="d6518-114">요약: 현 시점에는 Azure Linux VM에서의 SAP NetWeaver 실행에 대해 SAP에서 공식적으로 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-114">Summary: There is no official SAP support for running SAP NetWeaver on Azure Linux VMs at this point in time.</span></span> <span data-ttu-id="d6518-115">그렇기는 하지만 고객이 SAP 지원에 문의할 필요가 없다면 Azure Linux VM에서 일부 테스트를 수행하거나 SAP 데모 또는 교육 시스템 실행을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-115">Nevertheless customers might want to do some testing or might consider to run SAP demo or training systems on Azure Linux VMs as long as there is no need for contacting SAP support.</span></span> <span data-ttu-id="d6518-116">이 문서는 SAP를 실행할 수 있도록 Azure SUSE Linux VM을 설정하는 데 도움을 주며 일반적으로 일어날 수 있는 위험을 방지하기 위한 몇 가지 기본적인 힌트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-116">This article should help setting up Azure SUSE Linux VMs for running SAP and gives some basic hints in order to avoid common potential pitfalls.</span></span>

<span data-ttu-id="d6518-117">업데이트한 날짜: 2015년 12월</span><span class="sxs-lookup"><span data-stu-id="d6518-117">Updated: December 2015</span></span>

[<span data-ttu-id="d6518-118">이 문서는 여기서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d6518-118">This article can be found here</span></span>](../../virtual-machines-linux-sap-on-suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

