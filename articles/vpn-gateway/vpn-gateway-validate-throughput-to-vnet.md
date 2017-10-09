---
title: "Microsoft Azure 가상 네트워크 VPN 처리량 tooa 유효성 검사 | Microsoft Docs"
description: "hello이 문서의 목적은 toohelp 사용자 자신의 온-프레미스 리소스 tooan Azure 가상 컴퓨터에서에서 hello 네트워크 처리량의 유효성을 검사 합니다."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a>어떻게 toovalidate VPN 처리량 tooa 가상 네트워크

VPN 게이트웨이 연결 tooestablish Azure 내에서 가상 네트워크와 온-프레미스 간의 보안 크로스-프레미스 연결을 사용 하면 IT 인프라입니다.

이 문서에서는 어떻게 toovalidate 네트워크 처리량 hello에서 온-프레미스 리소스 tooan Azure 가상 컴퓨터를 보여 줍니다. 문제 해결 지침도 제공합니다.

>[!NOTE]
>이 문서에서는 toohelp를 진단 하 고 일반적인 문제를 해결 합니다. 다음 정보를 hello를 사용 하 여 없습니다 toosolve hello 문제 라면 [지원에 문의](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.
>
>

## <a name="overview"></a>개요

VPN 게이트웨이 연결 hello hello 다음과 같은 구성 요소가 포함 됩니다.

- 온-프레미스 VPN 장치([유효성 검사된 VPN 장치](vpn-gateway-about-vpn-devices.md#devicetable) 목록 보기).
- 공용 인터넷
- Azure VPN Gateway
- Azure 가상 컴퓨터

hello 다이어그램을 다음 온-프레미스 네트워크 tooan VPN 통해 Azure 가상 네트워크의 hello 논리적 연결을 보여 줍니다.

![논리적 연결의 고객 네트워크 tooMSFT VPN을 사용 하는 네트워크](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a>Hello 최대 예상된 송/수신 계산

1.  응용 프로그램의 기준선 처리량 요구 사항을 결정합니다.
2.  Azure VPN Gateway 처리량 제한을 결정합니다. hello "동시에 집계 처리량 SKU 및 VPN 유형별" 섹션을 참조 하십시오 [계획 및 디자인 VPN 게이트웨이에 대 한](vpn-gateway-plan-design.md)합니다.
3.  Hello 결정 [Azure VM 처리량 지침](../virtual-machines/virtual-machines-windows-sizes.md) VM 크기에 대 한 합니다.
4.  ISP(인터넷 서비스 공급자) 대역폭을 결정합니다.
5.  예상 처리량을 계산합니다((VM, Gateway, ISP)의 최소 대역폭 * 0.8).

계산 된 처리량 응용 프로그램의 기본 처리량 요구를 충족 하지 않으면 경우 hello 병목으로 식별 된 hello 리소스의 tooincrease hello 대역폭을 해야 합니다. Azure VPN 게이트웨이 사용 하는 tooresize 참조 [게이트웨이 SKU 변경](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)합니다. 가상 컴퓨터 tooresize 참조 [VM의 크기를 조정](../virtual-machines/virtual-machines-windows-resize-vm.md)합니다. 예상된 인터넷 대역폭을 발생 하지 않은 경우 할 수 있습니다 toocontact ISP입니다.

## <a name="validate-network-throughput-by-using-performance-tools"></a>성능 도구를 사용하여 네트워크 처리량의 유효성 검사

테스트 중에 VPN 터널 처리량 포화가 발생하면 정확한 결과가 제공되지 않으므로 이 유효성 검사는 사용량이 많지 않은 시간에 수행해야 합니다.

이 테스트를 위해 사용 하는 hello 도구는 Windows와 Linux 모두에서 작동 하며 클라이언트와 서버 모드에 있는 iPerf입니다. Windows Vm에 대 한 제한 된 too3 g b p s 이며

이 도구는 모든 읽기/쓰기 작업 toodisk를 수행 하지 않습니다. 전적으로 하나의 끝 toohello 다른에서 생성 된 자체 TCP 트래픽을 생성합니다. 클라이언트와 서버 노드 간에 사용 가능한 hello 대역폭을 측정 하는 실험을 기준으로 통계를 생성 합니다. 두 노드 사이 테스트할 때는 hello 서버와 클라이언트도 다른 hello 역할 하나 합니다. 이 테스트 완료 되 면 hello 역할 tootest 업로드 및 두 노드에서 모두 처리량을 다운로드 하는 둘 다를 반대로 하는 것이 좋습니다.

### <a name="download-iperf"></a>iPerf 다운로드
[iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip)를 다운로드합니다. 자세한 내용은 [iPerf 설명서](https://iperf.fr/iperf-doc.php)를 참조하세요.

 >[!NOTE]
 >이 문서에 나와 있는 hello 타사 제품은 Microsoft와 무관 한 회사에서 제조한 합니다. Microsoft는 이러한 제품의 hello 성능이 나 신뢰성에 대 한 명시적이 든 묵시적 보증도 하지 않습니다.
 >
 >

### <a name="run-iperf-iperf3exe"></a>iPerf(iperf3.exe) 실행
1. (공용 IP 주소는 Azure VM에 대 한 테스트)에 대 한 hello 트래픽을 허용 하는 NSG/ACL 규칙을 사용 하도록 설정 합니다.

2. 두 노드에서 모두 포트 5001에 대한 방화벽 예외를 사용하도록 설정합니다.

    **Windows:** 실행 hello 다음 관리자 권한으로 명령:

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    tooremove hello 규칙을 테스트할 때 완료 되 면이 명령을 실행 합니다.

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    **Azure Linux:** Azure Linux 이미지에는 허용되는 방화벽이 있습니다. 포트에서 수신 하는 응용 프로그램 이면 통해 hello 트래픽이 허용 됩니다. 보안 설정된 사용자 지정 이미지를 사용하려면 명시적으로 열린 포트가 필요할 수 있습니다. 일반적인 Linux OS 계층 방화벽에는 `iptables`, `ufw` 또는 `firewalld`가 포함됩니다.

3. Hello 서버 노드에서 iperf3.exe 추출한 toohello 디렉터리를 변경 합니다. 그런 다음 iPerf 서버 모드에서 실행으로 설정 하십시오 toolisten 5001이 고 포트에서 다음 명령을 hello:

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. Hello 클라이언트 노드에서 toohello 디렉터리 iperf 도구는 추출 하 고 다음 hello 다음 명령을 실행 하는 위치를 변경 합니다.

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    hello 클라이언트는 30 초 동안 5001 toohello 서버 포트에서 트래픽을 실행 합니다. 플래그 hello '-P ' 32 동시 연결 toohello 서버 노드를 사용 하는 것을 나타내는입니다.

    hello 다음 화면이 hello 출력을에서 표시이 예제:

    ![출력](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. (선택 사항) toopreserve hello 테스트 결과이 명령을 실행 합니다.

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. Hello 이전 단계를 완료 한 후 hello 역할과 동일한 단계를 되돌릴 hello hello 서버 노드를 이제 수 있도록 클라이언트 hello와 반대로 실행 합니다.

## <a name="address-slow-file-copy-issues"></a>느린 파일 복사 문제 처리
Windows 탐색기를 사용하거나 RDP 세션을 통해 끌어서 놓으면 파일 복사가 느려질 수 있습니다. 이 문제는 일반적으로 tooone 또는 hello 요소 다음의 두 가지 모두 기한:

- Windows 탐색기 및 RDP와 같은 파일 복사 응용 프로그램은 파일을 복사할 때 여러 스레드를 사용하지 않습니다. 성능 향상을 위해 사용 하 여 다중 스레드 파일 복사 응용 프로그램 같은 [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) 16 또는 32 스레드를 사용 하 여 toocopy 파일입니다. toochange hello 스레드 번호 Richcopy, 파일 복사에 대 한 클릭 **동작** > **복사 옵션** > **파일을 복사**합니다.<br><br>
![느린 파일 복사 문제](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)<br>
- 부족한 VM 디스크 읽기/쓰기 속도. 자세한 내용은 [Azure Storage 문제 해결](../storage/common/storage-e2e-troubleshooting.md)을 참조하세요.

## <a name="on-premises-device-external-facing-interface"></a>온-프레미스 장치 외부 연결 인터페이스
Hello 온-프레미스 VPN 장치 인터넷 연결 IP 주소는 hello에 포함 된 경우 [로컬 네트워크](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) Azure의 정의 불가능 toobring 산발적 VPN의 연결을 끊습니다 hello 또는 성능 문제를 발생할 수 있습니다.

## <a name="checking-latency"></a>대기 시간 확인
홉 사이 100 밀리초를 초과 하는 모든 지연 tracert tootrace tooMicrosoft Azure 가장자리 장치 toodetermine를 사용 합니다.

Hello 온-프레미스 네트워크에서 실행 *tracert* hello Azure 게이트웨이 또는 VM의 VIP toohello 합니다. 만 표시 되 면 * 반환 하 고, 아시다시피 hello Azure 가장자리에 도달 했습니다. DNS 이름을 반환 하는 "MSN"를 포함 하는 표시 되 면 hello Microsoft backbone 도달한 알 수 있습니다.<br><br>
![대기 시간 확인](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)

## <a name="next-steps"></a>다음 단계
자세한 정보나 도움말에 대 한 링크를 따라 hello 확인해 보세요.

- [Azure 가상 컴퓨터에 대한 네트워크 처리량 최적화](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
