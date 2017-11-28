## <span data-ttu-id="ead1d-101"><a name="os-config"></a>VM 운영 체제에 IP 주소 추가</span><span class="sxs-lookup"><span data-stu-id="ead1d-101"><a name="os-config"></a>Add IP addresses to a VM operating system</span></span>

<span data-ttu-id="ead1d-102">여러 개인 IP 주소를 사용하여 만든 VM에 연결하고 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-102">Connect and login to a VM you created with multiple private IP addresses.</span></span> <span data-ttu-id="ead1d-103">VM에 추가한 모든 개인 IP 주소(기본 포함)를 수동으로 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-103">You must manually add all the private IP addresses (including the primary) that you added to the VM.</span></span> <span data-ttu-id="ead1d-104">VM 운영 체제에 대한 다음 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-104">Complete the following steps for your VM operating system:</span></span>

### <a name="windows"></a><span data-ttu-id="ead1d-105">Windows</span><span class="sxs-lookup"><span data-stu-id="ead1d-105">Windows</span></span>

1. <span data-ttu-id="ead1d-106">명령 프롬프트에서 *ipconfig /all*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-106">From a command prompt, type *ipconfig /all*.</span></span>  <span data-ttu-id="ead1d-107">*기본* 개인 IP 주소(DHCP를 통한)만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-107">You only see the *Primary* private IP address (through DHCP).</span></span>
2. <span data-ttu-id="ead1d-108">명령 프롬프트 창에 *ncpa.cpl*을 입력하여 **네트워크 연결** 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-108">Type *ncpa.cpl* in the command prompt to open the **Network connections** window.</span></span>
3. <span data-ttu-id="ead1d-109">적절한 어댑터 **로컬 영역 연결**에 대한 속성을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-109">Open the properties for the appropriate adapter: **Local Area Connection**.</span></span>
4. <span data-ttu-id="ead1d-110">IPv4(인터넷 프로토콜 버전 4)를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-110">Double-click Internet Protocol version 4 (IPv4).</span></span>
5. <span data-ttu-id="ead1d-111">**다음 IP 주소 사용**을 선택하고 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-111">Select **Use the following IP address** and enter the following values:</span></span>

    * <span data-ttu-id="ead1d-112">**IP 주소**: *기본* 개인 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-112">**IP address**: Enter the *Primary* private IP address</span></span>
    * <span data-ttu-id="ead1d-113">**서브넷 마스크**: 서브넷을 기준으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-113">**Subnet mask**: Set based on your subnet.</span></span> <span data-ttu-id="ead1d-114">예를 들어 서브넷이 /24이면 서브넷 마스크는 255.255.255.0입니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-114">For example, if the subnet is a /24 subnet then the subnet mask is 255.255.255.0.</span></span>
    * <span data-ttu-id="ead1d-115">**기본 게이트웨이**: 서브넷의 첫 번째 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-115">**Default gateway**: The first IP address in the subnet.</span></span> <span data-ttu-id="ead1d-116">서브넷이 10.0.0.0/24이면 게이트웨이 IP 주소는 10.0.0.1입니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-116">If your subnet is 10.0.0.0/24, then the gateway IP address is 10.0.0.1.</span></span>
    * <span data-ttu-id="ead1d-117">**다음 DNS 서버 주소 사용** 을 클릭하고 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-117">Click **Use the following DNS server addresses** and enter the following values:</span></span>
        * <span data-ttu-id="ead1d-118">**기본 설정 DNS 서버**: 자체 DNS 서버를 사용하지 않는 경우 168.63.129.16을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-118">**Preferred DNS server**: If you are not using your own DNS server, enter 168.63.129.16.</span></span>  <span data-ttu-id="ead1d-119">자체 DNS 서버를 사용하는 경우 서버의 IP 주소를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-119">If you are using your own DNS server, enter the IP address for your server.</span></span>
    * <span data-ttu-id="ead1d-120">**고급** 단추를 클릭하고 추가 IP 주소를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-120">Click the **Advanced** button and add additional IP addresses.</span></span> <span data-ttu-id="ead1d-121">8단계에 나열된 각 보조 개인 IP 주소를 기본 IP 주소에 대해 지정된 것과 동일한 서브넷을 갖는 NIC에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-121">Add each of the secondary private IP addresses listed in step 8 to the NIC with the same subnet specified for the primary IP address.</span></span>
        >[!WARNING] 
        ><span data-ttu-id="ead1d-122">위의 단계를 제대로 따르지 않으면 VM에 대한 연결이 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-122">If you do not follow the steps above correctly, you may lose connectivity to your VM.</span></span> <span data-ttu-id="ead1d-123">계속하기 전에 5단계에서 입력한 정보가 정확한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-123">Ensure the information entered for step 5 is accurate before proceeding.</span></span>

    * <span data-ttu-id="ead1d-124">**확인**을 클릭하여 TCP/IP 설정을 닫은 다음 **확인**을 다시 클릭하여 어댑터 설정을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-124">Click **OK** to close out the TCP/IP settings and then **OK** again to close the adapter settings.</span></span> <span data-ttu-id="ead1d-125">RDP 연결이 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-125">Your RDP connection is re-established.</span></span>

6. <span data-ttu-id="ead1d-126">명령 프롬프트에서 *ipconfig /all*을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-126">From a command prompt, type *ipconfig /all*.</span></span> <span data-ttu-id="ead1d-127">추가한 모든 IP 주소가 표시되고 DHCP는 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-127">All IP addresses you added are shown and DHCP is turned off.</span></span>


### <a name="validation-windows"></a><span data-ttu-id="ead1d-128">유효성 검사(Windows)</span><span class="sxs-lookup"><span data-stu-id="ead1d-128">Validation (Windows)</span></span>

<span data-ttu-id="ead1d-129">보조 IP 구성과 연결된 공용 IP를 통해 인터넷에 연결할 수 있는지 확인하기 위해서 위의 단계를 사용하여 IP를 제대로 추가하고 나면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-129">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, once you have added it correctly using steps above, use the following command:</span></span>

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="ead1d-130">보조 IP 구성의 경우 구성에 공용 IP 주소가 연결된 경우에만 인터넷에 ping할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-130">For secondary IP configurations, you can only ping to the Internet if the configuration has a public IP address associated with it.</span></span> <span data-ttu-id="ead1d-131">기본 IP 구성의 경우 공용 IP 주소가 인터넷에 ping되지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-131">For primary IP configurations, a public IP address is not required to ping to the Internet.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="ead1d-132">Linux(Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="ead1d-132">Linux (Ubuntu)</span></span>

1. <span data-ttu-id="ead1d-133">터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-133">Open a terminal window.</span></span>
2. <span data-ttu-id="ead1d-134">루트 사용자인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-134">Make sure you are the root user.</span></span> <span data-ttu-id="ead1d-135">그렇지 않으면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-135">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="ead1d-136">네트워크 인터페이스(‘eth0’이라고 가정)의 구성 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-136">Update the configuration file of the network interface (assuming ‘eth0’).</span></span>

    * <span data-ttu-id="ead1d-137">dhcp에 대한 기존 줄 항목을 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-137">Keep the existing line item for dhcp.</span></span> <span data-ttu-id="ead1d-138">기본 IP 주소가 이전에 구성된 대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-138">The primary IP address remains configured as it was previously.</span></span>
    * <span data-ttu-id="ead1d-139">다음 명령을 사용하여 추가 정적 IP 주소에 대한 구성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-139">Add a configuration for an additional static IP address with the following commands:</span></span>

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    <span data-ttu-id="ead1d-140">.cfg 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-140">You should see a .cfg file.</span></span>
4. <span data-ttu-id="ead1d-141">파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-141">Open the file.</span></span> <span data-ttu-id="ead1d-142">파일 끝에 다음 줄이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-142">You should see the following lines at the end of the file:</span></span>

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. <span data-ttu-id="ead1d-143">이 파일에 있는 줄 뒤에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-143">Add the following lines after the lines that exist in this file:</span></span>

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. <span data-ttu-id="ead1d-144">다음 명령을 실행하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-144">Save the file by using the following command:</span></span>

    ```bash
    :wq
    ```

7. <span data-ttu-id="ead1d-145">다음 명령을 사용하여 네트워크 인터페이스를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-145">Reset the network interface with the following command:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ead1d-146">원격 연결을 사용하는 경우 같은 줄에서 ifdown 및 ifup을 둘 다 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-146">Run both ifdown and ifup in the same line if using a remote connection.</span></span>
    >

8. <span data-ttu-id="ead1d-147">다음 명령을 사용하여 네트워크 인터페이스에 IP 주소가 추가되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-147">Verify the IP address is added to the network interface with the following command:</span></span>

    ```bash
    ip addr list eth0
    ```

    <span data-ttu-id="ead1d-148">목록의 일부로 추가한 IP 주소가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-148">You should see the IP address you added as part of the list.</span></span>

### <a name="linux-redhat-centos-and-others"></a><span data-ttu-id="ead1d-149">Linux(Redhat, CentOS 및 기타)</span><span class="sxs-lookup"><span data-stu-id="ead1d-149">Linux (Redhat, CentOS, and others)</span></span>

1. <span data-ttu-id="ead1d-150">터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-150">Open a terminal window.</span></span>
2. <span data-ttu-id="ead1d-151">루트 사용자인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-151">Make sure you are the root user.</span></span> <span data-ttu-id="ead1d-152">그렇지 않으면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-152">If you are not, enter the following command:</span></span>

    ```bash
    sudo -i
    ```

3. <span data-ttu-id="ead1d-153">암호를 입력하고 화면 지시를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-153">Enter your password and follow instructions as prompted.</span></span> <span data-ttu-id="ead1d-154">루트 사용자인 경우 다음 명령을 사용하여 네트워크 스크립트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-154">Once you are the root user, navigate to the network scripts folder with the following command:</span></span>

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. <span data-ttu-id="ead1d-155">다음 명령을 사용하여 관련 ifcfg 파일을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-155">List the related ifcfg files using the following command:</span></span>

    ```bash
    ls ifcfg-*
    ```

    <span data-ttu-id="ead1d-156">*ifcfg-eth0* 이 파일 중 하나로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-156">You should see *ifcfg-eth0* as one of the files.</span></span>

5. <span data-ttu-id="ead1d-157">IP 주소를 추가하려면 아래와 같이 그에 대한 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-157">To add an IP address, create a configuration file for it as shown below.</span></span> <span data-ttu-id="ead1d-158">각 IP 구성에 대해 하나의 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-158">Note that one file must be created for each IP configuration.</span></span>

    ```bash
    touch ifcfg-eth0:0
    ```

6. <span data-ttu-id="ead1d-159">다음 명령을 사용하여 *ifcfg-eth0:0* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-159">Open the *ifcfg-eth0:0* file with the following command:</span></span>

    ```bash
    vi ifcfg-eth0:0
    ```

7. <span data-ttu-id="ead1d-160">이 경우에 다음 명령을 사용하여 *eth0:0* 파일에 내용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-160">Add content to the file, *eth0:0* in this case, with the following command.</span></span> <span data-ttu-id="ead1d-161">IP 주소에 따라 정보를 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-161">Be sure to update information based on your IP address.</span></span>

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. <span data-ttu-id="ead1d-162">다음 명령을 실행하여 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-162">Save the file with the following command:</span></span>

    ```bash
    :wq
    ```

9. <span data-ttu-id="ead1d-163">다음 명령을 실행하여 네트워크 서비스를 다시 시작하고 변경이 성공적으로 수행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-163">Restart the network services and make sure the changes are successful by running the following commands:</span></span>

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    <span data-ttu-id="ead1d-164">반환된 목록에서 추가한 IP 주소 *eth0:0*이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-164">You should see the IP address you added, *eth0:0*, in the list returned.</span></span>

### <a name="validation-linux"></a><span data-ttu-id="ead1d-165">유효성 검사(Linux)</span><span class="sxs-lookup"><span data-stu-id="ead1d-165">Validation (Linux)</span></span>

<span data-ttu-id="ead1d-166">보조 IP 구성과 연결된 공용 IP를 통해 인터넷에 연결할 수 있는지 확인하기 위해서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-166">To ensure you are able to connect to the internet from your secondary IP configuration via the public IP associated it, use the following command:</span></span>

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
><span data-ttu-id="ead1d-167">보조 IP 구성의 경우 구성에 공용 IP 주소가 연결된 경우에만 인터넷에 ping할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-167">For secondary IP configurations, you can only ping to the Internet if the configuration has a public IP address associated with it.</span></span> <span data-ttu-id="ead1d-168">기본 IP 구성의 경우 공용 IP 주소가 인터넷에 ping되지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-168">For primary IP configurations, a public IP address is not required to ping to the Internet.</span></span>

<span data-ttu-id="ead1d-169">Linux VM의 경우 보조 NIC의 아웃바운드 연결에 대한 유효성 검사를 시도하는 경우 적절한 경로를 추가해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-169">For Linux VMs, when trying to validate outbound connectivity from a secondary NIC, you may need to add appropriate routes.</span></span> <span data-ttu-id="ead1d-170">이 작업을 수행하는 방법은 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-170">There are many ways to do this.</span></span> <span data-ttu-id="ead1d-171">Linux 배포에 대한 적절한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ead1d-171">Please see appropriate documentation for your Linux distribution.</span></span> <span data-ttu-id="ead1d-172">다음은 이 작업을 수행하는 한 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-172">The following is one method to accomplish this:</span></span>

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- <span data-ttu-id="ead1d-173">반드시 대체할 항목:</span><span class="sxs-lookup"><span data-stu-id="ead1d-173">Be sure to replace:</span></span>
    - <span data-ttu-id="ead1d-174">**10.0.0.5**를 공용 IP 주소가 연결되어 있는 개인 IP 주소로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-174">**10.0.0.5** with the private IP address that has a public IP address associated to it</span></span>
    - <span data-ttu-id="ead1d-175">**10.0.0.1**을 기본 게이트웨이로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-175">**10.0.0.1** to your default gateway</span></span>
    - <span data-ttu-id="ead1d-176">**eth2**를 보조 NIC의 이름으로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ead1d-176">**eth2** to the name of your secondary NIC</span></span>
