---
title: "Windows Server VM에 연결 | Microsoft Docs"
description: "Azure 포털 및 리소스 관리자 배포 모델을 사용하여 Windows VM에 연결 및 로그온하는 방법을 알아봅니다."
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
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="5a699-103">Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법</span><span class="sxs-lookup"><span data-stu-id="5a699-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="5a699-104">Azure Portal의 **연결** 단추를 사용하여 Windows 데스크톱에서 RDP(원격 데스크톱) 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="5a699-105">먼저 가상 컴퓨터에 연결한 다음 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="5a699-106">Mac에서 Windows VM에 연결하려는 경우 [Microsoft 원격 데스크톱](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417)과 같이 Mac용 RDP 클라이언트를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="5a699-107">가상 컴퓨터에 연결</span><span class="sxs-lookup"><span data-stu-id="5a699-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="5a699-108">아직 로그인하지 않은 경우 [Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5a699-109">허브 메뉴에서 **가상 컴퓨터**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="5a699-110">목록에서 가상 컴퓨터를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="5a699-111">가상 컴퓨터 블레이드에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![VM에 연결하는 방법을 보여 주는 Azure 포털의 스크린샷입니다.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="5a699-113">포털에서 **연결** 단추가 회색으로 표시되고 [Express 경로](../../expressroute/expressroute-introduction.md) 또는 [사이트 간 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 연결을 통해 Azure에 연결되지 않는 경우 RDP를 사용하려면 먼저 공용 IP 주소를 만들고 VM에 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="5a699-114">자세한 내용은 [Azure의 공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="5a699-115">가상 컴퓨터에 로그온</span><span class="sxs-lookup"><span data-stu-id="5a699-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="5a699-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5a699-116">Next steps</span></span>
<span data-ttu-id="5a699-117">연결하려고 할 때 문제가 발생할 경우 [원격 데스크톱 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a699-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5a699-118">이 문서에서는 일반적인 문제를 진단 및 해결하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="5a699-118">This article walks you through diagnosing and resolving common problems.</span></span>

