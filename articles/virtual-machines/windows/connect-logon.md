---
title: Windows Server VM aaaConnect tooa | Microsoft Docs
description: "어떻게 tooconnect 및 tooa Windows VM 사용 하 여 로그온 hello Azure 포털 및 hello 리소스 관리자 배포 모델에 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="9b5ae-103">어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="9b5ae-104">Hello를 사용 하 여 **연결** hello Azure 포털 toostart Windows 바탕 화면에서 RDP (원격 데스크톱) 세션에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="9b5ae-105">먼저 toohello 가상 컴퓨터를 연결 하면 다음에 로그온 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="9b5ae-106">Mac 용 RDP 클라이언트가 같은 tooinstall tooconnect tooa Mac에서 Windows VM을 시도 하는 경우 해야 [Microsoft 원격 데스크톱](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="9b5ae-107">Toohello 가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="9b5ae-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="9b5ae-108">그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9b5ae-109">Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="9b5ae-110">Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="9b5ae-111">Hello 가상 컴퓨터에 대 한 hello 블레이드에서 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Hello Azure 포털 보여 주는 스크린샷 어떻게 tooconnect tooyour VM입니다.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="9b5ae-113">경우 hello **연결** hello 포털에서 단추는 회색을 통해 연결 된 tooAzure 없습니다는 [Express 경로](../../expressroute/expressroute-introduction.md) 또는 [사이트 간 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 연결을 toocreate 필요 하 고 RDP를 사용 하려면 먼저 VM 공용 IP 주소를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="9b5ae-114">자세한 내용은 [Azure의 공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="9b5ae-115">Toohello 가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="9b5ae-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="9b5ae-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9b5ae-116">Next steps</span></span>
<span data-ttu-id="9b5ae-117">Tooconnect 려 할 때 문제를 실행 하면 참조 [문제를 해결 하는 원격 데스크톱 연결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9b5ae-118">이 문서에서는 일반적인 문제를 진단 및 해결하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="9b5ae-118">This article walks you through diagnosing and resolving common problems.</span></span>

