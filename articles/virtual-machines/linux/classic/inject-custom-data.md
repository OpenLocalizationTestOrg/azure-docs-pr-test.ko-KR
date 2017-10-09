---
title: "aaaInject 데이터를 Azure에서 Linux Vm의 경우 | Microsoft Docs"
description: "이 항목에서는 방법을 tooinject에 사용자 지정 데이터를 Azure 가상 컴퓨터 때 설명 hello 인스턴스가 생성 되 고 어떻게 toolocate hello Windows 또는 Linux에서 사용자 지정 데이터입니다."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: d376093c-e01d-4ee3-a826-2b5a35caaa7e
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: a3197e06a8d367eab6336577e5cfb6d2d6858441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="6b075-103">Azure 가상 컴퓨터에 사용자 지정 데이터 삽입</span><span class="sxs-lookup"><span data-stu-id="6b075-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="6b075-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b075-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6b075-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b075-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6b075-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6b075-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6b075-107">사용자 지정 스크립트 확장이 hello hello 리소스 관리자 model과 함께 사용 하는 방법에 대 한 내용은 [여기](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="6b075-107">For information about using hello Custom Script Extension with hello Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

