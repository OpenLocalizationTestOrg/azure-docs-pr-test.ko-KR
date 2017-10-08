---
title: "Azure 네트워크 감시자 다음 홉-Azure 포털 aaaFind 다음 홉 | Microsoft Docs"
description: "이 문서에서는 설명 방법을 어떤 hello 다음 홉 형식 및 ip 주소를 사용 하 여 다음 홉을 사용 하 여 hello Azure 포털을 찾을 수 있습니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a>어떤 hello 다음 홉 형식이 hello 다음 홉 기능을 사용 하 여 Azure 네트워크 감시자 hello 포털을 사용 하는 확인

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

다음 홉 hello 기능을 제공 하는 네트워크 감시자의 기능을 가져오고 hello 다음 홉 형식이 지정 된 가상 컴퓨터를 기반으로 하는 IP 주소입니다. 이 기능은 가상 컴퓨터를 종료 하는 트래픽이 게이트웨이, 인터넷 또는 가상 네트워크 tooget tooits 대상에서 이동 하는 경우를 결정 하는 데 유용 합니다.

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자를 만들](network-watcher-create.md) toocreate 네트워크 감시자 합니다. hello 시나리오는 또한 적합 한 가상 컴퓨터가 리소스 그룹 사용 toobe 있다고 가정 합니다.

## <a name="scenario"></a>시나리오

이 문서에서 설명 하는 hello 시나리오는 리소스에 대 한 다음 홉 toofind hello 다음 홉 형식이 및 IP 주소를 사용 합니다. 다음 홉에 대 한 자세한 toolearn 방문 [다음 홉 개요](network-watcher-next-hop-overview.md)합니다.

이 시나리오에서는 다음을 수행합니다.

* 가상 컴퓨터에서 다음 홉 hello를 검색 합니다.

## <a name="get-next-hop"></a>다음 홉 가져오기

### <a name="step-1"></a>1단계

Hello Azure 포털에서에서 tooyour 네트워크 감시자 리소스를 이동 합니다.

### <a name="step-2"></a>2단계

클릭 **다음 홉** hello 원본 및 대상 IP hello 탐색 창, 선택 hello 가상 컴퓨터 및 네트워크 인터페이스를 작성 하 고 hello 클릭 **다음 홉** 단추입니다.

> [!NOTE]
> 다음 홉 VM 리소스 hello toorun가 할당 되는 필요 합니다.

![다음 홉 가져오기 개요][1]

### <a name="step-3"></a>3단계

Hello 작업 완료 되 면 hello 결과가 제공 됩니다. IP 주소와 장치 hello 다음 홉 유형을 hello가 표시 됩니다. hello 다음 표에 hello 사용할 수 있는 반환된 값 hello 포털에 있습니다.

**다음 홉 유형**

* 인터넷
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* 없음

사용자 지정 경로 사용 하는 tooroute hello 결과 함께이 트래픽은 hello 사용자 정의 경로 (UDR)도 표시 됩니다.

![다음 홉 결과 가져오기][2]

## <a name="next-steps"></a>다음 단계

자세한 내용은 방법 tooreview 방문 하 여 프로그래밍 방식으로 네트워크 보안 그룹 설정을 [NSG 감사 네트워크 감시자를](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














