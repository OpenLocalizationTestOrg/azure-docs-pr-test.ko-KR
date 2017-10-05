---
title: "Windows 클래식 VM에 대한 가용성 집합 | Microsoft Docs"
description: "Azure 포털 및 Azure PowerShell을 사용하여 클래식 배포 모델에서 새 Windows 가상 컴퓨터 또는 기존 Windows 가상 컴퓨터에 대한 가용성 집합을 구성합니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c3b7fdec-fb59-4412-a4f4-f3a0b9c62e93
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: cynthn
ms.openlocfilehash: a5cbbdf402ee06a34a339b193b0cdd5c952d6248
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-windows-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="23c5c-103">클래식 배포 모델에서 Windows 가상 컴퓨터에 대한 가용성 집합을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="23c5c-103">How to configure an availability set for Windows virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="23c5c-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23c5c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="23c5c-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="23c5c-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="23c5c-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="23c5c-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="23c5c-107">또한 리소스 관리자 배포에서 [가용성 집합을 구성](../tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23c5c-107">You can also [configure availability sets](../tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]

