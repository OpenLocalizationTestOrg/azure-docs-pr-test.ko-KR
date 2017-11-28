---
title: "aaaDifferent 방법으로 Azure에서 Windows VM toocreate | Microsoft Docs"
description: "Hello 다양 한 방법 toocreate 리소스 관리자와 Windows 가상 컴퓨터를 나열합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a><span data-ttu-id="1d890-103">다양 한 방법 toocreate Windows 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="1d890-103">Different ways toocreate a Windows virtual machine</span></span>

<span data-ttu-id="1d890-104">Azure 가상 컴퓨터는 여러 사용자 및 목적에 적합 하기 때문에 가상 컴퓨터를 다른 방법으로 toocreate를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d890-104">Azure offers different ways toocreate a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="1d890-105">즉, 있습니다 toomake hello 가상 컴퓨터에 대 한 몇 가지 옵션 및 방법을 toocreate 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1d890-105">This means that you need toomake some choices about hello virtual machine and how toocreate it.</span></span> <span data-ttu-id="1d890-106">이 문서는 이러한 방법에 대 한 요약을 제공 하 고 tooinstructions 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="1d890-106">This article gives you a summary of these choices and links tooinstructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="1d890-107">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1d890-107">Azure portal</span></span>
<span data-ttu-id="1d890-108">Hello Azure 포털을 사용 하 여 가상 컴퓨터는 간단한 방법을 tootry는 특히 시작한 Azure와 함께 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1d890-108">Using hello Azure portal is a simple way tootry out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="1d890-109">Hello 포털을 사용 하 여 Windows를 실행 하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1d890-109">Create a virtual machine running Windows using hello portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="1d890-110">템플릿</span><span class="sxs-lookup"><span data-stu-id="1d890-110">Template</span></span>
<span data-ttu-id="1d890-111">가상 컴퓨터에 가용성 집합 및 저장소 계정과 같은 리소스의 조합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1d890-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="1d890-112">배포의 각 리소스를 별도로 관리 하는 대신 배포 하 고 모든 단일, 통합 작업에서 hello 리소스를 프로 비전 하는 Azure 리소스 관리자 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d890-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of hello resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="1d890-113">리소스 관리자 템플릿을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1d890-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="1d890-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d890-114">Azure PowerShell</span></span>
<span data-ttu-id="1d890-115">명령 셸에서 작업하고 싶다면 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1d890-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="1d890-116">PowerShell을 사용하여 Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="1d890-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="1d890-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d890-117">Visual Studio</span></span>
<span data-ttu-id="1d890-118">Visual Studio toobuild를 사용 하 여, 관리 및 Visual Studio에 대 한 hello Azure tools는 Vm을 배포 및 Azure SDK hello</span><span class="sxs-lookup"><span data-stu-id="1d890-118">Use Visual Studio toobuild, manage, and deploy VMs with hello Azure Tools for Visual Studio and hello Azure SDK.</span></span>

[<span data-ttu-id="1d890-119">Azure Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1d890-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

