---
title: "클래식 Linux Vm에 대해 aaaAvailability 설정 | Microsoft Docs"
description: "가용성 집합을 hello Azure 포털 및 Azure PowerShell을 사용 하 여 hello 클래식 배포 모델에서 기존 또는 새 Linux 가상 컴퓨터를 구성 합니다."
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
ms.openlocfilehash: 8d8d041e3540e42a1921f5665469a2fdcaa30a29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-linux-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="da4c3-103">Tooconfigure 가용성에 대해 어떻게 설정 hello 클래식 배포 모델에서 Linux 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="da4c3-103">How tooconfigure an availability set for Linux virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="da4c3-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da4c3-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="da4c3-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="da4c3-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="da4c3-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="da4c3-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="da4c3-107">또한 리소스 관리자 배포에서 [가용성 집합을 구성](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da4c3-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]