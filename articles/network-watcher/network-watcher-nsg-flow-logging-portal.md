---
title: "Azure 네트워크 감시자를 사용 하 여 aaaManage 네트워크 보안 그룹 흐름 로그 | Microsoft Docs"
description: "이 페이지에서는 toomanage 네트워크 보안 그룹 흐름 Azure 네트워크 감시자 로그인 하는 방법을 설명 합니다."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Hello Azure 포털에서에서 네트워크 보안 그룹 흐름 로그 관리

> [!div class="op_single_selector"]
> - [Azure 포털](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

네트워크 보안 그룹 흐름 로그는 네트워크 보안 그룹을 통해 IP 트래픽 ingress 및 egress에 대 한 tooview 정보를 사용 하면 네트워크 감시자의 기능입니다. 이러한 흐름 로그는 JSON 형식으로 작성되며 다음과 같은 중요한 정보를 제공합니다. 

- 규칙 단위 기반의 아웃바운드 및 인바운드 흐름
- hello 흐름 hello NIC에 적용 됩니다.
- hello 흐름 (소스/대상 IP, 소스/대상 포트, 프로토콜)에 대 한 정보를 5-튜플입니다.
- 트래픽에 대한 허용 또는 거부 여부 정보

## <a name="before-you-begin"></a>시작하기 전에

이 시나리오에서는 hello 단계에 따라 이미 가정 [네트워크 감시자 인스턴스를 만들고](network-watcher-create.md)합니다. hello 시나리오도 있다고 가정 합니다는 적합 한 가상 컴퓨터가 리소스 그룹입니다.

## <a name="register-insights-provider"></a>Insights 공급자 등록

흐름에 대 한 로깅 toowork 성공적으로 hello **Microsoft.Insights** 공급자를 등록 해야 합니다. 단계를 수행 하는 내용이 hello tooregister hello 공급자: 

1. 너무 이동**구독**, 한 다음 tooenable 흐름 로그 원하는 hello 구독을 선택 합니다. 
2. Hello에 **구독** 블레이드를 **리소스 공급자**합니다. 
3. 공급자의 hello 목록을 확인 하 고 해당 hello 확인 **microsoft.insights** 공급자가 등록 되어 있습니다. 그렇지 않으면 **등록**을 선택합니다.

![공급자 보기][providers]

## <a name="enable-flow-logs"></a>흐름 로그를 사용하도록 설정

다음이 단계 흐름 로그를 네트워크 보안 그룹을 사용 하도록 설정 hello 프로세스를 안내 합니다.

### <a name="step-1"></a>1단계

Tooa 네트워크 감시자 인스턴스를 이동 하 고 다음 선택 **기록 NSG 흐름**합니다.

![흐름 로그 개요][1]

### <a name="step-2"></a>2단계

Hello 목록에서 네트워크 보안 그룹을 선택 합니다.

![흐름 로그 개요][2]

### <a name="step-3"></a>3단계 

Hello에 **흐름 로그 설정을** 블레이드에서 너무 hello 상태 설정**에**, 고 저장소 계정을 구성 합니다.  완료되면 **확인**을 선택합니다. 그런 다음 **저장**을 선택합니다.

![흐름 로그 개요][3]

## <a name="download-flow-logs"></a>흐름 로그 다운로드

흐름 로그는 저장소 계정에 저장됩니다. 흐름 로그 tooview 다운로드 하 합니다.

### <a name="step-1"></a>1단계

toodownload 흐름 로그 선택 **구성 된 저장소 계정에서 흐름 로그를 다운로드할 수**합니다. 이 단계에서는 있습니다 tooa 저장소 계정 보기는 로그 toodownload를 선택할 수 있습니다.

![흐름 로그 설정][4]

### <a name="step-2"></a>2단계

Toohello 올바른 저장소 계정 이동 합니다. 그런 다음 **컨테이너** > **insights-log-networksecuritygroupflowevent**를 선택합니다.

![흐름 로그 설정][5]

### <a name="step-3"></a>3단계

Hello 흐름 로그의 toohello 위치,를 선택한 다음 선택 **다운로드**합니다.

![흐름 로그 설정][6]

Hello 로그의 hello 구조에 대 한 내용은 방문 [네트워크 보안 그룹 흐름 로그 개요](network-watcher-nsg-flow-logging-overview.md)합니다.

## <a name="next-steps"></a>다음 단계

너무 방법에 대해 알아봅니다[PowerBI 사용 하 여 프로그램 NSG 흐름 로그 시각화](network-watcher-visualize-nsg-flow-logs-power-bi.md)합니다.

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
