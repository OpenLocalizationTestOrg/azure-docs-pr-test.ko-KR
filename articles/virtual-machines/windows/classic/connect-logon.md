---
title: "aaaLog tooa에 클래식 Azure VM | Microsoft Docs"
description: "Azure 포털 toolog hello를 사용 하 여 hello 클래식 배포 모델을 사용 하 여 만든 tooa Windows 가상 컴퓨터."
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
ms.openlocfilehash: 2e32b7036c2538e73b46580e0f5f8f4979e8a685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="log-on-tooa-windows-virtual-machine-using-hello-azure-portal"></a><span data-ttu-id="9d521-103">로그온 tooa hello Azure 포털을 사용 하 여 Windows 가상 컴퓨터</span><span class="sxs-lookup"><span data-stu-id="9d521-103">Log on tooa Windows virtual machine using hello Azure portal</span></span>
<span data-ttu-id="9d521-104">Hello Azure 포털을 사용 하 여 hello **연결** 원격 데스크톱 세션 toostart 단추 및 tooa Windows VM에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-104">In hello Azure portal, you use hello **Connect** button toostart a Remote Desktop session and log on tooa Windows VM.</span></span>

<span data-ttu-id="9d521-105">Linux VM tooconnect tooa 하 시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="9d521-105">Do you want tooconnect tooa Linux VM?</span></span> <span data-ttu-id="9d521-106">참조 [어떻게 Linux를 실행 하는 tooa 가상 컴퓨터에서 toolog](../../linux/mac-create-ssh-keys.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-106">See [How toolog on tooa virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how too[perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="9d521-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9d521-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="9d521-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="9d521-110">모델을 사용 하 여 tooa VM에 toolog 리소스 관리자 hello 하는 방법에 대 한 정보에 대 한 참고 하십시오 [여기](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-110">For information about how toolog on tooa VM using hello Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="9d521-111">Toohello 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="9d521-111">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="9d521-112">Azure 포털 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="9d521-113">원하는 tooaccess hello 가상 컴퓨터에서 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-113">Click on hello virtual machine that you want tooaccess.</span></span> <span data-ttu-id="9d521-114">hello 이름이 hello에 나열 되어 **모든 리소스** 창.</span><span class="sxs-lookup"><span data-stu-id="9d521-114">hello name is listed in hello **All resources** pane.</span></span>

    ![Virtual-machine-locations](./media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="9d521-116">클릭 **연결** hello 가상 컴퓨터 대시보드 맨 위에 있는 hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-116">Click **Connect** on hello command bar atop hello virtual machine dashboard.</span></span>

    ![연결 hello 가상 컴퓨터에 대 한 아이콘](./media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If hello **Connect** button isn't available, see hello troubleshooting tips at hello end of this article.
>
>
-->

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="9d521-118">Toohello 가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="9d521-118">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="9d521-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9d521-119">Next steps</span></span>
* <span data-ttu-id="9d521-120">경우 hello **연결** 단추는 비활성화 또는 hello 원격 데스크톱 연결에 다른 문제가 발생 하는, hello 구성을 다시 설정 해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-120">If hello **Connect** button is inactive or you are having other problems with hello Remote Desktop connection, try resetting hello configuration.</span></span> <span data-ttu-id="9d521-121">클릭 **원격 액세스를 다시 설정** hello 가상 컴퓨터 대시보드에서.</span><span class="sxs-lookup"><span data-stu-id="9d521-121">click **Reset remote access** from hello virtual machine dashboard.</span></span>

    ![Reset-remote-access](./media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="9d521-123">암호에 문제가 있는 경우 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="9d521-124">클릭 **암호 재설정** hello 따라 왼쪽 가장자리의 가상 컴퓨터 대시보드 아래 **지원 + 문제 해결**합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-124">Click **Reset password** along hello left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](./media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="9d521-126">이러한 팁 작동 하지 않는지 또는 필요한 참조 되지 않습니다. 경우 [Windows 기반 Azure 가상 컴퓨터 문제를 해결 하는 원격 데스크톱 연결 tooa](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9d521-127">이 문서에서는 일반적인 문제를 진단 및 해결하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9d521-127">This article walks you through diagnosing and resolving common problems.</span></span>
