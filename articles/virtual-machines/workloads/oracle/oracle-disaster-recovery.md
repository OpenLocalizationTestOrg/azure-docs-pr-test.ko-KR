---
title: "Azure 환경에서 Oracle 재해 복구 시나리오의 aaaOverview | Microsoft Docs"
description: "Azure 환경의 Oracle Database 12c 데이터베이스에 대한 재해 복구 시나리오입니다."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 6/2/2017
ms.author: rclaus
ms.openlocfilehash: 1fa69e1ba044b46b27695fec92fd9ca82df796f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-for-an-oracle-database-12c-database-in-an-azure-environment"></a>Azure 환경의 Oracle Database 12c 데이터베이스 재해 복구

## <a name="assumptions"></a>가정

- Oracle Data Guard 설계 및 Azure 환경에 대해 이해하고 있습니다.


## <a name="goals"></a>목표
- 디자인 hello 토폴로지 및 재해 복구 (DR) 요구 사항에 맞게 구성 합니다.

## <a name="scenario-1-primary-and-dr-sites-on-azure"></a>시나리오 1: 기본 사이트 및 DR 사이트가 Azure에 있음

고객에 게는 Oracle 데이터베이스 설정 hello 기본 사이트에 있습니다. DR 사이트는 다른 지역에 있습니다. hello 고객 Oracle Data Guard를 사용 하 여 이러한 사이트 간의 빠른 복구. hello 기본 사이트에는 역시 보고에 대 한 보조 데이터베이스 및 다른 용도로 사용 합니다. 

### <a name="topology"></a>토폴로지

다음은 hello Azure 설치에 대 한 요약이입니다.

- 두 사이트(기본 사이트 및 DR 사이트)
- 두 가상 네트워크
- Data Guard가 있는 두 Oracle 데이터베이스(주 및 대기)
- Golden Gate 또는 Data Guard가 있는 두 Oracle 데이터베이스(기본 사이트에만 해당)
- 두 개의 응용 프로그램 서비스, 기본 및 hello DR 사이트에
- *가용성 집합* hello 기본 사이트에서 데이터베이스 및 응용 프로그램 서비스에 사용 되는
- 하나의 jumpbox toohello 개인 네트워크 액세스를 제한 하 고 관리자가 한 로그인만 허용 하는 각 사이트에
- 별도의 서브넷에 있는 Jumpbox, 응용 프로그램 서비스, 데이터베이스 및 VPN 게이트웨이
- 응용 프로그램 및 데이터베이스 서브넷에 적용되는 NSG

![Hello DR 토폴로지에 페이지의 스크린샷](./media/oracle-disaster-recovery/oracle_topology_01.png)

## <a name="scenario-2-primary-site-on-premises-and-dr-site-on-azure"></a>시나리오 2: 기본 사이트는 온-프레미스에 있고, DR 사이트는 Azure에 있음

고객이 온-프레미스에 Oracle 데이터베이스를 설치했습니다(기본 사이트). DR 사이트는 Azure에 있습니다. Oracle Data Guard는 이러한 사이트 간의 빠른 복구에 사용됩니다. hello 기본 사이트에는 역시 보고에 대 한 보조 데이터베이스 및 다른 용도로 사용 합니다. 

이 설치에 대한 접근 방법은 두 가지가 있습니다.

### <a name="approach-1-direct-connections-between-on-premises-and-azure-requiring-open-tcp-ports-on-hello-firewall"></a>온-프레미스와 Azure hello 방화벽에서 열려 있는 TCP 포트 요구 간 접근 방식 1: 직접 연결 

외부 세계 hello TCP 포트 toohello 노출 하기 때문에 직접 연결 사용 합니다.

#### <a name="topology"></a>토폴로지

다음은 hello Azure 설치에 대 한 요약입니다.

- 하나의 DR 사이트 
- 가상 네트워크 1개
- Data Guard가 있는 하나의 Oracle 데이터베이스(활성)
- Hello DR 사이트에서 하나의 응용 프로그램 서비스
- Toohello 개인 네트워크 액세스를 제한 하 고 관리자가 한 로그인만 허용 하는 하나의 jumpbox
- 별도의 서브넷에 있는 Jumpbox, 응용 프로그램 서비스, 데이터베이스 및 VPN 게이트웨이
- 응용 프로그램 및 데이터베이스 서브넷에 적용되는 NSG
- NSG 정책/규칙 tooallow 인바운드 TCP 포트 1521 (또는 사용자 지정 포트)
- NSG 정책/규칙 toorestrict 유일한 hello IP 주소/온-프레미스 (DB 또는 응용 프로그램) tooaccess hello에 대 한 가상 네트워크 주소

![Hello DR 토폴로지에 페이지의 스크린샷](./media/oracle-disaster-recovery/oracle_topology_02.png)

### <a name="approach-2-site-to-site-vpn"></a>방법 2: 사이트 간 VPN
사이트 간 VPN이 더 나은 방법입니다. VPN 설정에 대한 자세한 내용은 [CLI를 사용하여 사이트 간 VPN 연결로 가상 네트워크 만들기](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)를 참조하세요.

#### <a name="topology"></a>토폴로지

다음은 hello Azure 설치에 대 한 요약입니다.

- 하나의 DR 사이트 
- 가상 네트워크 1개 
- Data Guard가 있는 하나의 Oracle 데이터베이스(활성)
- Hello DR 사이트에서 하나의 응용 프로그램 서비스
- Toohello 개인 네트워크 액세스를 제한 하 고 관리자가 한 로그인만 허용 하는 하나의 jumpbox
- 별도의 서브넷에 있는 Jumpbox, 응용 프로그램 서비스, 데이터베이스 및 VPN 게이트웨이
- 응용 프로그램 및 데이터베이스 서브넷에 적용되는 NSG
- 온-프레미스와 Azure 간의 사이트 간 VPN 연결

![Hello DR 토폴로지에 페이지의 스크린샷](./media/oracle-disaster-recovery/oracle_topology_03.png)

## <a name="additional-reading"></a>추가 참조 자료

- [Azure에서 Oracle 데이터베이스 설계 및 구현](oracle-design.md)
- [Oracle Data Guard 구성](configure-oracle-dataguard.md)
- [Oracle Golden Gate 구성](configure-oracle-golden-gate.md)
- [Oracle 백업 및 복구](oracle-backup-recovery.md)


## <a name="next-steps"></a>다음 단계

- [자습서: 고가용성 VM 만들기](../../linux/create-cli-complete.md)
- [VM 배포 Azure CLI 샘플 탐색](../../linux/cli-samples.md)
