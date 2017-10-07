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
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행 합니다.
Hello를 사용 하 여 **연결** hello Azure 포털 toostart Windows 바탕 화면에서 RDP (원격 데스크톱) 세션에서 단추입니다. 먼저 toohello 가상 컴퓨터를 연결 하면 다음에 로그온 합니다.

Mac 용 RDP 클라이언트가 같은 tooinstall tooconnect tooa Mac에서 Windows VM을 시도 하는 경우 해야 [Microsoft 원격 데스크톱](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417)합니다.

## <a name="connect-toohello-virtual-machine"></a>Toohello 가상 컴퓨터에 연결
1. 그렇게 이미 하지 않은 경우 toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.
2. Hello 허브 메뉴에서 클릭 **가상 컴퓨터**합니다.
3. Hello 목록에서 hello 가상 컴퓨터를 선택 합니다.
4. Hello 가상 컴퓨터에 대 한 hello 블레이드에서 클릭 **연결**합니다.
   
    ![Hello Azure 포털 보여 주는 스크린샷 어떻게 tooconnect tooyour VM입니다.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > 경우 hello **연결** hello 포털에서 단추는 회색을 통해 연결 된 tooAzure 없습니다는 [Express 경로](../../expressroute/expressroute-introduction.md) 또는 [사이트 간 VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 연결을 toocreate 필요 하 고 RDP를 사용 하려면 먼저 VM 공용 IP 주소를 할당 합니다. 자세한 내용은 [Azure의 공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)에서 확인할 수 있습니다.
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Toohello 가상 컴퓨터에 로그온
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>다음 단계
Tooconnect 려 할 때 문제를 실행 하면 참조 [문제를 해결 하는 원격 데스크톱 연결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다. 이 문서에서는 일반적인 문제를 진단 및 해결하는 과정을 안내합니다.

