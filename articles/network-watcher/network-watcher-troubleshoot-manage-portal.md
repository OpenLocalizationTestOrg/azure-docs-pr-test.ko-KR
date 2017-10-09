---
title: "aaaTroubleshoot Azure 가상 네트워크 게이트웨이 및 연결-PowerShell | Microsoft Docs"
description: "이 페이지에서는 toouse hello Azure 네트워크 감시자 PowerShell cmdlet을 해결 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Azure Network Watcher PowerShell을 사용하여 Virtual Network 게이트웨이 및 연결 문제 해결

> [!div class="op_single_selector"]
> - [포털](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

네트워크 감시자 toounderstanding Azure의 네트워크 리소스 관련해 서 다양 한 기능을 제공 합니다. 이러한 기능 중 하나는 리소스 문제 해결입니다. 리소스 문제를 해결 하는 hello 포털, PowerShell, CLI 또는 REST API를 통해 호출할 수 있습니다. 호출 되 면 네트워크 감시자 가상 네트워크 게이트웨이 또는 연결의 hello 상태를 검사 하 고 해당 결과 반환 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다.

지원되는 게이트웨이 유형 목록을 보려면 [지원되는 게이트웨이 유형](network-watcher-troubleshoot-overview.md#supported-gateway-types)을 방문하세요.

## <a name="overview"></a>개요

Hello 기능을 제공 리소스 문제 해결 가상 네트워크 게이트웨이 및 연결 때 발생 하는 문제를 해결 합니다. 요청이 이루어지면 tooresource 문제 해결 로그 되는 쿼리 및 검사 합니다. 검사 완료 되 면 hello 결과가 반환 됩니다. 결과 여러 분 tooreturn를 수행할 수 있는 리소스 문제 해결 요청은 장기 실행 요청 합니다. 문제 해결에서 hello 로그에 지정 된 저장소 계정에 대 한 컨테이너에 저장 됩니다.

## <a name="troubleshoot-a-gateway-or-connection"></a>게이트웨이 또는 연결 문제 해결

1. Toohello 이동 [Azure 포털](https://portal.azure.com) 클릭 **네트워킹** > **네트워크 감시자** > **VPN 진단**
2. **구독**, **리소스 그룹** 및 **위치**를 선택합니다.
3. 문제 해결 리소스 hello 리소스의 hello 상태에 대 한 데이터를 반환합니다. 또한 toobe 검토 하는 관련 로그 tooa 저장소 계정을 저장 합니다. 클릭 **저장소 계정** tooselect 저장소 계정입니다.
4. Hello에 **저장소 계정은** 블레이드를 기존 저장소 계정을 선택 하거나 클릭 **저장소 계정 추가** toocreate 새 합니다.
5. Hello에 **컨테이너** 블레이드에서 기존 컨테이너를 선택 하거나 클릭 **+ 컨테이너** toocreate 새 컨테이너입니다. 완료되면 **저장**을 클릭합니다.
6. Hello 게이트웨이와 연결 리소스 tootroubleshoot를 선택 하 고 클릭 **문제 해결 시작**

여러 리소스를 선택한 경우 문제 해결은 게이트웨이 리소스에 동시에 실행됩니다. 연결에서 실행할 수 없습니다 및 hello에 게이트웨이에 연결 된 동시 합니다. Tootroubleshoot 게이트웨이 것이 좋습니다 먼저 긴 프로세스는 연결 문제 해결 합니다. VPN 진단 리소스 hello에서 실행 되는 동안 **상태 문제 해결** 열의 상태가 표시 됩니다 **실행**

완료 되 면 hello 상태 열 변경 내용 너무**정상** 또는 **Unhealthy**합니다.

![문제 해결 완료][2]

## <a name="understanding-hello-results"></a>Hello 결과 이해

Hello에 **세부 정보** 섹션 hello 창의 hello **상태** 탭에 표시 hello 마지막 문제 해결의 hello 상태 실행 hello 선택한 리소스에 있습니다. Hello 최신 진단 결과가 표시 된 xx 분 후에 hello 마지막으로 실행 합니다.

|속성  |설명  |
|---------|---------|
|리소스     | 링크 toohello 리소스입니다.        |
|저장소 경로     |  경로 toohello 저장소 계정 및 컨테이너 (모든 hello를 실행 하는 동안 생성 된) 경우 hello 로그를 포함 하는 합니다. Hello 포털을 나간 후에이 설정은 유지 되지 않습니다.        |
|요약     | 요약 hello 리소스 상태입니다.        |
|세부 정보     | Hello 리소스 상태에 대 한 자세한 정보입니다.        |
|마지막 실행     | 마지막 시간 hello hello 실행 된 시간 문제를 해결 합니다.        |


hello **동작** 탭 어떻게 tooresolve hello 문제에 일반적인 지침을 제공 합니다. Hello 문제에 대 한 작업을 수행할 수, 링크를 추가 하는 지침과 함께 제공 됩니다. Hello 경우에서 hello 응답을 자세한 지침은 없으며가 있는 hello url tooopen 지원 사례를 제공 합니다.  Hello 응답 및 포함 된 항목의 hello 속성에 대 한 자세한 내용은 방문 [네트워크 감시자 문제 해결 개요](network-watcher-troubleshoot-overview.md)


## <a name="next-steps"></a>다음 단계

해당 중지 VPN 연결 설정이 변경 되었으며, 참조 [네트워크 보안 그룹 관리](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack 아래로 hello 네트워크 보안 그룹 및 보안 규칙을 문제가 될 수 있습니다.


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
