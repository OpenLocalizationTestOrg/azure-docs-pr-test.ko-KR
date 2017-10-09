## <span data-ttu-id="fad9d-101"><a name="os-config"></a>IP 주소 tooa VM 운영 체제 추가</span><span class="sxs-lookup"><span data-stu-id="fad9d-101"><a name="os-config"></a>Add IP addresses tooa VM operating system</span></span>

<span data-ttu-id="fad9d-102">연결 하 고 여러 개인 IP 주소를 사용 하 여 만든 로그인 tooa VM입니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-102">Connect and login tooa VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="fad9d-103">모든 hello 개인 IP 주소 (주 복제본 hello 포함) 추가한 toohello VM을 수동으로 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-103">You must manually add all hello private IP addresses (including hello primary) that you added toohello VM.</span></span> <span data-ttu-id="fad9d-104">Hello VM 운영 체제에 대 한 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-104">Complete hello following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="fad9d-105">Windows</span><span class="sxs-lookup"><span data-stu-id="fad9d-105">Windows</span></span>

1. <span data-ttu-id="fad9d-106">명령 프롬프트에서 *ipconfig /all*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="fad9d-107">Hello에만 표시 *기본* (DHCP)를 통한 개인 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-107">You only see hello *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="fad9d-108">형식 *ncpa.cpl* hello 명령 프롬프트 tooopen hello에 **네트워크 연결** 창.</span><span class="sxs-lookup"><span data-stu-id="fad9d-108">Type *ncpa.cpl* in hello command prompt tooopen hello **Network connections** window.</span></span>
3. <span data-ttu-id="fad9d-109">Hello 적절 한 어댑터에 대 한 hello 속성을 열고: **로컬 영역 연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-109">Open hello properties for hello appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="fad9d-110">IPv4(인터넷 프로토콜 버전 4)를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="fad9d-111">선택 **다음 IP 주소 사용 하 여 hello** hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-111">Select **Use hello following IP address** and enter hello following values:</span></span>

    * <span data-ttu-id="fad9d-112">**IP 주소**: hello 입력 *기본* 개인 IP 주소</span><span class="sxs-lookup"><span data-stu-id="fad9d-112">**IP address**: Enter hello *Primary* private IP address</span></span>
    * <span data-ttu-id="fad9d-113">**서브넷 마스크**: 서브넷을 기준으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="fad9d-114">예를 들어 경우 hello 서브넷은 / 24 서브넷 다음 hello 서브넷 마스크는 255.255.255.0입니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-114">For example, if hello subnet is a /24 subnet then hello subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="fad9d-115">**기본 게이트웨이**: hello hello 서브넷에서 첫 번째 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-115">**Default gateway**: hello first IP address in hello subnet.</span></span> <span data-ttu-id="fad9d-116">서브넷 10.0.0.0/24 이면 hello 게이트웨이 IP 주소는 10.0.0.1 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-116">If your subnet is 10.0.0.0/24, then hello gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="fad9d-117">클릭 **다음 DNS 서버 주소를 사용 하 여 hello** hello 다음 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-117">Click **Use hello following DNS server addresses** and enter hello following values:</span></span>
        * <span data-ttu-id="fad9d-118">**기본 설정 DNS 서버**: 자체 DNS 서버를 사용하지 않는 경우 168.63.129.16을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="fad9d-119">자체 DNS 서버를 사용 하는 서버에 대 한 hello IP 주소를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-119">If you are using your own DNS server, enter hello IP address for your server.</span></span>
    * <span data-ttu-id="fad9d-120">Hello 클릭 **고급** 단추 및 IP 주소를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-120">Click hello **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="fad9d-121">각 hello 보조 개인 IP 주소가 동일한 서브넷 hello 기본 IP 주소에 대해 지정 하는 hello와 8 단계 toohello NIC에에서 나열 된 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-121">Add each of hello secondary private IP addresses listed in step 8 toohello NIC with hello same subnet specified for hello primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="fad9d-122">위의 hello 단계를 올바르게 수행 하지 않는 경우 연결 tooyour VM 손실 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-122">If you do not follow hello steps above correctly, you may lose connectivity tooyour VM.</span></span> <span data-ttu-id="fad9d-123">5 단계에 대 한 입력 hello 정보가 진행 하기 전에 정확한 지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-123">Ensure hello information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="fad9d-124">클릭 **확인** tooclose hello TCP/IP 설정을 차례로 **확인** 다시 tooclose hello 어댑터 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-124">Click **OK** tooclose out hello TCP/IP settings and then **OK** again tooclose hello adapter settings.</span></span> <span data-ttu-id="fad9d-125">RDP 연결이 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="fad9d-126">명령 프롬프트에서 *ipconfig /all*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="fad9d-127">추가한 모든 IP 주소가 표시되고 DHCP는 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="fad9d-128">유효성 검사(Windows)</span><span class="sxs-lookup"><span data-stu-id="fad9d-128">Validation (Windows)</span></span>

<span data-ttu-id="fad9d-129">tooensure 수 tooconnect toohello 인터넷 hello 올바르게 사용 하 여 추가한 후 공용 IP 연결을 통해 보조 IP 구성에서 위의 프로세스를 hello 다음 명령을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="fad9d-129">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, once you have added it correctly using steps above, use hello following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="fad9d-130">보조 IP 구성에 대 한 hello 구성에 연결 된 공용 IP 주소를 있으면 toohello 인터넷만 ping 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-130">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="fad9d-131">기본 IP 구성에 대 한 공용 IP 주소를 아니며 필요한 tooping toohello 인터넷</span><span class="sxs-lookup"><span data-stu-id="fad9d-131">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="fad9d-132">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="fad9d-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="fad9d-133">터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-133">Open a terminal window.</span></span>
2. <span data-ttu-id="fad9d-134">Hello 루트 사용자 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-134">Make sure you are hello root user.</span></span> <span data-ttu-id="fad9d-135">가 아닌 경우에 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-135">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="fad9d-136">Hello 네트워크 인터페이스 ('t h 0' 가정)의 hello 구성 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-136">Update hello configuration file of hello network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="fad9d-137">Dhcp에 대 한 hello 기존 행 항목을 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-137">Keep hello existing line item for dhcp.</span></span> <span data-ttu-id="fad9d-138">이전에 hello 기본 IP 주소 구성 된 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-138">hello primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="fad9d-139">명령 다음 hello로 추가 정적 IP 주소에 대 한 구성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-139">Add a configuration for an additional static IP address with hello following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="fad9d-140">.cfg 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="fad9d-141">열기 hello 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-141">Open hello file.</span></span> <span data-ttu-id="fad9d-142">위의 hello hello 파일 끝에 삼각형 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-142">You should see hello following lines at hello end of hello file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="fad9d-143">이 파일에 존재 하는 hello 줄 다음에 오는 줄을 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-143">Add hello following lines after hello lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="fad9d-144">Hello 다음 명령을 사용 하 여 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-144">Save hello file by using hello following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="fad9d-145">다음 명령을 hello로 hello 네트워크 인터페이스를 다시 설정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="fad9d-145">Reset hello network interface with hello following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="fad9d-146">원격 연결을 사용 하는 경우 라인 동일 hello에서 ifdown와 ifup 모두를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-146">Run both ifdown and ifup in hello same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="fad9d-147">Hello IP 주소는 다음 명령을 hello로 toohello 네트워크 인터페이스를 추가 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-147">Verify hello IP address is added toohello network interface with hello following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="fad9d-148">Hello IP 주소 hello 목록의 일부로 추가한 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-148">You should see hello IP address you added as part of hello list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="fad9d-149">Linux(Redhat, CentOS 및 기타)</span><span class="sxs-lookup"><span data-stu-id="fad9d-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="fad9d-150">터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-150">Open a terminal window.</span></span>
2. <span data-ttu-id="fad9d-151">Hello 루트 사용자 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-151">Make sure you are hello root user.</span></span> <span data-ttu-id="fad9d-152">가 아닌 경우에 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-152">If you are not, enter hello following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="fad9d-153">암호를 입력하고 화면 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="fad9d-154">Hello 루트 사용자 인 경우 되 면 다음 명령을 hello로 toohello 네트워크 스크립트 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-154">Once you are hello root user, navigate toohello network scripts folder with hello following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="fad9d-155">목록 hello 관련 hello 다음 명령을 사용 하 여 ifcfg 파일:</span><span class="sxs-lookup"><span data-stu-id="fad9d-155">List hello related ifcfg files using hello following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="fad9d-156">표시 되어야 *ifcfg eth0* hello 파일 중 하 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-156">You should see *ifcfg-eth0* as one of hello files.</span></span>

5. <span data-ttu-id="fad9d-157">아래와 같이 tooadd IP 주소에 대 한 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-157">tooadd an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="fad9d-158">각 IP 구성에 대해 하나의 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="fad9d-159">열기 hello *ifcfg-eth0:0* 다음 명령을 hello로 파일:</span><span class="sxs-lookup"><span data-stu-id="fad9d-159">Open hello *ifcfg-eth0:0* file with hello following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="fad9d-160">콘텐츠 toohello 파일을 추가 *eth0:0* 이 경우 hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-160">Add content toohello file, *eth0:0* in this case, with hello following command.</span></span> <span data-ttu-id="fad9d-161">있는지 tooupdate 정보 IP 주소에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-161">Be sure tooupdate information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="fad9d-162">다음 명령을 hello로 hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-162">Save hello file with hello following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="fad9d-163">Hello 네트워크 서비스를 다시 시작 하 고 hello 다음 명령을 실행 하 여 hello 변경 사항이 정상적으로 수행 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-163">Restart hello network services and make sure hello changes are successful by running hello following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="fad9d-164">Hello IP 주소를 추가, 표시 되어야 *eth0:0*, 반환 되는 hello 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-164">You should see hello IP address you added, *eth0:0*, in hello list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="fad9d-165">유효성 검사(Linux)</span><span class="sxs-lookup"><span data-stu-id="fad9d-165">Validation (Linux)</span></span>

<span data-ttu-id="fad9d-166">다음 명령을 hello를 사용 하 여과 것 tooensure 수 tooconnect toohello는 hello 공용 IP 통해 보조 IP 구성에서 인터넷 연결:</span><span class="sxs-lookup"><span data-stu-id="fad9d-166">tooensure you are able tooconnect toohello internet from your secondary IP configuration via hello public IP associated it, use hello following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="fad9d-167">보조 IP 구성에 대 한 hello 구성에 연결 된 공용 IP 주소를 있으면 toohello 인터넷만 ping 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-167">For secondary IP configurations, you can only ping toohello Internet if hello configuration has a public IP address associated with it.</span></span> <span data-ttu-id="fad9d-168">기본 IP 구성에 대 한 공용 IP 주소를 아니며 필요한 tooping toohello 인터넷</span><span class="sxs-lookup"><span data-stu-id="fad9d-168">For primary IP configurations, a public IP address is not required tooping toohello Internet.</span></span>

<span data-ttu-id="fad9d-169">Linux vm의 경우 보조 NIC에서 toovalidate 아웃 바운드 연결을 시도할 때, tooadd 적절 한 경로 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-169">For Linux VMs, when trying toovalidate outbound connectivity from a secondary NIC, you may need tooadd appropriate routes.</span></span> <span data-ttu-id="fad9d-170">가지가 여러 방법으로 toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fad9d-170">There are many ways toodo this.</span></span> <span data-ttu-id="fad9d-171">Linux 배포에 대한 적절한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fad9d-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="fad9d-172">hello 다음 하나의 메서드 tooaccomplish 이것은:</span><span class="sxs-lookup"><span data-stu-id="fad9d-172">hello following is one method tooaccomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="fad9d-173">있는지 tooreplace 수 있습니다:</span><span class="sxs-lookup"><span data-stu-id="fad9d-173">Be sure tooreplace:</span></span>
    - <span data-ttu-id="fad9d-174">**10.0.0.5** hello 개인 ip 주소는 공용 IP가 있는 주소 관련된 tooit</span><span class="sxs-lookup"><span data-stu-id="fad9d-174">**10.0.0.5** with hello private IP address that has a public IP address associated tooit</span></span>
    - <span data-ttu-id="fad9d-175">**10.0.0.1** tooyour 기본 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="fad9d-175">**10.0.0.1** tooyour default gateway</span></span>
    - <span data-ttu-id="fad9d-176">**eth2** 보조 NIC의 toohello 이름</span><span class="sxs-lookup"><span data-stu-id="fad9d-176">**eth2** toohello name of your secondary NIC</span></span>
