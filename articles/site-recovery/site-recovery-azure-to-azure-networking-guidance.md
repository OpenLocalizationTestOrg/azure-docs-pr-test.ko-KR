---
title: "사이트 복구 tooAzure Azure에서 가상 컴퓨터 복제를 위한 네트워킹 지침 aaaAzure | Microsoft Docs"
description: "Azure Virtual Machines 복제에 대한 네트워킹 지침"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Azure Virtual Machines 복제에 대한 네트워킹 지침

>[!NOTE]
> Azure Virtual Machines에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.

복제 하 고 하나의 영역 tooanother 지역에서 Azure 가상 컴퓨터를 복구 하는 경우 Azure Site Recovery에 대 한 네트워킹 지침을 hello 하는이 문서에 자세히 설명 합니다. Azure 사이트 복구 요구 사항에 대 한 자세한 참조 hello [필수 구성 요소](site-recovery-prereq.md) 문서.

## <a name="site-recovery-architecture"></a>Site Recovery 아키텍처

사이트 복구는 쉽고 간단한 방법이 tooreplicate에서 실행 중인 Azure 가상 컴퓨터 tooanother Azure 지역 hello 기본 지역에서 중단 한 경우 복구할 수 있도록 하는 응용 프로그램을 제공 합니다. [이 시나리오와 Site Recovery 아키텍처](site-recovery-azure-to-azure-architecture.md)에 대해 자세히 알아보세요.

## <a name="your-network-infrastructure"></a>네트워크 인프라

hello 다음 다이어그램은 Azure 가상 컴퓨터에서 실행 중인 응용 프로그램에 대 한 일반적인 Azure 환경 hello:

![고객 환경](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Azure express 경로 또는 온-프레미스 네트워크 tooAzure에서 VPN 연결을 사용 하는 경우 hello 환경은 다음과 같습니다.

![고객 환경](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

일반적으로 고객은 방화벽 및/또는 NSG(네트워크 보안 그룹)를 사용하여 네트워크를 보호합니다. hello 방화벽 네트워크 연결을 제어 하기 위한 URL 기반 또는 IP 기반 허용 목록을 사용할 수 있습니다. Nsg IP 범위 toocontrol 네트워크 연결을 사용 하 여 규칙을 허용 합니다.

>[!IMPORTANT]
> 인증 된 프록시 toocontrol 네트워크 연결을 사용 하는 경우 지원 되지 않습니다 및 사이트 복구 복제를 사용할 수 없습니다. 

hello 다음 섹션에서는 설명 하는 사이트 복구 복제 toowork에 대 한 Azure 가상 컴퓨터에서 필요한 hello 네트워크 아웃 바운드 연결 변경 합니다.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Azure Site Recovery URL에 대한 아웃바운드 연결

모든 방화벽 URL 기반 프록시 toocontrol 아웃 바운드 연결을 사용할 수 있는지 toowhitelist 다음의 필수 Azure Site Recovery 서비스 Url:


**URL** | **목적**  
--- | ---
*.blob.core.windows.net | 데이터 수 쓸 수 있도록 toohello 캐시 저장소 계정 hello 소스 영역에 hello VM에서에서 필요 합니다.
login.microsoftonline.com | 권한 부여 및 인증 toohello Site Recovery 서비스 Url에 필요합니다.
*.hypervrecoverymanager.windowsazure.com | Hello Site Recovery 서비스 통신 hello VM에서에서 실행 될 수 있도록 해야 합니다.
*.servicebus.windows.net | Hello VM에서에서 hello 사이트 복구 모니터링 및 진단 데이터를 쓸 수 있도록 해야 합니다.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Azure Site Recovery IP 범위에 대한 아웃바운드 연결

>[!NOTE]
> tooautomatically hello 네트워크 보안 그룹에 필요한 hello NSG 규칙을 만들 수 있습니다, [다운로드 하 여이 스크립트를 사용 하 여](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702)합니다.

>[!IMPORTANT]
> * 테스트 네트워크 보안 그룹에서 필요한 hello NSG 규칙을 만들고 프로덕션 네트워크 보안 그룹에서 hello 규칙을 만들기 전에 문제 없이 되었는지 확인 하는 것이 좋습니다.
> * NSG 규칙 toocreate 필요한 hello 수 가입이 허용 목록 인지 확인 합니다. 고객 지원으로 문의 tooincrease hello NSG 규칙 제한 구독에서입니다.

모든 IP 기반 방화벽 프록시 또는 NSG 규칙 toocontrol 아웃 바운드 연결을 사용 하는 경우 hello 다음 IP 범위 필요 hello 가상 컴퓨터의 hello 원본 및 대상 위치에 따라 toobe 허용 목록.

- Toohello 원본 위치에 해당 하는 모든 IP 범위입니다. (Hello를 다운로드할 수 있습니다 [IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653).) 데이터가 VM hello에서 toohello 캐시 저장소 계정 기록 될 수 있도록 허용 목록이 필요 합니다.

- TooOffice 365 해당 하는 모든 IP 범위 [인증 및 id IP V4 끝점](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)합니다.

    >[!NOTE]
    > Hello 앞에 새 Ip tooOffice 365 IP 범위 추가 하는 경우 새 NSG 규칙 toocreate 해야 합니다.
    
- 대상 위치에 따라 다른 Site Recovery 서비스 끝점 IP([XML 파일로 제공](https://aka.ms/site-recovery-public-ips)) 

   **대상 위치** | **Site Recovery 서비스 IP** |  **Site Recovery 모니터링 IP**
   --- | --- | ---
   동아시아 | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   동남아시아 | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   인도 중부 | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   인도 남부 | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   미국 중북부 | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   북유럽 | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   서유럽 | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   미국 동부 | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   미국 서부 | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   미국 중남부 | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   미국 중부 | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   미국 동부 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   일본 동부 | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   일본 서부 | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   브라질 남부 | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   오스트레일리아 동부 | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   오스트레일리아 남동부 | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   캐나다 중부 | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   캐나다 동부 | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   미국 중서부 | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   미국 서부 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   영국 서부 | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   영국 남부 | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>샘플 NSG 구성
이 섹션에서는 사이트 복구 복제 가상 컴퓨터에서 작동할 수 있도록 hello 단계 tooconfigure NSG 규칙을 설명 합니다. NSG 규칙 toocontrol 아웃 바운드 연결을 사용 하는 경우 "허용 HTTPS 아웃 바운드" 규칙을 사용 하 여 모든 필요한 hello IP 범위에 대 한 합니다.

>[!Note]
> tooautomatically hello 네트워크 보안 그룹에 필요한 hello NSG 규칙을 만들 수 있습니다, [다운로드 하 여이 스크립트를 사용 하 여](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702)합니다.

예를 들어 VM의 소스 위치가 "미국 동부" 하는 경우 복제 대상 위치는 "Central US" hello 다음 두 섹션에서 hello 단계를 수행 합니다.

>[!IMPORTANT]
> * 테스트 네트워크 보안 그룹에서 필요한 hello NSG 규칙을 만들고 프로덕션 네트워크 보안 그룹에서 hello 규칙을 만들기 전에 문제 없이 되었는지 확인 하는 것이 좋습니다.
> * NSG 규칙 toocreate 필요한 hello 수 가입이 허용 목록 인지 확인 합니다. 고객 지원으로 문의 tooincrease hello NSG 규칙 제한 구독에서입니다. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>미국 동부 네트워크 보안 그룹을 hello에 NSG 규칙

* 너무 해당 하는 규칙을 만들[동부 미국 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653)합니다. 데이터가 VM hello에서 toohello 캐시 저장소 계정 기록 될 수 있도록 이것이 필요 합니다.

* TooOffice 365 해당 하는 모든 IP 범위에 대 한 규칙을 만들 [인증 및 id IP V4 끝점](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)합니다.

* Toohello 대상 위치에 해당 하는 규칙을 만듭니다.

   **위치**: | **Site Recovery 서비스 IP** |  **Site Recovery 모니터링 IP**
    --- | --- | ---
   미국 중부 | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Hello 중미 네트워크 보안 그룹에 NSG 규칙

Hello 대상 지역 toohello 소스 지역 장애 조치 후에서에서 복제를 사용할 수 있도록 이러한 규칙 요소가 필요 합니다.

* 너무 해당 하는 규칙[중앙 미국 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653)합니다. 이 데이터가 hello VM에서에서 toohello 캐시 저장소 계정 기록 될 수 있도록 필요 합니다.

* TooOffice 365 해당 하는 모든 IP 범위에 대 한 규칙 [인증 및 id IP V4 끝점](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)합니다.

* Toohello 원본 위치에 해당 하는 규칙:

   **위치**: | **Site Recovery 서비스 IP** |  **Site Recovery 모니터링 IP**
    --- | --- | ---
   미국 동부 | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>기존 Azure-온-프레미스 ExpressRoute/VPN 구성에 대한 지침

온-프레미스와 hello 간에 VPN 또는 express 경로도 연결이 있는 경우 Azure의 위치를 원본,이 섹션의 hello 지침을 따릅니다.

### <a name="forced-tunneling-configuration"></a>강제 터널링 구성

일반적인 고객 구성은 toodefine hello 온-프레미스 위치를 통해 아웃 바운드 인터넷 트래픽을 tooflow를 강제로 수행 하는 기본 경로 (0.0.0.0/0). 이는 권장되지 않습니다. 복제 트래픽을 hello 및 사이트 복구 서비스 통신 hello Azure 경계를 유지 하지 해야 합니다. hello 솔루션은 tooadd에 대 한 사용자 정의 경로 (UDRs) [이러한 IP 범위](#outbound-connectivity-for-azure-site-recovery-ip-ranges) hello 복제 트래픽을 온-프레미스를 이동 하지 않습니다.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Hello 대상 및 온-프레미스 위치 간 연결

Hello 대상 위치와 hello 온-프레미스 위치 간 연결에 대 한 다음이 지침을 따릅니다.
- 응용 프로그램에 필요한 tooconnect toohello 온-프레미스 컴퓨터 또는 VPN/ExpressRoute를 통해 온-프레미스에서 toohello 응용 프로그램을 연결 하는 클라이언트가 없는 경우 갖추어야 할 적어도 [사이트 간 연결](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) 사이 대상 Azure 지역과 hello 온-프레미스 데이터 센터입니다.

- 경우에 예상 되는 대상 Azure 지역 및 hello 온-프레미스 데이터 센터 간의 트래픽 tooflow 많이 만든 다른 [ExpressRoute 연결](../expressroute/expressroute-introduction.md) hello 대상 Azure 지역과 hello 온-프레미스 데이터 센터 사이입니다.

- 장애 조치 후 hello 가상 컴퓨터에 대 한 Ip tooretain 사용 하려면, 연결이 끊어진 상태에서 hello 대상 지역 사이트-에-사이트/ExpressRoute 연결을 유지 합니다. 이 없는 범위 충돌 hello 소스 영역 IP 범위 및 대상 지역 IP 범위 사이 인지 toomake입니다.

### <a name="best-practices-for-expressroute-configuration"></a>ExpressRoute 구성에 대한 모범 사례
ExpressRoute 구성의 경우 다음 모범 사례를 따릅니다.

- 두 hello 원본과 대상 지역에서 ExpressRoute 회로 toocreate가 필요합니다. 그런 다음 toocreate 경우 연결이 필요합니다.
  - hello 원본 가상 네트워크 및 hello ExpressRoute 회로 합니다.
  - hello 대상 가상 네트워크 및 hello ExpressRoute 회로 합니다.

- ExpressRoute 표준의 일부로 hello에서 회로 만들 수 있습니다 동일한 지리적 지역입니다. 서로 다른 지리적 지역에 toocreate ExpressRoute 회로 Azure ExpressRoute 프리미엄은 필요한 경우 증분 비용이 포함입니다. ExpressRoute Premium을 이미 사용 중인 경우에는 추가 비용이 발생하지 않습니다. 자세한 내용은 참조 hello [ExpressRoute 위치 문서](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) 및 [ExpressRoute 가격](https://azure.microsoft.com/pricing/details/expressroute/)합니다.

- 원본 지역과 대상 지역에서 서로 다른 IP 범위를 사용하는 것이 좋습니다. ExpressRoute 회로 hello 못할 hello에 tooconnect hello의 두 Azure 가상 네트워크와 동일한 IP 범위 동시 합니다.

- Hello 동일한 IP 두 영역으로 범위를 만들고 다음 ExpressRoute 회로 두 지역에 있는 가상 네트워크를 만들 수 있습니다. 장애 조치 이벤트가 hello 경우 hello 회로 hello 원본 가상 네트워크에서 분리 하 고 hello 회로 hello 대상 가상 네트워크에 연결 합니다.

 >[!IMPORTANT]
 > Hello 완전히 아래쪽 hello 기본 지역의 경우, 연결 끊기 작업이 실패할 수 있습니다. Hello 대상 가상 네트워크를 방지 하는 express 경로 연결 수 없도록 합니다.

## <a name="next-steps"></a>다음 단계
[Azure Virtual Machines를 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호를 시작합니다.
