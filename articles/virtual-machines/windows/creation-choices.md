---
title: "Azure에서 Windows VM을 만드는 다양한 방법 | Microsoft Docs"
description: "리소스 관리자로 Windows 가상 컴퓨터를 만드는 다양한 방법을 나열합니다."
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
ms.openlocfilehash: 5e51c49aac01a22d86c7c1a12b2f2ca7ddc056bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="different-ways-to-create-a-windows-virtual-machine"></a><span data-ttu-id="eab6a-103">Windows 가상 컴퓨터를 만드는 다양한 방법</span><span class="sxs-lookup"><span data-stu-id="eab6a-103">Different ways to create a Windows virtual machine</span></span>

<span data-ttu-id="eab6a-104">가상 컴퓨터는 다양한 사용자와 목적에 맞게 조절 가능하기 때문에 Azure에서는 여러 방법으로 가상 컴퓨터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-104">Azure offers different ways to create a virtual machine because virtual machines are suited for different users and purposes.</span></span> <span data-ttu-id="eab6a-105">즉 가상 컴퓨터를 만드는 방법과 그에 대한 몇 가지 선택이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-105">This means that you need to make some choices about the virtual machine and how to create it.</span></span> <span data-ttu-id="eab6a-106">이 문서에서는 이 선택 사항 및 지침에 대한 링크 요약을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-106">This article gives you a summary of these choices and links to instructions.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="eab6a-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="eab6a-107">Azure portal</span></span>
<span data-ttu-id="eab6a-108">Azure 포털의 사용은 특히 Azure로 시작한 경우 가상 컴퓨터를 사용해 볼 수 있는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-108">Using the Azure portal is a simple way to try out a virtual machine, especially if you're just starting out with Azure.</span></span> 

[<span data-ttu-id="eab6a-109">포털에서 Windows를 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="eab6a-109">Create a virtual machine running Windows using the portal</span></span>](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a><span data-ttu-id="eab6a-110">Template</span><span class="sxs-lookup"><span data-stu-id="eab6a-110">Template</span></span>
<span data-ttu-id="eab6a-111">가상 컴퓨터에 가용성 집합 및 저장소 계정과 같은 리소스의 조합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-111">Virtual machines require a combination of resources (such as a availability sets and storage accounts).</span></span> <span data-ttu-id="eab6a-112">각 리소스를 개별적으로 배포하고 관리하는 대신, 모든 리소스를 하나의 조정된 작업으로 배포하고 프로비전하는 Azure Resource Manager 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-112">Rather than deploying and managing each resource separately, you can create an Azure Resource Manager template that deploys and provisions all of the resources in a single, coordinated operation.</span></span>

* [<span data-ttu-id="eab6a-113">리소스 관리자 템플릿을 사용하여 Windows 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="eab6a-113">Create a Windows virtual machine with a Resource Manager template</span></span>](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a><span data-ttu-id="eab6a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="eab6a-114">Azure PowerShell</span></span>
<span data-ttu-id="eab6a-115">명령 셸에서 작업하고 싶다면 Azure PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-115">If you prefer working in a command shell, you can use Azure PowerShell.</span></span>

* [<span data-ttu-id="eab6a-116">PowerShell을 사용하여 Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="eab6a-116">Create a Windows VM using PowerShell</span></span>](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a><span data-ttu-id="eab6a-117">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eab6a-117">Visual Studio</span></span>
<span data-ttu-id="eab6a-118">Visual Studio를 사용하여 Azure Tools for Visual Studio 및 Azure SDK로 VM을 빌드, 관리 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="eab6a-118">Use Visual Studio to build, manage, and deploy VMs with the Azure Tools for Visual Studio and the Azure SDK.</span></span>

[<span data-ttu-id="eab6a-119">Azure Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eab6a-119">Azure Tools for Visual Studio</span></span>](https://www.visualstudio.com/features/azure-tools-vs)

