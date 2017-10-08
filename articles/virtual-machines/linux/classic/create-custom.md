---
title: "사용 하 여 클래식 Linux VM aaaCreate hello Azure CLI 1.0 | Microsoft Docs"
description: "Toocreate hello Azure CLI 1.0 사용 하 여 Linux 가상 컴퓨터를 클래식 배포 모델을 hello 하는 방법에 대해 알아봅니다"
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
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a><span data-ttu-id="0fe6a-103">클래식 Linux VM a tooCreate Azure CLI 1.0 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0fe6a-103">How tooCreate a Classic Linux VM with hello Azure CLI 1.0</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0fe6a-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0fe6a-105">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0fe6a-106">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0fe6a-107">Hello 리소스 관리자 버전에 대 한 참조 [여기](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-107">For hello Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0fe6a-108">이 항목에서는 toocreate hello Azure CLI 1.0 사용 하 여 Linux 가상 컴퓨터 (VM) 클래식 배포 모델을 hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-108">This topic describes how toocreate a Linux virtual machine (VM) with hello Azure CLI 1.0 using hello Classic deployment model.</span></span> <span data-ttu-id="0fe6a-109">사용 가능한 hello에서 Linux 이미지를 사용 하 여 우리 **이미지** Azure에서.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-109">We use a Linux image from hello available **IMAGES** on Azure.</span></span> <span data-ttu-id="0fe6a-110">hello Azure CLI 1.0 명령을 각기 다른 규칙 으로부터 구성 선택 항목을 다음 hello 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-110">hello Azure CLI 1.0 commands give hello following configuration choices, among others:</span></span>

* <span data-ttu-id="0fe6a-111">Hello VM tooa 가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="0fe6a-111">Connecting hello VM tooa virtual network</span></span>
* <span data-ttu-id="0fe6a-112">Hello VM tooan 기존 클라우드 서비스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-112">Adding hello VM tooan existing cloud service</span></span>
* <span data-ttu-id="0fe6a-113">Hello VM tooan 기존 저장소 계정 추가</span><span class="sxs-lookup"><span data-stu-id="0fe6a-113">Adding hello VM tooan existing storage account</span></span>
* <span data-ttu-id="0fe6a-114">Hello VM tooan 가용성 집합이 나 위치를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-114">Adding hello VM tooan availability set or location</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fe6a-115">호스트 이름 또는 크로스-프레미스 연결을 설정 하 여 직접 tooit 연결할 수 있도록 가상 네트워크에 VM toouse를 원하는 경우 hello VM을 만들 때 hello 가상 네트워크를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-115">If you want your VM toouse a virtual network so you can connect tooit directly by hostname or set up cross-premises connections, make sure you specify hello virtual network when you create hello VM.</span></span> <span data-ttu-id="0fe6a-116">Hello VM을 만드는 경우에 VM 가상 네트워크 구성된 toojoin을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-116">A VM can be configured toojoin a virtual network only when you create hello VM.</span></span> <span data-ttu-id="0fe6a-117">가상 네트워크에 대한 자세한 내용은 [Azure 가상 네트워크 개요](http://go.microsoft.com/fwlink/p/?LinkID=294063)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0fe6a-117">For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).</span></span>
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a><span data-ttu-id="0fe6a-118">어떻게 사용 하 여 Linux VM a toocreate hello 클래식 배포 모델</span><span class="sxs-lookup"><span data-stu-id="0fe6a-118">How toocreate a Linux VM using hello Classic deployment model</span></span>
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

