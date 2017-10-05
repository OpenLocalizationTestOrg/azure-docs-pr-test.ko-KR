---
title: "클래식 Linux VM에 대한 가용성 집합 | Microsoft Docs"
description: "Azure 포털 및 Azure PowerShell을 사용하여 클래식 배포 모델에서 새 가상 컴퓨터 또는 기존 Linux 가상 컴퓨터에 대한 가용성 집합을 구성합니다."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 41d427862150d17e1ad726afc51114d6f62f5a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-linux-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="b7f1f-103">클래식 배포 모델에서 Linux 가상 컴퓨터에 대한 가용성 집합을 구성하는 방법</span><span class="sxs-lookup"><span data-stu-id="b7f1f-103">How to configure an availability set for Linux virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b7f1f-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7f1f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b7f1f-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7f1f-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b7f1f-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b7f1f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b7f1f-107">또한 리소스 관리자 배포에서 [가용성 집합을 구성](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7f1f-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]