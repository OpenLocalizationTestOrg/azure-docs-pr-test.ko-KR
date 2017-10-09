---
title: "i p v 6-Azure 템플릿 인터넷 연결 부하 분산 aaaDeploy | Microsoft Docs"
description: "어떻게 toodeploy IPv6 Azure 부하 분산 장치 및 부하 분산 된 Vm에 대 한 지원."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: "ipv6, Azure Load Balancer, 이중 스택, 공용 IP, 기본 ipv6, 모바일, iot"
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>템플릿을 사용하여 IPv6로 인터넷 연결 부하 분산 장치 솔루션을 배포합니다.

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [템플릿](load-balancer-ipv6-internet-template.md)

Azure 부하 분산 장치는 계층 4(TCP, UDP) 부하 분산 장치입니다. hello 부하 분산 장치 부하 분산 장치 집합의 가상 컴퓨터 또는 클라우드 서비스의 비정상 상태 서비스 인스턴스 간에 들어오는 트래픽을 분산 하 여 고가용성을 제공 합니다. Azure Load Balancer는 여러 포트, 여러 IP 주소 또는 둘 다에서 이러한 서비스를 제공할 수도 있습니다.

## <a name="example-deployment-scenario"></a>예제 배포 시나리오

hello 다음 다이어그램에서는 hello 부하 분산 솔루션이이 문서에서 설명 하는 hello 예제 서식 파일을 사용 하 여 배포 되 고 있습니다.

![부하 분산 장치 시나리오](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

이 시나리오에서는 Azure 리소스를 수행 하는 hello를 만듭니다.

* 할당된 IPv4 및 IPv6 주소를 사용하는 각 VM에 대한 가상 네트워크 인터페이스
* IPv4 및 IPv6 공용 IP 주소를 가진 인터넷 연결 부하 분산 장치
* 두 개의 끝점을 로드 균형 조정 규칙 toomap hello 공용 Vip toohello 개인
* hello 두 Vm이 포함 된 가용성 집합
* 2개의 가상 컴퓨터(VM)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Azure 포털 hello를 사용 하 여 hello 템플릿을 배포 합니다.

이 문서는 hello에 게시 된 템플릿을 참조 [Azure 빠른 시작 템플릿](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) 갤러리입니다. Hello 갤러리에서 hello 템플릿을 다운로드 하거나 hello 갤러리에서 직접 Azure의 hello 배포를 시작할 수 있습니다. 이 문서에서는 로컬 컴퓨터를 tooyour hello 서식 파일을 다운로드 한 가정 합니다.

1. Azure 포털 hello 및 사용 권한 toocreate Vm 및 Azure 구독 내에서 네트워킹 리소스를 포함 하는 계정으로 로그인을 엽니다. 또한 기존 리소스를 사용 하지 않으면 hello 계정 있어야 권한 toocreate 리소스 그룹 및 저장소 계정입니다.
2. 클릭 하 여 "+ 새로 만들기" 유형 "템플릿" hello 검색 상자에 hello 메뉴에서 합니다. Hello 검색 결과에서 "템플릿 배포"를 선택 합니다.

    ![lb-ipv6-portal-step2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. 모든 hello 블레이드에서 "템플릿을 배포 합니다."를 클릭 합니다.

    ![lb-ipv6-portal-step3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. "만들기"를 클릭합니다.

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. "템플릿 편집"을 클릭합니다. Hello 기존 내용을 삭제 하 고 hello 템플릿 파일의 전체 내용 hello에에서 복사/붙여넣기 (tooinclude hello 시작 및 종료 {}), "저장"을 클릭 한 다음

    > [!NOTE]
    > 붙여 넣을 때에 Microsoft Internet Explorer를 사용 하는 경우 tooallow toohello Windows 클립보드 액세스를 요청 하는 대화 상자가 나타납니다. "액세스 허용"을 클릭합니다.

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. "매개 변수 편집"을 클릭합니다. Hello 매개 변수 블레이드 hello 템플릿 매개 변수 섹션에서에서 hello 지침에 따라 hello 값을 지정 하 고 "저장" tooclose hello 매개 변수 블레이드 클릭 합니다. 사용자 지정 배포 블레이드에서 hello 구독, 기존 리소스 그룹을 선택 하거나 만드십시오. 리소스 그룹을 만들면 hello 리소스 그룹에 대 한 위치를 선택 합니다. 그런 다음 클릭 **약관**, 클릭 **구매** hello 약관에 대 한 합니다. Azure는 hello 리소스 배포를 시작 합니다. 몇 분 toodeploy hello 리소스를 모두 필요합니다.

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    이러한 매개 변수에 대 한 자세한 내용은 참조 hello [템플릿 매개 변수 및 변수](#template-parameters-and-variables) 이 문서의 뒷부분에 나오는 섹션.

7. hello 템플릿에 의해 생성 된 toosee hello 리소스 찾아보기, "리소스 그룹"을 참조 후를 클릭 하 여 hello 목록 아래로 스크롤하여 클릭 합니다.

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. Hello 리소스 그룹 블레이드에서 6 단계에서 지정한 hello 리소스 그룹의 hello 이름을 클릭 합니다. 배포 된 모든 hello 리소스의 목록을 표시 합니다. 모든 것이 순조롭다면 "마지막 배포" 아래에 "Succeeded"이라고 표시되어야 합니다. 그렇지 않으면 사용 중인 hello 계정 권한을 toocreate hello 필요한 리소스에 있는지 확인 합니다.

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > 6 단계를 완료 한 직후 리소스 그룹을 이동 하는 경우에 "마지막 배포" hello 리소스를 배포 하는 동안 "배포"의 hello 상태에 표시 됩니다.

9. 리소스의 hello 목록에 "myIPv6PublicIP"를 클릭 합니다. IP 주소 아래에서 IPv6 주소에 해당 DNS 이름이 6 단계에서 hello dnsNameforIPv6LbIP 매개 변수에 대해 지정 된 값이 hello 인지 표시 됩니다. 이 리소스는 hello 공용 IPv6 주소 및 호스트 이름을 tooInternet-클라이언트가 액세스할 수 있습니다.

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>연결 유효성 검사

Hello 서식 파일을 성공적으로 배포 하는 경우에 hello 다음 작업을 완료 하 여 연결을 확인할 수 있습니다.

1. Azure 포털 toohello에 로그인 하 고 hello hello 템플릿 배포 하 여 만든 Vm의 tooeach 연결 키를 누릅니다. Windows Server VM을 배포한 경우 명령 프롬프트에서 ipconfig /all을 실행합니다. 표시는 hello Vm IPv4 및 IPv6 모두 주소를 갖게 됩니다. Linux Vm을 배포한 경우 tooconfigure hello Linux OS tooreceive 동적 IPv6 주소 Linux 배포판에 대해 제공 된 hello 지침을 사용 해야 합니다.
2. IPv6 인터넷에 연결 된 클라이언트에서 연결 toohello 공용 IPv6 주소 hello 부하 분산 장치를 시작 합니다. 부하 분산 장치 hello tooconfirm hello 두 Vm 간의 균형은, 각 hello Vm에서 Microsoft 인터넷 정보 서비스 (IIS)와 같은 웹 서버를 설치할 수 있습니다. 각 서버에서 기본 웹 페이지 hello hello 텍스트 "Server0"를 포함 하거나 "Server1" toouniquely 식별 합니다. 그런 다음 IPv6 인터넷에 연결 된 클라이언트에서 인터넷 브라우저를 열고 toohello hostname hello 부하 분산 장치 tooconfirm 종단 간 IPv6 연결 tooeach VM의 hello dnsNameforIPv6LbIP 매개 변수를 지정 합니다. 하나의 서버에서 웹 페이지 hello만 표시 되 면 브라우저 캐시에 tooclear 할 수 있습니다. 여러 개인 찾아보기 세션을 엽니다. 각 서버에서의 응답이 표시됩니다.
3. IPv4 인터넷에 연결 된 클라이언트에서 연결 toohello 공용 IPv4 주소가 hello 부하 분산 장치를 시작 합니다. 부하 분산 장치 hello tooconfirm는 부하 분산 hello 두 Vm, 2 단계에서에서 설명 된 대로 IIS를 사용 하 여 테스트할 수입니다.
4. 각 VM에서 아웃 바운드 연결 tooan IPv6 또는 인터넷 IPv4에 연결 된 장치를 시작 합니다. 두 경우 모두 hello 대상 장치에서 인식 하는 hello 원본 IP는 hello 공용 IPv4 또는 IPv6 주소 hello 부하 분산 장치입니다.

> [!NOTE]
> Hello Azure 네트워크에서에서 ICMP-IPv4 및 IPv6 모두 차단 됩니다. 따라서 ping과 같은 ICMP 도구는 언제나 작동하지 않습니다. tootest 연결 TCPing 같은 TCP 대안을 사용 하 여 또는 PowerShell 테스트 NetConnection cmdlet를 환영 합니다. Hello hello 다이어그램에 표시 된 IP 주소는 표시 될 수 있는 값의 예입니다. Hello IPv6 주소를 동적으로 할당 되었는지, 있으므로 나타나면 hello 주소 다릅니다 되 고 지역에 따라 달라질 수 있습니다. 또한이 hello 백 엔드 풀의 IPv6 주소를 개인 hello 보다 hello hello 부하 분산 장치 toostart 다른 접두사와 함께 공용 IPv6 주소에 대 한 일반적입니다.

## <a name="template-parameters-and-variables"></a>템플릿 매개 변수 및 변수

Azure 리소스 관리자 템플릿 여러 변수와 tooyour 요구를 사용자 지정할 수 있는 매개 변수를 포함 합니다. 변수는 사용자 toochange 하지 않이 고정된 값에 사용 됩니다. 매개 변수는 hello 서식 파일을 배포할 때 사용자 tooprovide를 원하는 값에 사용 됩니다. hello 예제 서식 파일은이 문서에 설명 된 hello 시나리오에 대해 구성 됩니다. 사용자 환경의이 tooneeds이를 사용자 지정할 수 있습니다.

이 문서에서 사용 하는 서식 파일에 hello 다음과 같은 hello 예제 변수 및 매개 변수:

| 매개 변수 / 변수 | 참고 사항 |
| --- | --- |
| adminUsername |Toosign 있는 toohello 가상 컴퓨터에 사용 하는 hello hello 관리자 계정 이름을 지정 합니다. |
| adminPassword |Toosign 있는 toohello 가상 컴퓨터에 사용 하는 hello hello 관리자 계정의 암호를 지정 합니다. |
| dnsNameforIPv4LbIP |Tooassign hello hello 부하 분산 장치의 공개 이름으로 원하는 hello DNS 호스트 이름을 지정 합니다. 이 이름은 toohello 부하 분산 장치의 공용 IPv4 주소를 확인합니다. hello 이름은 소문자 여야 하 고 hello regex 일치: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$ 합니다. |
| dnsNameforIPv6LbIP |Tooassign hello hello 부하 분산 장치의 공개 이름으로 원하는 hello DNS 호스트 이름을 지정 합니다. 이 이름은 toohello 부하 분산 장치의 공용 IPv6 주소를 확인합니다. hello 이름은 소문자 여야 하 고 hello regex 일치: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$ 합니다. Hello 수 IPv4 주소 hello 이름을 동일 합니다. 클라이언트가 보내는 경우이 이름은 Azure에 대 한 DNS 쿼리가 돌아옵니다 hello A 및 AAAA 레코드 모두 hello 이름을 공유 하는 경우. |
| vmNamePrefix |Hello VM 이름 접두사를 지정 합니다. 숫자를 추가 하는 hello 템플릿 (0, 1, 등) toohello 때 이름 hello Vm 만들어집니다. |
| nicNamePrefix |Hello 네트워크 인터페이스 이름 접두사를 지정 합니다. 숫자를 추가 하는 hello 템플릿 (0, 1, 등) hello 네트워크 인터페이스를 만들 때 toohello 이름입니다. |
| storageAccountName |기존 저장소 계정의 hello 이름을 입력 하거나 hello 템플릿으로 만든 새 하나의 toobe의 hello 이름을 지정 합니다. |
| availabilitySetName |Hello 가용성 이름이 toobe Vm hello로 사용 되는 설정 입력 |
| addressPrefix |hello 가상 네트워크의 toodefine hello 주소 범위를 사용 하는 hello 주소 접두사 |
| subnetName |VNet hello에 대 한 생성의 hello 서브넷의 hello 이름 |
| subnetPrefix |hello 서브넷의 toodefine hello 주소 범위를 사용 하는 hello 주소 접두사 |
| vnetName |VNet hello Vm에서 사용 하는 hello에 대 한 hello 이름을 지정 합니다. |
| ipv4PrivateIPAddressType |IP 주소 (정적 또는 동적) hello 개인에 대 한 hello 할당 방법 사용 |
| ipv6PrivateIPAddressType |hello 할당 방법 hello 개인에 대 한 IP 주소 (동적)를 사용 합니다. IPv6 만이 동적 할당을 지원합니다. |
| numberOfInstances |hello 수가 부하 분산 hello 서식 파일에서 배포 된 인스턴스가 |
| ipv4PublicIPAddressName |Hello hello 부하 분산 장치의 공용 IPv4 주소와 toouse toocommunicate 원하는 hello DNS 이름을 지정 합니다. |
| ipv4PublicIPAddressType |hello 공용 IP 주소 (정적 또는 동적)에 사용 되는 hello 할당 방법 |
| Ipv6PublicIPAddressName |Hello hello 부하 분산 장치 공용 IPv6 주소와 toouse toocommunicate 원하는 hello DNS 이름을 지정 합니다. |
| ipv6PublicIPAddressType |hello 할당 방법 hello 공용 IP 주소 (동적)에 사용 합니다. IPv6 만이 동적 할당을 지원합니다. |
| lbName |Hello hello 부하 분산 장치 이름을 지정 합니다. 이 이름은 hello 포털에 표시 되거나 CLI 또는 PowerShell 명령 사용 하 여 tooit 지칭할 때 사용 됩니다. |

hello 서식 파일에서 나머지 변수 hello Azure hello 리소스를 만들 때 할당 된 파생된 값을 포함 합니다. 이러한 변수를 변경하지 마십시오.
