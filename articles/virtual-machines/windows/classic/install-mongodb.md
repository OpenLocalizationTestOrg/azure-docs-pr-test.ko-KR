---
title: "Azure에서 Windows VM에 MongoDB 설치 | Microsoft Docs"
description: "클래식 배포 모델을 사용하여 만든, Windows Server를 실행하는 Azure VM에 MongoDB를 설치하는 방법을 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 6b5af18d02fd508a21cdc21b38b1c16e79f07ecb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="8c4a9-103">Azure에서 Windows VM에 MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="8c4a9-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8c4a9-104">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8c4a9-105">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8c4a9-106">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8c4a9-107">Resource Manager 배포 모델을 사용하여 MongoDB를 설치하고 구성하려면 [이 문서](../install-mongodb.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-107">To install and configure MongoDB using the Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="8c4a9-108">[MongoDB][MongoDB]는 인기 있는 고성능 오픈 소스 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="8c4a9-109">이 문서에서는[Azure Portal][AzurePortal]을 사용하여 Windows Server VM(가상 컴퓨터)을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-109">This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal].</span></span> <span data-ttu-id="8c4a9-110">그런 다음 MongoDB를 설치하고 구성하기 전에 데이터 디스크를 만든 후 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-110">You then create and attach a data disk to the VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="8c4a9-111">Azure에 사용하려는 기존 VM이 있는 경우 [MongoDB 설치 및 구성](#install-and-run-mongodb-on-the-virtual-machine)단계로 바로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-111">If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="8c4a9-112">Windows Server를 실행하는 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8c4a9-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="8c4a9-113">가상 컴퓨터를 만들려면 다음 지침을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-113">Follow these instructions to create a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="8c4a9-114">가상 컴퓨터를 만드는 동안 MongoDB의 끝점을 추가하고 다음과 같이 구성할 수 있습니다. 이름을 **Mongo**로 지정하고 **TCP**를 프로토콜로 사용하고 공용 및 개인 포트를 모두 **27017**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-114">You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="8c4a9-115">데이터 디스크 연결</span><span class="sxs-lookup"><span data-stu-id="8c4a9-115">Attach a data disk</span></span>
<span data-ttu-id="8c4a9-116">가상 컴퓨터에 대한 저장소를 제공하려면 데이터 디스크를 연결한 다음 Windows에서 사용할 수 있도록 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-116">To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="8c4a9-117">데이터 디스크가 이미 있는 경우 해당 기존 디스크를 연결할 수도 있고 빈 디스크를 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="8c4a9-118">디스크 초기화 지침은 [Windows 가상 컴퓨터에 데이터 디스크를 연결하는 방법](attach-disk.md)에서 "방법: Windows Server에서 새 데이터 디스크 초기화"를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-118">For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-the-virtual-machine"></a><span data-ttu-id="8c4a9-119">가상 컴퓨터에서 MongoDB 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="8c4a9-119">Install and run MongoDB on the virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="8c4a9-120">요약</span><span class="sxs-lookup"><span data-stu-id="8c4a9-120">Summary</span></span>
<span data-ttu-id="8c4a9-121">이 자습서에서는 Windows Server를 실행하는 가상 컴퓨터를 만들고 가상 컴퓨터에 원격으로 연결한 다음 데이터 디스크를 연결하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-121">In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.</span></span>  <span data-ttu-id="8c4a9-122">또한 Windows 기반 가상 컴퓨터에 MongoDB를 설치 및 구성하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-122">You also learned how to install and configure MongoDB on the Windows-based virtual machine.</span></span> <span data-ttu-id="8c4a9-123">이제 [MongoDB 설명서][MongoDocs](영문)의 고급 항목에 따라 Windows 기반 가상 컴퓨터에서 MongoDB에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8c4a9-123">You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

