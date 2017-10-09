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
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="ad453-103">대역폭/처리량 테스트(NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="ad453-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="ad453-104">Azure의 네트워크 처리량 성능을 테스트 때는 최상의 toouse hello 네트워크 테스트를 위한 대상으로 하 고 성능에 영향을 줄 수 있는 다른 리소스의 hello 사용을 최소화 하는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="ad453-105">NTTTCP가 권장됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="ad453-106">Hello 도구 tootwo Azure Vm의 hello 복사 크기가 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="ad453-107">하나의 VM 보낸 사람 및 받는 사람으로 다른 hello로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="ad453-108">테스트를 위해 VM 배포</span><span class="sxs-lookup"><span data-stu-id="ad453-108">Deploying VMs for testing</span></span>
<span data-ttu-id="ad453-109">Hello이이 테스트를 위해 두 개의 Vm에 있어야 하는 hello hello 동일한 클라우드 서비스 또는 म 내부 Ip를 사용 하 고 hello 테스트에서 hello 부하 분산 장치를 제외할 수 있도록 동일한 가용성 집합을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="ad453-110">Hello VIP로 가능한 tootest 이지만이 유형의 테스트이 문서의 hello 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="ad453-111">Hello 수신기의 IP 주소를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="ad453-112">해당 IP를 "a.b.c.r"로 지칭하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="ad453-113">Hello VM에 hello 코어 수가 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="ad453-114">이것을 "\#num\_cores"로 지칭하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="ad453-115">VM hello 발신자와 수신자 VM에서 hello NTTTCP 300 초 (또는 5 분)에 대 한 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="ad453-116">팁: hello에 대 한이 테스트를 처음으로 설정 하면 하려고 할 수 있습니다 더 짧은 테스트 기간 tooget 피드백 더 빨리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="ad453-117">Hello 도구 예상 대로 작동 하는지, 되 면 hello 가장 정확한 결과 대 한 hello 테스트 기간 too300 초를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="ad453-118">hello 보낸 사람 **및** 수신기를 지정 해야 **동일 hello** 테스트 기간 매개 변수 (-t).</span><span class="sxs-lookup"><span data-stu-id="ad453-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="ad453-119">10 초 동안 단일 TCP 스트림 tootest:</span><span class="sxs-lookup"><span data-stu-id="ad453-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="ad453-120">수신기 매개 변수: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="ad453-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="ad453-121">송신기 매개 변수: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="ad453-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="ad453-122">hello 샘플 앞에 있어야 사용된 tooconfirm 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="ad453-123">올바른 테스트 예제는 이 문서 뒷부분에 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="ad453-124">Windows가 실행되는 VM 테스트:</span><span class="sxs-lookup"><span data-stu-id="ad453-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="ad453-125">Hello Vm에 NTTTCP를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="ad453-126">Hello 최신 버전 다운로드: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="ad453-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="ad453-127">또는 <https://www.bing.com/search?q=ntttcp+download>\<로 이동되면 최신 버전을 검색합니다. 첫 번째로 검색되는 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="ad453-128">NTTTCP를 c:\\tools와 같은 별도 폴더에 추가하는 것을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="ad453-129">Hello Windows 방화벽을 통해 NTTTCP 허용</span><span class="sxs-lookup"><span data-stu-id="ad453-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="ad453-130">Hello 수신기에서 Windows 방화벽 tooallow hello에 허용 규칙을 NTTTCP 트래픽 tooarrive 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="ad453-131">특정 TCP 포트 tooallow 인바운드 아니라 쉬운 tooallow hello 전체 NTTTCP 프로그램 이름으로를입니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="ad453-132">다음과 같이 hello Windows 방화벽을 통해 ntttcp 허용:</span><span class="sxs-lookup"><span data-stu-id="ad453-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="ad453-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="ad453-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="ad453-134">예를 들어, ntttcp.exe toohello를 복사 하는 경우 "c:\\도구" 폴더를 이와 같이 hello 명령 수:</span><span class="sxs-lookup"><span data-stu-id="ad453-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="ad453-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="ad453-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="ad453-136">NTTTCP 테스트 실행</span><span class="sxs-lookup"><span data-stu-id="ad453-136">Running NTTTCP tests</span></span>

<span data-ttu-id="ad453-137">Hello 수신기에서 NTTTCP 시작 (**CMD에서 실행**, PowerShell에서가 아니라):</span><span class="sxs-lookup"><span data-stu-id="ad453-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="ad453-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="ad453-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="ad453-139">Hello VM 4 개의 코어 한 IP 주소는 10.0.0.4가 있으면 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="ad453-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="ad453-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="ad453-141">보낸 사람에 게 hello에서 NTTTCP 시작 (**CMD에서 실행**, PowerShell에서가 아니라):</span><span class="sxs-lookup"><span data-stu-id="ad453-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="ad453-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="ad453-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="ad453-143">Hello 결과 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="ad453-144">LINUX가 실행되는 VM 테스트:</span><span class="sxs-lookup"><span data-stu-id="ad453-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="ad453-145">nttcp-for-linux를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="ad453-146"><https://github.com/Microsoft/ntttcp-for-linux>에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="ad453-147">Hello Linux Vm의 경우 (보낸 사람 및 받는 사람)에 다음이 명령을 실행 하 여 Vm에서 linux에 대 한 ntttcp 준비:</span><span class="sxs-lookup"><span data-stu-id="ad453-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="ad453-148">CentOS - Git 설치:</span><span class="sxs-lookup"><span data-stu-id="ad453-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="ad453-149">Ubuntu - Git 설치:</span><span class="sxs-lookup"><span data-stu-id="ad453-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="ad453-150">둘 다에서 만들고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="ad453-151">Hello Windows 예제와 같이 hello Linux 수신기의 IP는 10.0.0.4 가정</span><span class="sxs-lookup"><span data-stu-id="ad453-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="ad453-152">Hello 수신기에서 Linux에 대 한 NTTTCP를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="ad453-153">hello 보낸 사람에서 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="ad453-154">테스트 길이 기본값 too60 초 시간 매개 변수가 없는 경우 지정 된</span><span class="sxs-lookup"><span data-stu-id="ad453-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="ad453-155">Windows 및 LINUX가 실행되는 VM 간의 테스트:</span><span class="sxs-lookup"><span data-stu-id="ad453-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="ad453-156">이 시나리오에서 hello 테스트 실행 될 수 있도록 hello 없는 동기화 모드로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="ad453-157">Hello를 사용 하 여 이렇게 **-N 플래그** Linux 용 및 **100ns 플래그** Windows 용입니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="ad453-158">Linux tooWindows:</span><span class="sxs-lookup"><span data-stu-id="ad453-158">From Linux tooWindows:</span></span>

<span data-ttu-id="ad453-159">받는 사람 <Windows>:</span><span class="sxs-lookup"><span data-stu-id="ad453-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="ad453-160">보낸 사람 <Linux>:</span><span class="sxs-lookup"><span data-stu-id="ad453-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="ad453-161">Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="ad453-161">From Windows tooLinux:</span></span>

<span data-ttu-id="ad453-162">받는 사람 <Linux>:</span><span class="sxs-lookup"><span data-stu-id="ad453-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="ad453-163">보낸 사람 <Windows>:</span><span class="sxs-lookup"><span data-stu-id="ad453-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="ad453-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ad453-164">Next steps</span></span>
* <span data-ttu-id="ad453-165">그 결과 따라 있을 수 있습니다 공간이 너무[처리량 컴퓨터 네트워크 최적화](virtual-network-optimize-network-bandwidth.md) 시나리오에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad453-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="ad453-166">[Azure Virtual Network FAQ(질문과 대답)](virtual-networks-faq.md)에 대해 자세히 알아보기</span><span class="sxs-lookup"><span data-stu-id="ad453-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
