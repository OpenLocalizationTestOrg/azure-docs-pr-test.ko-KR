---
title: "사이트 복구와 VMware tooAzure 복제에 대 한 네트워킹 aaaPlan | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용하여 Azure VM을 복제할 때 필요한 네트워크 계획에 대해 설명합니다."
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>3단계: Azure VM 복제를 위한 네트워킹 계획

Hello를 확인 한 후 [배포 필수 구성 요소](azure-to-azure-walkthrough-prerequisites.md), hello를 사용 하 여 복제 하는 Azure 지역 tooanother에서 Azure 가상 컴퓨터 (Vm)를 복구 하는 경우의 고려 사항 네트워킹이 문서 toounderstand hello 읽기 Azure 사이트 복구 서비스입니다. 

- Clear 있어야 hello 문서를 완료 하면 tooset 아웃 바운드를 액세스 하는 방법을 Azure Vm에 대 한 사용자의 이해를 사용할지 tooreplicate, 및 온-프레미스에서 tooconnect toothose Vm 사이트 하는 방법입니다.
- 이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

>[!NOTE]
> Site Recovery를 사용하는 Azure VM 복제는 현재 미리 보기로 제공됩니다.



## <a name="network-overview"></a>네트워크 개요

일반적으로 Azure Vm에는 Azure 가상 네트워크/서브넷에 있고 Azure express 경로 또는 VPN 연결을 사용 하 여 온-프레미스 사이트 tooAzure에서 연결 되어 있습니다.

네트워크는 일반적으로 방화벽 및/또는 NSG(네트워크 보안 그룹)를 사용하여 보호됩니다. 방화벽 IP 기반 목록, toocontrol 네트워크 연결에 대해 URL 기반을 사용할 수 있습니다. NSG는 IP 범위 기반 규칙을 사용합니다. 


사이트 복구 toowork 예상, toomake tooreplicate 원하는 Vm에서 아웃 바운드 네트워크 연결의 일부 변경이 필요 합니다. 사이트 복구는 인증 프록시 toocontrol 네트워크 연결의 사용을 지원 하지 않습니다. 인증 프록시가 있는 경우 복제는 사용할 수 없습니다. 


hello 다음 다이어그램은 Azure Vm에서 실행 중인 응용 프로그램에 대 한 일반적인 환경입니다.

![고객 환경](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Azure VM 환경**

또한 Azure express 경로 또는 VPN 연결을 사용 하 여 온-프레미스 사이트에서 설정 하는 연결 tooAzure을 할 수 있습니다. 

![고객 환경](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**온-프레미스 연결 tooAzure**



## <a name="outbound-connectivity-for-urls"></a>URL에 대한 아웃바운드 연결

URL 기반 방화벽 프록시 toocontrol 아웃 바운드 연결을 사용 하는 경우 사이트 복구에 의해 사용 되는 이러한 Url을 허용 하는지 확인

**URL** | **세부 정보**  
--- | ---
*.blob.core.windows.net | 데이터 toobe를 hello VM hello 소스 지역의 toohello 캐시 저장소 계정에서에서 쓸 수 있습니다.
login.microsoftonline.com | 권한 부여 및 인증 tooSite Recovery 서비스 Url을 제공합니다.
*.hypervrecoverymanager.windowsazure.com | Hello hello VM에서에서 Site Recovery 서비스와 통신을 허용 합니다.
*.servicebus.windows.net | Hello VM에서에서 hello 사이트 복구 모니터링 및 진단 데이터를 쓸 수 있도록 해야 합니다.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>IP 주소 범위에 대한 아웃바운드 연결

- 다운로드 및 실행 하 여 hello NSG에 필요한 hello 규칙을 자동으로 만들 수 [이 스크립트](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702)합니다.
- NSG 테스트에 필요한 hello NSG 규칙을 만들 프로덕션 NSG에서 hello 규칙을 만들기 전에 문제가 없는지 되었는지 확인 하는 것이 좋습니다.
- NSG 규칙 toocreate 필요한 hello 수 가입이 허용 목록 인지 확인 합니다. 고객 지원으로 문의 tooincrease hello NSG 규칙 제한 구독에서입니다.
모든 IP 기반 방화벽 프록시 또는 NSG 규칙 toocontrol 아웃 바운드 연결을 사용 하는 경우 hello 다음 IP 범위 필요 hello 가상 컴퓨터의 hello 원본 및 대상 위치에 따라 toobe 허용 목록.

    - Toohello 원본 위치에 해당 하는 모든 IP 주소 범위 다운로드 hello [범위](https://www.microsoft.com/download/confirmation.aspx?id=41653).) 허용 목록이 반드시 데이터 hello VM에서에서 toohello 캐시 저장소 계정 기록 될 수 있도록 합니다.
    - TooOffice 365 해당 하는 모든 IP 범위 [인증 및 id IP V4 끝점](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)합니다. 새 Ip tooOffice 365 IP 범위 추가 하는 경우 새 NSG 규칙 toocreate 해야 합니다.
-     대상 위치에 따라 달라지는 Site Recovery 서비스 끝점 IP 주소([XML 파일로 제공](https://aka.ms/site-recovery-public-ips)) 

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

## <a name="example-nsg-configuration"></a>NSG 구성 예제

이 여기서는 VM에 대 한 복제 작동 되도록 tooconfigure NSG 규칙 방식 보여줍니다. NSG 규칙 toocontrol 아웃 바운드 연결을 사용 하는 경우 "허용 HTTPS 아웃 바운드" 규칙을 사용 하 여 모든 필요한 hello IP 범위에 대 한 합니다.

이 예제에서는 hello VM 원본 위치는 "미국 동부"입니다. hello 복제 대상 위치는 중앙 미국입니다.


### <a name="example"></a>예제

#### <a name="east-us"></a>미국 동부

1. 너무 해당 하는 규칙을 만들[동부 미국 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653)합니다. 데이터가 VM hello에서 toohello 캐시 저장소 계정 기록 될 수 있도록 이것이 필요 합니다.
2. TooOffice 365 해당 하는 모든 IP 범위에 대 한 규칙을 만들 [인증 및 id IP V4 끝점](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)합니다.
3. Toohello 대상 위치에 해당 하는 규칙을 만듭니다.

   **위치**: | **Site Recovery 서비스 IP** |  **Site Recovery 모니터링 IP**
    --- | --- | ---
   미국 중부 | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>미국 중부

이러한 규칙은 장애 조치 후 hello 대상 지역 toohello 소스 지역에서 복제를 활성화할 수 있습니다 수 있도록 필요 합니다.

1. 너무 해당 하는 규칙을 만들[중앙 미국 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653)합니다.
2. TooOffice 365 해당 하는 모든 IP 범위에 대 한 규칙을 만들 [인증 및 id IP V4 끝점](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity)합니다.
3. Toohello 원본 위치에 해당 하는 규칙을 만듭니다.

   **위치**: | **Site Recovery 서비스 IP** |  **Site Recovery 모니터링 IP**
    --- | --- | ---
   미국 동부 | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>기존 온-프레미스 연결

온-프레미스 사이트와 Azure의 hello 원본 위치 간에 VPN 또는 express 경로 연결 되어 있는 경우 다음이 지침을 따르십시오.

**구성** | **세부 정보**
--- | ---
**강제 터널링** | 기본 경로 (0.0.0.0/0) hello 온-프레미스 위치를 통해 아웃 바운드 인터넷 트래픽을 tooflow 하 게 됩니다. 이 구성은 권장되지 않습니다. 복제 트래픽 및 Site Recovery 통신은 Azure 내에서 유지해야 합니다.<br/><br/> 솔루션을 추가 하는 사용자 정의 경로 (UDRs)에 대 한 [이러한 IP 범위](#outbound-connectivity-for-azure-site-recovery-ip-ranges), hello 트래픽을 온-프레미스를 이동 하지 않습니다.
**연결** | 응용 프로그램 필요 tooconnect tooon 온-프레미스 컴퓨터 또는 온-프레미스 클라이언트 VPN/ExpressRoute를 통해 온-프레미스를 통해 toohello 응용 프로그램을 연결 하는 경우 했는지 확인 최소한 [사이트 간 연결](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)사이의 hello 대상 Azure 지역 및 hello 온-프레미스 사이트입니다.<br/><br/> 다른 트래픽 양을 hello 대상 Azure 지역 및 hello 온-프레미스 사이트 간에 높은 경우 만들 [ExpressRoute 연결](../expressroute/expressroute-introduction.md), hello 대상 지역 및 온-프레미스 사이입니다.<br/><br/> 장애 조치 후 Vm에 대 한 Ip tooretain를 원하는 경우 연결이 끊어진 상태에서 hello 대상 지역 사이트-에-사이트/ExpressRoute 연결을 유지 합니다. 이렇게 하면는 hello 소스 및 대상 IP 주소 범위 사이 범위 충돌 없습니다.
**ExpressRoute** | 원본 및 대상 지역이 hello의 ExpressRoute 회로 만들기.<br/><br/> 및 hello 대상 네트워크와 hello 회로 hello 원본 네트워크 및 hello express 경로 회선 사이의 연결을 만듭니다.<br/><br/> 원본 지역과 대상 지역에서 서로 다른 IP 범위를 사용하는 것이 좋습니다. hello 회로 됩니다 수 tooconnect toomore 동일 hello로 하나의 Azure 네트워크 보다 IP 범위 hello에서 같은 시간입니다.<br/><br/> Hello 동일한 IP 두 영역으로 범위를 만들고 다음 ExpressRoute 회로 두 지역에 있는 가상 네트워크를 만들 수 있습니다. 장애 조치의 경우 hello 소스 가상 네트워크에서 hello 회로 끊고 hello 회로 hello 대상 가상 네트워크에 연결 합니다.<br/><br/> Hello 완전히 아래쪽 hello 기본 지역의 경우, 연결 끊기 작업이 실패할 수 있습니다. 이 경우 hello 대상 가상 네트워크는 express 경로 연결을 가져올 없습니다.
**ExpressRoute Premium** | Hello에 회로 만들면 동일한 지리적 지역입니다.<br/><br/> 서로 다른 지리적 지역에 toocreate 회로 Azure ExpressRoute Premium이 필요 합니다.<br/><br/> Premium을 hello 비용은 증분입니다. 이미 사용 중인 경우 추가 비용은 없습니다.<br/><br/> [위치](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) 및 [가격](https://azure.microsoft.com/pricing/details/expressroute/)에 대해 자세히 알아보세요.



## <a name="next-steps"></a>다음 단계

너무 이동[4 단계: 자격 증명 모음 만들기](azure-to-azure-walkthrough-vault.md)

