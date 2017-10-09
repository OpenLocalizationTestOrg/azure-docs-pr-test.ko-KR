---
title: "Azure VM 네트워크 처리량 aaaTesting | Microsoft Docs"
description: "Azure 가상 컴퓨터 tootest 처리량 네트워크 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>대역폭/처리량 테스트(NTTTCP)

Azure의 네트워크 처리량 성능을 테스트 때는 최상의 toouse hello 네트워크 테스트를 위한 대상으로 하 고 성능에 영향을 줄 수 있는 다른 리소스의 hello 사용을 최소화 하는 도구입니다. NTTTCP가 권장됩니다.

Hello 도구 tootwo Azure Vm의 hello 복사 크기가 동일 합니다. 하나의 VM 보낸 사람 및 받는 사람으로 다른 hello로 작동합니다.

#### <a name="deploying-vms-for-testing"></a>테스트를 위해 VM 배포
Hello이이 테스트를 위해 두 개의 Vm에 있어야 하는 hello hello 동일한 클라우드 서비스 또는 म 내부 Ip를 사용 하 고 hello 테스트에서 hello 부하 분산 장치를 제외할 수 있도록 동일한 가용성 집합을 hello 합니다. Hello VIP로 가능한 tootest 이지만이 유형의 테스트이 문서의 hello 범위를 벗어납니다.
 
Hello 수신기의 IP 주소를 기록해 둡니다. 해당 IP를 "a.b.c.r"로 지칭하겠습니다.

Hello VM에 hello 코어 수가 적어 둡니다. 이것을 "\#num\_cores"로 지칭하겠습니다.
 
VM hello 발신자와 수신자 VM에서 hello NTTTCP 300 초 (또는 5 분)에 대 한 테스트를 실행 합니다.

팁: hello에 대 한이 테스트를 처음으로 설정 하면 하려고 할 수 있습니다 더 짧은 테스트 기간 tooget 피드백 더 빨리 합니다. Hello 도구 예상 대로 작동 하는지, 되 면 hello 가장 정확한 결과 대 한 hello 테스트 기간 too300 초를 확장 합니다.

> [!NOTE]
> hello 보낸 사람 **및** 수신기를 지정 해야 **동일 hello** 테스트 기간 매개 변수 (-t).

10 초 동안 단일 TCP 스트림 tootest:

수신기 매개 변수: ntttcp -r -t 10 -P 1

송신기 매개 변수: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1

> [!NOTE]
> hello 샘플 앞에 있어야 사용된 tooconfirm 구성 합니다. 올바른 테스트 예제는 이 문서 뒷부분에 나옵니다.

## <a name="testing-vms-running-windows"></a>Windows가 실행되는 VM 테스트:

#### <a name="get-ntttcp-onto-hello-vms"></a>Hello Vm에 NTTTCP를 가져옵니다.

Hello 최신 버전 다운로드: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

또는 <https://www.bing.com/search?q=ntttcp+download>\<로 이동되면 최신 버전을 검색합니다. 첫 번째로 검색되는 항목을 클릭합니다.

NTTTCP를 c:\\tools와 같은 별도 폴더에 추가하는 것을 고려합니다.

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>Hello Windows 방화벽을 통해 NTTTCP 허용
Hello 수신기에서 Windows 방화벽 tooallow hello에 허용 규칙을 NTTTCP 트래픽 tooarrive 만듭니다. 특정 TCP 포트 tooallow 인바운드 아니라 쉬운 tooallow hello 전체 NTTTCP 프로그램 이름으로를입니다.

다음과 같이 hello Windows 방화벽을 통해 ntttcp 허용:

netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

예를 들어, ntttcp.exe toohello를 복사 하는 경우 "c:\\도구" 폴더를 이와 같이 hello 명령 수: 

netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY

#### <a name="running-ntttcp-tests"></a>NTTTCP 테스트 실행

Hello 수신기에서 NTTTCP 시작 (**CMD에서 실행**, PowerShell에서가 아니라):

ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300

Hello VM 4 개의 코어 한 IP 주소는 10.0.0.4가 있으면 다음과 같이 표시 됩니다.

ntttcp -r –m 8,\*,10.0.0.4 -t 300


보낸 사람에 게 hello에서 NTTTCP 시작 (**CMD에서 실행**, PowerShell에서가 아니라):

ntttcp -s –m 8,\*,10.0.0.4 -t 300 

Hello 결과 기다립니다.


## <a name="testing-vms-running-linux"></a>LINUX가 실행되는 VM 테스트:

nttcp-for-linux를 사용합니다. <https://github.com/Microsoft/ntttcp-for-linux>에서 사용할 수 있습니다.

Hello Linux Vm의 경우 (보낸 사람 및 받는 사람)에 다음이 명령을 실행 하 여 Vm에서 linux에 대 한 ntttcp 준비:

CentOS - Git 설치:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - Git 설치:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
둘 다에서 만들고 설치합니다.
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Hello Windows 예제와 같이 hello Linux 수신기의 IP는 10.0.0.4 가정

Hello 수신기에서 Linux에 대 한 NTTTCP를 시작 합니다.

``` bash
ntttcp -r -t 300
```

hello 보낸 사람에서 실행 합니다.

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
테스트 길이 기본값 too60 초 시간 매개 변수가 없는 경우 지정 된

## <a name="testing-between-vms-running-windows-and-linux"></a>Windows 및 LINUX가 실행되는 VM 간의 테스트:

이 시나리오에서 hello 테스트 실행 될 수 있도록 hello 없는 동기화 모드로 설정 해야 합니다. Hello를 사용 하 여 이렇게 **-N 플래그** Linux 용 및 **100ns 플래그** Windows 용입니다.

#### <a name="from-linux-toowindows"></a>Linux tooWindows:

받는 사람 <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

보낸 사람 <Linux>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Windows tooLinux:

받는 사람 <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

보낸 사람 <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>다음 단계
* 그 결과 따라 있을 수 있습니다 공간이 너무[처리량 컴퓨터 네트워크 최적화](virtual-network-optimize-network-bandwidth.md) 시나리오에 대 한 합니다.
* [Azure Virtual Network FAQ(질문과 대답)](virtual-networks-faq.md)에 대해 자세히 알아보기
