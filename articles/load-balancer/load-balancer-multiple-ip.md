---
title: "Azure에서 여러 IP 구성에서 분산 aaaLoad | Microsoft Docs"
description: "기본 및 보조 IP 구성에서 부하 분산."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>부하 분산을 hello Azure 포털을 사용 하 여 여러 IP 구성은

> [!div class="op_single_selector"]
> * [포털](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

이 문서에서는 Azure 부하 분산 장치에서 여러 ip toouse 보조 네트워크 인터페이스 (NIC)에서 해결 하는 방법을 설명 합니다. 이 시나리오에 대 한 기본 및 보조 NIC 각각 Windows를 실행 하는 두 개의 Vm 했으므로 각 보조 hello Nic가 두 개의 IP 구성 합니다. 각 VM은 contoso.com 및 fabrikam.com 웹 사이트를 둘 다 호스트합니다. 각 웹 사이트는 hello 보조 NIC에서 hello IP 구성의 바인딩된 tooone Azure 부하 분산 장치 tooexpose 두 개의 프런트 엔드 IP 주소를 각 웹 사이트에 hello 웹 사이트에 대 한 toodistribute 트래픽 toohello 각 IP 구성에 대 한 사용 합니다. 이 시나리오에서는으로 백 엔드 풀 IP 주소 모두 같은 포트 번호 hello 합니다.

![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>필수 조건
이 예제에서는 명명 된 리소스 그룹이 있다고 가정 *contosofabrikam* 같은 구성이 hello로:
 -  명명 된 가상 네트워크 포함 *myVNet*, 라는 두 개의 Vm *VM1* 및 *v m 2* 내 각각 동일한 hello 가용성 명명 된 집합 *myAvailset*. 
 - 각 VM에는 주 NIC 및 보조 NIC가 있습니다. hello 기본 Nic 이름이 지정 된 *VM1NIC1* 및 *VM2NIC1* hello 보조 Nic 이름이 지정 되 *VM1NIC2* 및 *VM2NIC2*합니다. 여러 NIC가 있는 VM 만들기에 대한 자세한 내용은 [PowerShell을 사용하여 다중 NIC가 있는 VM 만들기](../virtual-network/virtual-network-deploy-multinic-arm-ps.md)를 참조하세요.

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>여러 IP 구성에 대 한 단계 tooload 잔액

이 문서에 설명 된 tooachieve hello 시나리오 아래에 다음이 단계를 수행 합니다.

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>1 단계: 구성 각 VM에 대 한 보조 Nic hello

각 가상 네트워크에 VM 추가 대 한 IP 구성 설정에 대 한 보조 NIC를 다음과 같이 hello:  

1. 브라우저에서 Azure 포털 toohello 이동: http://portal.azure.com 및 Azure 계정으로 로그인 합니다.
2. Hello의 왼쪽 위에 hello 화면을 hello 리소스 그룹 아이콘을 클릭 하 고 hello 리소스 그룹 hello Vm에 살고 있는 클릭 한 다음 (예를 들어 *contosofabrikam*). hello **리소스 그룹** 블레이드 hello Vm에 대 한 hello 네트워크 인터페이스와 함께 모든 hello 리소스를 나열 하는 표시 됩니다.
3. toohello 보조 NIC 각 VM의 IP 구성을 다음과 같이 추가 합니다.
    1. Hello 네트워크 인터페이스에 tooadd hello IP 구성을 선택 합니다.
    2. Hello 블레이드에서 나타나는 선택한 NIC hello에 대 한 클릭 **IP 구성을**합니다. 클릭 **추가** hello 나타나는 hello 블레이드 위쪽 방향으로 합니다.
    3. Hello에 **IP 추가 구성을** 블레이드를 다음과 같이 두 번째 IP 구성 toohello NIC를 추가 합니다. 
        1. 보조 IP 구성의 이름을 입력 (VM1 및 v m 2 hello로 IP 구성을 이름에 대 한 예를 들어 *VM1NIC2 ipconfig2* 및 *VM2NIC2 ipconfig2* 각각).
        2. **개인 IP 주소**, **할당**에 대해 **정적**을 선택합니다.
        3. **확인**을 클릭합니다.
        4. Hello에 표시 됩니다 hello에 대 한 두 번째 IP 구성을 hello 보조 NIC 완료 되 면 **IP 구성을** NIC. 제공 hello에 대 한 설정 블레이드

### <a name="step-2-create-a-load-balancer"></a>2단계: 부하 분산 장치 만들기

다음과 같이 부하 분산 장치를 만듭니다.

1. 브라우저에서 Azure 포털 toohello 이동: http://portal.azure.com 및 Azure 계정으로 로그인 합니다.
2. Hello의 왼쪽 위에 hello 화면을 클릭 **새로** > **네트워킹** > **부하 분산 장치**합니다. 다음으로 **만들기**를 클릭합니다.
3. Hello에 **부하 분산 장치 만들기** 블레이드, 부하 분산 장치에 대 한 이름 입력 합니다. 여기서는 *mylb*라고 지칭합니다.
4. 공용 IP 주소 아래에서 **PublicIP1**이라는 새 공용 IP를 만듭니다.
5. 리소스 그룹 선택 hello Vm의 기존 리소스 그룹 (예를 들어 *contosofabrikam*). 그런 다음 적절한 위치를 선택하고 **확인**을 클릭합니다. hello 부하 분산 장치 다음 toodeploy를 시작 및 toosuccessfully 완전 한 배포는 몇 분 정도 걸립니다.
6. 배포 된 후 hello 부하 분산 장치 리소스 그룹에 리소스로 표시 됩니다.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>3 단계: 구성 hello 프런트 엔드 IP 풀

다음과 같이 각 웹 사이트(Contoso 및 Fabrikam)에 대해 프런트 엔드 IP 풀을 구성합니다.

1. Hello 포털에서 클릭 **더 많은 서비스** > 형식 **공용 IP 주소** 필터 상자 hello와 클릭 **공용 IP 주소**합니다. 클릭 **추가** hello 나타나는 hello 블레이드 위쪽 방향으로 합니다.
2. 다음과 같이 두 웹 사이트(contoso 및 fabrikam)에 대해 두 개의 공용 IP 주소(*PublicIP1* 및 *PublicIP2*)를 구성합니다.
    1. 프런트 엔드 IP 주소의 이름을 입력합니다.
    2. 에 대 한 **리소스 그룹**, 선택 hello hello Vm의 기존 리소스 그룹 (예를 들어 *contosofabrikam*).
    3. 에 대 한 **위치**, Vm hello 대로 선택 hello 동일한 위치입니다.
    4. **확인**을 클릭합니다.
    5. Hello 두 공용 IP 주소를 만든 후 둘 다에 표시 된 hello **공용 IP** 주소 블레이드입니다.
3. Hello 포털에서 클릭 **더 많은 서비스** > 형식 **부하 분산 장치** 필터 상자 hello와 클릭 **부하 분산 장치**합니다.  
4. Hello 부하 분산 장치를 선택 (*mylb*) tooadd hello 프런트 엔드 IP 풀을 한다는 것입니다.
5. **설정**에서 **프런트 엔드 풀**을 선택합니다. 클릭 **추가** hello 나타나는 hello 블레이드 위쪽 방향으로 합니다.
6. 프런트 엔드 IP 주소의 이름을 입력합니다(*farbikamfe* 또는 **contosofe*).
7. 클릭 **IP 주소** hello에 **선택 공용 IP 주소** 블레이드, 프로그램 프런트 엔드에 대 한 IP 주소 선택 hello (*PublicIP1* 또는 *PublicIP2*).
8. 이 섹션 toocreate hello 두 번째 프런트 엔드 IP 주소 내 too7 3 단계를 반복 합니다.
9. Hello 프런트 엔드 IP 풀 구성이 완료 되 면 hello에 프런트 엔드 IP 주소가 모두 표시 됩니다 **프런트 엔드 IP 풀** 부하 분산 장치의 블레이드입니다. 
    
### <a name="step-4-configure-hello-backend-pool"></a>4 단계: hello 백 엔드 풀 구성   
다음과 같이 각 웹 사이트 (예: Contoso 및 Fabrikam)에 대 한 부하 분산 장치에서 백 엔드 주소 풀 hello를 구성 합니다.
        
1. Hello 포털에서 클릭 **더 많은 서비스** > hello 필터 상자에 부하 분산 장치를 입력 한 다음 클릭 **부하 분산 장치**합니다.  
2. Hello 부하 분산 장치를 선택 (*mylb*) tooadd hello 백 엔드 풀을 한다는 것입니다.
3. **설정**에서 **백 엔드 풀**을 선택합니다. 백 엔드 풀에 대한 이름을 입력합니다(예를 들어 *contosopool* 또는 *fabrikampool*). Hello 클릭 **추가** 단추 맨 위에서 hello hello 블레이드를 표시 합니다. 
4. **Associated to**(연결 대상)에서 **가용성 집합**을 선택합니다.
5. **가용성 집합**에서 **myAvailset**을 선택합니다.
6. 다음과 같이 두 VM에 대해 대상 네트워크 IP 구성을 추가합니다(그림 2 참조).  
    1. 에 대 한 **대상 가상 컴퓨터**, 선택 hello tooadd toohello 백 엔드 풀 (예를 들어 VM1 또는 v m 2)에서 사용할 VM입니다.
    2. 에 대 한 **네트워크 IP 구성**선택 합니다 (예를 들어 VM1NIC2 ipconfig2 또는 VM2NIC2 ipconfig2) 해당 VM에 대 한 hello 보조 Nic IP 구성 합니다.
    ![LB 시나리오 이미지](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **그림 2**: 백 엔드 풀을 사용 하 여 hello 부하 분산 장치 구성  
7. **확인**을 클릭합니다.
8. Hello 백 엔드 풀 구성이 완료 되 면 두 백 엔드 주소 풀 hello에 표시 됩니다 **백 엔드 풀 블레이드** 부하 분산 장치의 합니다.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>5단계: 부하 분산 장치의 상태 프로브 구성
다음과 같이 부하 분산 장치의 상태 프로브를 구성합니다.
    1. Hello 포털에서 더 많은 서비스를 클릭 > hello 필터 상자에 부하 분산 장치를 입력 한 다음 클릭 **부하 분산 장치**합니다.  
    2. Tooadd hello 백 엔드 풀을 원하는 hello 부하 분산 장치를 선택 합니다.
    3. **설정**에서 **상태 프로브**를 선택합니다. 클릭 **추가** hello 나타나는 hello 블레이드 위쪽 방향으로 합니다.
    4. Hello 상태 프로브 (예를 들어, HTTP)에 대 한 이름을 입력 하 고 클릭 **확인**합니다.

### <a name="step-6-configure-load-balancing-rules"></a>6단계: 부하 분산 규칙 구성
다음과 같이 각 웹 사이트에 대한 부하 분산 규칙 (*HTTPc* 및 *HTTPf*)을 구성합니다.
    
1. **설정**에서 **상태 프로브**를 선택합니다. 클릭 **추가** hello 나타나는 hello 블레이드 위쪽 방향으로 합니다.
2. 에 대 한 **이름**, hello 부하 분산 규칙에 대 한 이름을 입력 (예를 들어 *HTTPc* contoso, 또는 *HTTPf* Fabrikam에 대 한)
3. 프런트 엔드 IP 주소에 대 한 hello hello 프런트 엔드 IP 주소를 선택 합니다 (예를 들어 *Contosofe* 또는 *Fabrikamfe*)
4. 에 대 한 **포트** 및 **백 엔드 포트가**, hello 기본값 유지 **80**합니다.
5. **부동 IP(Direct Server Return)**에서**사용**을 클릭합니다.
6. **확인**을 클릭합니다.
7. 이 섹션 toocreate hello 두 번째 부하 분산 장치 규칙 내에서 too6 1 단계를 반복 합니다.
8. Hello 부하 분산 규칙 구성이 완료 하는 경우, 두 규칙 ((*HTTPc* 및 *HTTPf*) hello에 표시 되는 **부하 분산 규칙** 부하 분산 장치의 블레이드입니다.

### <a name="step-7-configure-dns-records"></a>7단계: DNS 레코드 구성
마지막으로 DNS 리소스 레코드 toopoint toohello 각 프런트 엔드 IP 주소 hello 부하 분산 장치를 구성 해야 합니다. 도메인을 Azure DNS에 호스트할 수 있습니다. Load Balancer와 Azure DNS를 사용하는 방법에 대한 자세한 내용은 [다른 Azure 서비스와 함께 Azure DNS 사용](../dns/dns-for-azure-services.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계
- 에 Azure에서 서비스 toocombine 부하 분산 방법에 대 한 자세한 [부하 분산 서비스를 사용 하 여 Azure에서](../traffic-manager/traffic-manager-load-balancing-azure.md)합니다.
- 다른 유형의 로그를 사용 하 여 Azure toomanage에 부하 분산 장치에 문제를 해결 하는 방법에 대해 알아봅니다 [Azure 부하 분산 장치에 대 한 로그 분석](../load-balancer/load-balancer-monitor-log.md)합니다.
