---
title: "aaaManage 패킷 캡처를 Azure 네트워크 감시자-Azure 포털 | Microsoft Docs"
description: "이 페이지에서는 방법을 toomanage hello Azure 포털을 사용 하 여 네트워크 감시자의 패킷 캡처 기능을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Hello 포털을 사용 하 여 Azure 네트워크 감시자를 사용 하 여 패킷 캡처를 관리

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API](network-watcher-packet-capture-manage-rest.md)

네트워크 감시자 패킷 캡처 toocreate 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다. 필터는 원하는 hello 트래픽만 캡처 hello 캡처 세션 tooensure 위해 제공 됩니다. 패킷 캡처 프로비저닝하지 및 사전 toodiagnose 네트워크 예외 수 있습니다. 통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다. 이 기능은 수 tooremotely 트리거 패킷 캡처 됨으로써 수동으로 및 시간을 단축할 수 있는 hello 원하는 컴퓨터에 패킷 캡처를 실행 해야 하는 hello 부담 래핑할 수 있습니다.

이 문서에서는 하 hello 패킷 캡처를 위해 현재 사용할 수 있는 다른 관리 작업 합니다.

- [**패킷 캡처 시작**](#start-a-packet-capture)
- [**패킷 캡처 중지**](#stop-a-packet-capture)
- [**패킷 캡처 삭제**](#delete-a-packet-capture)
- [**패킷 캡처 다운로드**](#download-a-packet-capture)

## <a name="before-you-begin"></a>시작하기 전에

이 문서의 다음 리소스는 hello 있다고 가정 합니다.

- 인스턴스 hello 지역에 대 한 네트워크 감시자의 원하는 toocreate 패킷 캡처
- Hello 패킷 사용 하 여 가상 컴퓨터 캡처 확장을 사용 합니다.

> [!IMPORTANT]
> 패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다. Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Hello 포털을 통해 패킷 캡처 agent 확장

tooinstall hello 패킷 캡처 hello 포털을 통해 VM 에이전트 tooyour 가상 컴퓨터를 탐색, 클릭 **확장** > **추가** 검색 한 **에 대 한 네트워크 감시자 에이전트 Windows**

![에이전트 보기][agent]

## <a name="packet-capture-overview"></a>패킷 캡처 개요

Toohello 이동 [Azure 포털](https://portal.azure.com) 클릭 **네트워킹** > **네트워크 감시자** > **패킷 캡처**

hello 개요 페이지 hello 상태에 관계 없이 존재 하는 모든 패킷 목록이 캡처합니다 표시 됩니다.

> [!NOTE]
> 패킷 캡처 포트 443 통해 연결 toohello 저장소 계정이 필요합니다.

![패킷 캡처 개요 화면][1]

## <a name="start-a-packet-capture"></a>패킷 캡처 시작

클릭 **추가** toocreate 패킷 캡처.

패킷 캡처에 정의할 수 있는 hello 속성은 같습니다.

**기본 설정**

- **구독** -이 값은 사용 되는 hello 구독, 각 구독에서 네트워크 감시자 인스턴스가 필요 합니다.
- **리소스 그룹** -대상이 되는 hello 가상 컴퓨터의 hello 리소스 그룹입니다.
- **가상 컴퓨터를 대상** -hello 패킷 캡처를 실행 하는 hello 가상 컴퓨터
- **패킷 캡처 name** -이 값은 hello 패킷 캡처의 hello 이름입니다.

**캡처 구성**

- **저장소 계정** - 패킷 캡처를 저장소 계정에 저장할지 여부를 결정합니다.
- **파일** -패킷 캡처 hello 가상 컴퓨터에 로컬로 저장 하는 경우를 결정 합니다.
- **저장소 계정** -hello에 저장소 계정 toosave hello 패킷 캡처를 선택 합니다. 기본 위치는 https://{저장소 계정 이름}.blob.core.windows.net/network-watcher-logs/subscriptions/{구독 ID}/resourcegroups/{리소스 그룹 이름}/providers/microsoft.compute/virtualmachines/{가상 컴퓨터 이름}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap입니다. (**저장소**를 선택한 경우에만 사용됨)
- **로컬 파일 경로** -가상 컴퓨터 toosave hello 패킷 캡처 hello 로컬 경로입니다. (**파일**을 선택한 경우에만 사용됨). 유효한 경로를 제공해야 합니다.
- **패킷 당 최대 바이트** -수 hello 바이트를 모두 비워 두면 캡처되는 각 패킷의 바이트 캡처합니다.
- **세션 마다 최대 바이트** -총의 hello 값 hello 패킷 캡처 중지에 도달 하면 캡처되는 바이트 수입니다.
- **제한 시간 (초)** -패킷 캡처 toostop hello에 대 한 시간 제한 값을 설정 합니다. 기본값은 18000초입니다.

> [!NOTE]
> Premium Storage 계정에서는 패킷 캡처 저장이 현재 지원되지 않습니다.

**필터링(선택 사항)**

- **프로토콜** -hello 패킷 캡처에 대 한 프로토콜 toofilter hello 합니다. hello 사용 가능한 값에는 TCP, UDP 및은 합니다.
- **로컬 IP 주소** -이 값이 필터 값 hello 로컬 IP 주소와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.
- **로컬 포트** -이 값이 필터 값 hello 로컬 포트와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.
- **원격 IP 주소** -이 값이 필터 값 hello 원격 IP와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.
- **원격 포트** -이 값이 필터 값 hello 원격 포트와 일치 하는 hello 패킷 캡처 toopackets 필터링 합니다.

> [!NOTE]
> 포트 및 IP 주소 값은 단일 값이거나 값 범위이거나 집합일 수 있습니다. (즉, 포트의 경우 80-1024) 원하는 만큼 많은 필터를 정의할 수 있습니다.

Hello 값 입력 된 후 클릭 **확인** toocreate hello 패킷 캡처.

![패킷 캡처 만들기][2]

Hello 시간 제한에 설정 hello 패킷 캡처 만료, hello 패킷 캡처 중지 되 고 검토할 수 있습니다. 수동으로 hello 패킷 캡처 세션을 중지할 수 있습니다.

## <a name="delete-a-packet-capture"></a>패킷 캡처 삭제

Hello 패킷에 보기를 캡처, hello 클릭 **상황에 맞는 메뉴** (...) 또는 마우스 오른쪽 단추로 클릭 하 고 클릭 **삭제** toostop hello 패킷 캡처

![패킷 캡처 삭제][3]

> [!NOTE]
> 패킷 캡처를 삭제 하는 경우에 hello 파일 hello 저장소 계정에서 삭제 되지 않습니다.

요청 toodelete hello 패킷 캡처를 원하는 tooconfirm 클릭 **예**

![확인][4]

## <a name="stop-a-packet-capture"></a>패킷 캡처 중지

Hello 패킷에 보기를 캡처, hello 클릭 **상황에 맞는 메뉴** (...) 또는 마우스 오른쪽 단추로 클릭 하 고 클릭 **중지** toostop hello 패킷 캡처

## <a name="download-a-packet-capture"></a>패킷 캡처 다운로드

패킷 캡처 세션이 완료 되 면 hello 캡처 파일은 업로드 tooblob 저장소나 tooa 로컬 파일 hello VM에서. hello 패킷 캡처의 hello 저장소 위치는 hello 세션의 작성 시 정의 됩니다. 저장 된 tooa 저장소 계정이 여기에서 다운로드할 수 있는 Microsoft Azure 저장소 탐색기는 파일을 캡처하기 이러한 편리한 도구 tooaccess: http://storageexplorer.com/

저장소 계정이 지정 되어 있으면 hello 수정할 수 있는 위치에서 저장소 계정은 tooa 패킷 캡처 파일에 저장 됩니다.
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>다음 단계

어떻게 tooautomate 패킷 캡처를 가상 컴퓨터 경고 보기에 대해 알아봅니다 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)

[IP 흐름 확인 확인](network-watcher-check-ip-flow-verify-portal.md)을 방문하여 특정 트래픽이 VM에서 허용되는지 알아봅니다.

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













