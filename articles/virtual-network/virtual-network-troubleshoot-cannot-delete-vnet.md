---
title: "Azure에서 가상 네트워크를 삭제 하는 aaaCannot | Microsoft Docs"
description: "어떻게 tootroubleshoot hello Azure의 가상 네트워크를 삭제할 수는 없습니다 문제에 알아봅니다."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Azure의 가상 네트워크 toodelete 실패 문제 해결:

Microsoft Azure에서 가상 네트워크 toodelete 려 할 때 오류가 발생할 수 있습니다. 이 문서에서는 문제 해결 단계 toohelp이이 문제를 해결 합니다. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>문제 해결 지침 

1. [가상 네트워크 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network)합니다.
2. [응용 프로그램 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.](#check-whether-an-application-gateway-is-running-in-the-virtual-network)합니다.
3. [Azure Active Directory 도메인 서비스 hello 가상 네트워크에서 활성화 되어 있는지 여부를 확인](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network)합니다.
4. [Hello 가상 네트워크에 연결 된 tooother 리소스 인지 확인](#check-whether-the-virtual-network-is-connected-to-other-resource)합니다.
5. [Hello 가상 네트워크의 가상 컴퓨터가 여전히 실행 중인지 확인](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network)합니다.
6. [Hello 가상 네트워크 마이그레이션 걸려 있는지 여부를 확인](#check-whether-the-virtual-network-is-stuck-in-migration)합니다.

## <a name="troubleshooting-steps"></a>문제 해결 단계

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>가상 네트워크 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.

tooremove hello 가상 네트워크를 hello 가상 네트워크 게이트웨이 먼저 제거 해야 있습니다.

클래식 가상 네트워크에 대 한 이동 toohello **개요** hello Azure 포털의에서 hello 클래식 가상 네트워크의 페이지입니다. Hello에 **VPN 연결** 섹션에서 hello IP 표시는 hello 게이트웨이 hello 가상 네트워크에서 실행 중인 경우 hello 게이트웨이의 주소입니다. 

![게이트웨이가 실행 중인지 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

가상 네트워크에 대 한 이동 toohello **개요** hello 가상 네트워크의 페이지입니다. 확인 **연결 된 장치** hello 가상 네트워크 게이트웨이에 대 한 합니다.

![Hello 연결 된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Hello 게이트웨이 제거 하기 전에 먼저 제거 **연결** hello 게이트웨이의 개체입니다. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>응용 프로그램 게이트웨이 hello 가상 네트워크에서 실행 되 고 있는지 확인 하십시오.

Toohello 이동 **개요** hello 가상 네트워크의 페이지입니다. Hello 확인 **연결 된 장치** hello 응용 프로그램 게이트웨이에 대 한 합니다.

![Hello 연결 된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

응용 프로그램 게이트웨이 이면 hello 가상 네트워크를 삭제 하려면 먼저 제거 해야 합니다.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Azure Active Directory 도메인 서비스 hello 가상 네트워크에서 설정 되어 있는지 확인

Hello Active Directory 도메인 서비스는 활성화 되어 연결 된 toohello 가상 네트워크를이 가상 네트워크를 삭제할 수 없습니다. 

![Hello 연결 된 장치 확인](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable 서비스 hello, 다음이 단계를 수행 합니다.

1. Toohello 이동 [Azure 클래식 포털](https://manage.windowsazure.com)합니다.
2. Hello 왼쪽된 창에서 선택 **Active Directory**합니다.
3. Active Directory 도메인 서비스를 사용할 수 있는 hello Azure Active Directory (Azure AD) 디렉터리를 선택 합니다.
4. 선택 hello **구성** 탭 합니다.
5. 아래 **도메인 서비스**, hello 변경 **이 디렉터리에 대 한 도메인 서비스 사용** 옵션**아니요**합니다.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Hello 가상 네트워크에 연결 된 tooother 리소스 인지 확인

서킷 링크, 연결 및 가상 네트워크 피어링이 있는지 확인합니다. 이러한 가상 네트워크 삭제 toofail을 발생할 수 있습니다. 

hello 권장된 삭제 순서는 다음과 같습니다.

1. 게이트웨이 연결
2. 게이트웨이
3. IP
4. 가상 네트워크 피어링
5. ASE(App Service Environment)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Hello 가상 네트워크의 가상 컴퓨터가 여전히 실행 중인지 확인

어떤 가상 컴퓨터도 hello 가상 네트워크에 있는지 확인 합니다.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Hello 가상 네트워크 마이그레이션 걸려 있는지 여부를 확인 하십시오.

Hello 가상 네트워크 마이그레이션 상태에 걸려를 삭제할 수 없습니다. Hello tooabort hello 마이그레이션 명령을 실행 하 고 hello 가상 네트워크를 삭제 합니다.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>다음 단계

- [Azure Virtual Network](virtual-networks-overview.md)
- [Azure Virtual Network FAQ(질문과 대답)](virtual-networks-faq.md)