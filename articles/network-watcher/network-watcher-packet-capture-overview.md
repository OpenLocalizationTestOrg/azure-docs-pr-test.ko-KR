---
title: "Azure 네트워크 감시자에서 aaaIntroduction tooPacket 캡처 | Microsoft Docs"
description: "이 페이지 hello 네트워크 감시자 패킷 캡처 기능에 대 한 개요를 제공합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Azure 네트워크 감시자에서 소개 toovariable 패킷 캡처

네트워크 감시자 변수 패킷 캡처 toocreate 패킷 캡처 세션 tootrack 트래픽 tooand를 가상 컴퓨터를 수 있습니다. 패킷 캡처 프로비저닝하지 toodiagnose 네트워크 비정상 모두 사용 하면 proactivity 및 합니다. 통신 및 더 많은 네트워크 침입, toodebug 클라이언트-서버에 대 한 정보를 확보 하는 네트워크 통계를 수집 하는 것이 다른 사용 됩니다.

패킷 캡처는 Network Watcher를 통해 원격으로 시작되는 가상 컴퓨터 확장입니다. 이 기능은 중요 한 시간을 절약할 hello 필요한 가상 컴퓨터에서 패킷 캡처를 수동으로 실행의 hello 부담을 줄일 수 있습니다. Hello 포털, PowerShell, CLI 또는 REST API를 통해 패킷 캡처를 트리거할 수 있습니다. 패킷 캡처를 트리거하는 방식에 대한 한 가지 예는 Virtual Machine 경고를 사용하는 것입니다. 필터는 hello 캡처 세션 tooensure toomonitor 원하는 트래픽을 관한 제공. 필터는 5개 튜플(프로토콜, 로컬 IP 주소, 원격 IP 주소, 로컬 포트 및 원격 포트) 정보를 기반으로 합니다. hello 캡처된 데이터는 hello 로컬 디스크 또는 저장소 blob에 저장 됩니다. 구독당 하위 지역별로 패킷 캡처 세션 수가 10개로 제한됩니다. 이 한도 toohello 세션만 적용 하 고 hello VM에서 로컬로 또는 저장소 계정에서 패킷 캡처 파일을 저장 하는 toohello 적용 되지 않습니다.

> [!IMPORTANT]
> 패킷 캡처에는 가상 컴퓨터 확장 `AzureNetworkWatcherExtension`이 필요합니다. Windows VM에서 hello 확장을 설치 하는 것에 대 한 방문 [Windows에 대 한 네트워크 감시자 에이전트가 Azure 가상 컴퓨터 확장](../virtual-machines/windows/extensions-nwa.md) 및 방문을 Linux VM에 대 한 [Linux용Azure네트워크감시자에이전트가가상컴퓨터확장](../virtual-machines/linux/extensions-nwa.md).

다음 옵션 hello 패킷 캡처 세션에 사용할 수 있는 원하는 tooonly hello 정보를 캡처하는 tooreduce hello 정보:

**캡처 구성**

|속성|설명|
|---|---|
|**패킷당 최대 바이트(bytes)** | 번호 hello 바이트를 모두 비워 두면 캡처되는 각 패킷의 바이트 캡처합니다. 번호 hello 바이트를 모두 비워 두면 캡처되는 각 패킷의 바이트 캡처합니다. 유일한 hello IPv4 헤더 – 필요한 경우 여기 34를 나타냅니다. |
|**세션당 최대 바이트(bytes)** | Hello 값 hello 세션 끝에 도달 하는 바이트의 총이 캡처됩니다.|
|**시간 제한(초)** | 집합 hello 패킷에 대 한 시간 제약 세션을 캡처합니다. hello 기본값은 18000 초 또는 5 시간입니다.|

**필터링(선택 사항)**

|속성|설명|
|---|---|
|**프로토콜** | hello 패킷에 대 한 프로토콜 toofilter hello를 캡처합니다. hello 사용 가능한 값에는 TCP, UDP 및 모든은 합니다.|
|**로컬 IP 주소** | 이 값이 필터 값 hello 로컬 IP 주소와 일치 하는 hello 패킷 캡처 toopackets를 필터링 합니다.|
|**로컬 포트** | 이 값 필터 hello 패킷 캡처 toopackets hello 로컬 포트가이 필터 값과 일치 합니다.|
|**원격 IP 주소** | 이 값 필터 hello 패킷 캡처 toopackets hello 원격 IP가이 필터 값과 일치 합니다.|
|**원격 포트** | 이 값 필터 hello 패킷 캡처 toopackets hello 원격 포트가이 필터 값과 일치 합니다.|

### <a name="next-steps"></a>다음 단계

방문 하 여 hello 포털을 통해 패킷 캡처를 관리 하는 방법에 대해 알아봅니다 [hello Azure 포털에에서 대 한 패킷 캡처를 관리](network-watcher-packet-capture-manage-portal.md) 또는 방문 하 여 PowerShell [PowerShell과 함께 패킷 캡처를 관리](network-watcher-packet-capture-manage-powershell.md)합니다.

방문 하 여 가상 컴퓨터 경고를 기반으로 toocreate 사전 패킷 캡처 방법을 알아보려면 [경고 트리거된 패킷 캡처를 만들려면](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













