---
title: "클래식 Azure VM에 로그온 | Microsoft Docs"
description: "Azure Portal을 사용하여 클래식 배포 모델로 만든 Windows 가상 컴퓨터에 로그온할 수 있습니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 43d54de7e875de9212c23c49ad0539bf2272a312
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="57fd0-103">Azure 포털을 사용하여 Windows 가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="57fd0-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="57fd0-104">Azure 포털에서 **연결** 단추를 사용하여 원격 데스크톱 세션을 시작하고 Windows VM에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="57fd0-105">Linux VM에 연결하고 싶으세요?</span><span class="sxs-lookup"><span data-stu-id="57fd0-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="57fd0-106">[Linux를 실행하는 가상 컴퓨터에 로그온하는 방법](../../linux/mac-create-ssh-keys.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57fd0-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="57fd0-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="57fd0-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="57fd0-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="57fd0-110">Resource Manager 모델을 사용하여 VM에 로그온하는 방법에 대한 정보는 [여기](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57fd0-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="57fd0-111">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="57fd0-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="57fd0-112">Azure 포털에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="57fd0-113">액세스할 가상 컴퓨터를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="57fd0-114">이름은 **모든 리소스** 창에 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-114">The name is listed in the **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="57fd0-116">가상 컴퓨터 대시보드 위쪽의 명령 모음에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![가상 컴퓨터의 연결 아이콘](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="57fd0-118">가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="57fd0-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="57fd0-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57fd0-119">Next steps</span></span>
* <span data-ttu-id="57fd0-120">**연결** 단추가 비활성 상태이거나 원격 데스크톱 연결에 다른 문제가 있는 경우 구성을 다시 설정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="57fd0-121">가상 컴퓨터 대시보드에서 **원격 액세스 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="57fd0-123">암호에 문제가 있는 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="57fd0-124">**지원 + 문제 해결** 아래에서 가상 컴퓨터 대시보드의 왼쪽 가장자리를 따라 **암호 재설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="57fd0-126">이러한 팁이 작동하지 않거나 필요한 정보가 아닌 경우 [Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="57fd0-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="57fd0-127">이 문서에서는 일반적인 문제를 진단 및 해결하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="57fd0-127">This article walks you through diagnosing and resolving common problems.</span></span>
