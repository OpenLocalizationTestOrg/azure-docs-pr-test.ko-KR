---
title: "PowerShell 샘플 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 샘플"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a>네트워킹에 대한 Azure PowerShell 샘플

hello 다음 표에서 링크 tooscripts Azure PowerShell을 사용 하 여 작성 합니다.

| | |
|-|-|
|**Azure 리소스 간 연결**||
| [다중 계층 응용 프로그램을 위한 가상 네트워크 만들기](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다. 트래픽 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP, 트래픽 toohello 동안 백 엔드 서브넷은 제한 된 tooSQL, 포트 1433입니다. |
| [2개 가상 네트워크 피어링](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | 만들고 hello에 두 개의 가상 네트워크를 연결 합니다. 동일한 지역입니다. |
| [네트워크 가상 어플라이언스를 통한 트래픽 라우팅](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | 프런트 엔드 및 백 엔드 서브넷 및 hello 두 서브넷 간의 트래픽 tooroute 수 있는 VM 가상 네트워크를 만듭니다. |
| [인바운드 및 아웃바운드 VM 네트워크 트래픽 필터링](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | 프런트 엔드 및 백 엔드 서브넷이 있는 가상 네트워크를 만듭니다. 인바운드 네트워크 트래픽을 toohello 프런트 엔드 서브넷은 제한 된 tooHTTP 및 HTTPS입니다. 아웃 바운드 트래픽을 toohello 인터넷 hello 백 엔드 서브넷에서 허용 되지 않습니다. |
|**부하 분산 및 트래픽 방향**||
| [고가용성을 위한 분산 트래픽 tooVMs 로드](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | 고가용성의 부하가 분산된 구성으로 여러 가상 컴퓨터를 만듭니다. |
| [VM에서 여러 웹 사이트에 부하 분산](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | 조인 된 tooan Azure 가용성 집합을 통해 Azure 부하 분산 장치는 액세스할 수 있는 여러 IP 구성을 사용 하 여 두 개의 Vm을 만듭니다. |
| [높은 응용 프로그램 가용성을 위해 여러 지역 간에 트래픽 전송](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  두 개의 App Service 계획, 두 개의 웹앱, Traffic Manager 프로필 및 두 개의 Traffic Manager 끝점을 만듭니다. |
| | |
