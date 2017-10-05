---
title: "Azure CLI 1.0을 사용하여 클래식 Linux VM 만들기 | Microsoft Docs"
description: "Azure CLI 1.0에서 클래식 배포 모델을 사용하여 Linux 가상 컴퓨터를 만드는 방법에 대해 알아보기"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 8ddbacbbb70c0cf1a2537fab4d981a316610a4d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a><span data-ttu-id="34149-103">Azure CLI 1.0을 사용하여 클래식 Linux VM을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="34149-103">How to Create a Classic Linux VM with the Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="34149-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34149-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="34149-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="34149-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="34149-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="34149-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="34149-107">Resource Manager 버전은 [여기](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34149-107">For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="34149-108">이 항목에서는 Azure CLI 1.0에서 클래식 배포 모델을 사용하여 Linux VM(가상 컴퓨터)을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="34149-108">This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model.</span></span> <span data-ttu-id="34149-109">Azure에서 제공되는 **이미지** 의 Linux 이미지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="34149-109">We use a Linux image from the available **IMAGES** on Azure.</span></span> <span data-ttu-id="34149-110">Azure CLI 1.0 명령은 특히 다음과 같은 구성 선택 항목을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="34149-110">The Azure CLI 1.0 commands give the following configuration choices, among others:</span></span>

* <span data-ttu-id="34149-111">가상 네트워크에 VM 연결</span><span class="sxs-lookup"><span data-stu-id="34149-111">Connecting the VM to a virtual network</span></span>
* <span data-ttu-id="34149-112">기존 클라우드 서비스에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="34149-112">Adding the VM to an existing cloud service</span></span>
* <span data-ttu-id="34149-113">기존 저장소 계정에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="34149-113">Adding the VM to an existing storage account</span></span>
* <span data-ttu-id="34149-114">가용성 집합 또는 위치에 VM 추가</span><span class="sxs-lookup"><span data-stu-id="34149-114">Adding the VM to an availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34149-115">VM에서 가상 네트워크를 사용하여 호스트 이름으로 VM에 직접 연결하거나 프레미스 간 연결을 설정할 수 있게 하려는 경우 VM을 만들 때 가상 네트워크를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="34149-115">If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM.</span></span> <span data-ttu-id="34149-116">VM을 만드는 경우에만 가상 네트워크에 가입하도록 VM을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34149-116">A VM can be configured to join a virtual network only when you create the VM.</span></span> <span data-ttu-id="34149-117">가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 개요](http://go.microsoft.com/fwlink/p/?LinkID=294063)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="34149-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a><span data-ttu-id="34149-118">클래식 배포 모델을 사용하여 Linux VM을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="34149-118">How to create a Linux VM using the Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

