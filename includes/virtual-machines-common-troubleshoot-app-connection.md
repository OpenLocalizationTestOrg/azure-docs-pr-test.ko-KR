<span data-ttu-id="15410-101">Azure VM(가상 컴퓨터)에서 실행되는 응용 프로그램을 시작 또는 연결할 수 없는 다양한 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-101">There are various reasons when you cannot start or connect to an application running on an Azure virtual machine (VM).</span></span> <span data-ttu-id="15410-102">이유로는 응용 프로그램이 실행되지 않거나 예상된 포트에서 수신 대기하지 않거나, 수신 포트가 차단되었거나, 네트워킹 규칙이 응용 프로그램에 트래픽을 올바르게 전달하지 않는 등의 경우가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="15410-102">Reasons include the application not running or listening on the expected ports, the listening port blocked, or networking rules not correctly passing traffic to the application.</span></span> <span data-ttu-id="15410-103">이 문서에서는 문제를 찾고 해결하는 체계적인 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-103">This article describes a methodical approach to find and correct the problem.</span></span>

<span data-ttu-id="15410-104">RDP 또는 SSH를 사용하여 VM에 연결하는 데 문제가 있는 경우 먼저 다음 문서 중 하나를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-104">If you are having issues connecting to your VM using RDP or SSH, see one of the following articles first:</span></span>

* [<span data-ttu-id="15410-105">Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="15410-105">Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* <span data-ttu-id="15410-106">[Linux 기반 Azure 가상 컴퓨터에 SSH(보안 셸) 연결 문제 해결](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="15410-106">[Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

> [!NOTE]
> <span data-ttu-id="15410-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../articles/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../articles/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="15410-108">이 문서에서는 두 모델을 모두 사용하여 설명하지만 대부분의 새로운 배포에는 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-108">This article covers using both models, but Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="15410-109">이 문서의 어디에서든 도움이 필요한 경우 [MSDN Azure 및 스택 오버플로 포럼](https://azure.microsoft.com/support/forums/)에서 Azure 전문가에게 문의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-109">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="15410-110">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="15410-111">[Azure 지원 사이트](https://azure.microsoft.com/support/options/) 로 가서 **지원 받기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-111">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="quick-start-troubleshooting-steps"></a><span data-ttu-id="15410-112">빠른 시작 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="15410-112">Quick-start troubleshooting steps</span></span>
<span data-ttu-id="15410-113">응용 프로그램에 연결하는 데 문제가 있는 경우 다음과 같은 일반적인 문제 해결 단계를 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-113">If you have problems connecting to an application, try the following general troubleshooting steps.</span></span> <span data-ttu-id="15410-114">각 단계 후 응용 프로그램을 다시 연결해 보세요.</span><span class="sxs-lookup"><span data-stu-id="15410-114">After each step, try connecting to your application again:</span></span>

* <span data-ttu-id="15410-115">가상 컴퓨터 다시 시작</span><span class="sxs-lookup"><span data-stu-id="15410-115">Restart the virtual machine</span></span>
* <span data-ttu-id="15410-116">끝점 / 방화벽 규칙 / NSG(네트워크 보안 그룹) 규칙 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="15410-116">Recreate the endpoint / firewall rules / network security group (NSG) rules</span></span>
  * [<span data-ttu-id="15410-117">Resource Manager 모델 - 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="15410-117">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [<span data-ttu-id="15410-118">클래식 모델 - 클라우드 서비스 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="15410-118">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* <span data-ttu-id="15410-119">다른 Azure 가상 네트워크 등 다른 위치에서 연결</span><span class="sxs-lookup"><span data-stu-id="15410-119">Connect from different location, such as a different Azure virtual network</span></span>
* <span data-ttu-id="15410-120">가상 컴퓨터 다시 배포</span><span class="sxs-lookup"><span data-stu-id="15410-120">Redeploy the virtual machine</span></span>
  * [<span data-ttu-id="15410-121">Windows VM 다시 배포</span><span class="sxs-lookup"><span data-stu-id="15410-121">Redeploy Windows VM</span></span>](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [<span data-ttu-id="15410-122">Linux VM 다시 배포</span><span class="sxs-lookup"><span data-stu-id="15410-122">Redeploy Linux VM</span></span>](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* <span data-ttu-id="15410-123">가상 컴퓨터 다시 만들기</span><span class="sxs-lookup"><span data-stu-id="15410-123">Recreate the virtual machine</span></span>

<span data-ttu-id="15410-124">자세한 내용은 [끝점 연결 문제 해결(RDP/SSH/HTTP 등의 오류)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-124">For more information, see [Troubleshooting Endpoint Connectivity (RDP/SSH/HTTP, etc. failures)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).</span></span>

## <a name="detailed-troubleshooting-overview"></a><span data-ttu-id="15410-125">자세한 문제 해결 개요</span><span class="sxs-lookup"><span data-stu-id="15410-125">Detailed troubleshooting overview</span></span>
<span data-ttu-id="15410-126">Azure 가상 컴퓨터에서 실행되는 응용 프로그램의 액세스 문제 해결에 대한 4개의 주요 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-126">There are four main areas to troubleshoot the access of an application that is running on an Azure virtual machine.</span></span>

![응용 프로그램을 시작할 수 없는 문제 해결](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. <span data-ttu-id="15410-128">Azure 가상 컴퓨터에서 실행되는 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="15410-128">The application running on the Azure virtual machine.</span></span>
   * <span data-ttu-id="15410-129">응용 프로그램 자체가 제대로 실행되나요?</span><span class="sxs-lookup"><span data-stu-id="15410-129">Is the application itself running correctly?</span></span>
2. <span data-ttu-id="15410-130">Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="15410-130">The Azure virtual machine.</span></span>
   * <span data-ttu-id="15410-131">VM 자체가 제대로 실행되고 요청에 응답하나요?</span><span class="sxs-lookup"><span data-stu-id="15410-131">Is the VM itself running correctly and responding to requests?</span></span>
3. <span data-ttu-id="15410-132">Azure 네트워크 끝점.</span><span class="sxs-lookup"><span data-stu-id="15410-132">Azure network endpoints.</span></span>
   * <span data-ttu-id="15410-133">클래식 배포 모델의 가상 컴퓨터용 클라우드 서비스 끝점.</span><span class="sxs-lookup"><span data-stu-id="15410-133">Cloud service endpoints for virtual machines in the Classic deployment model.</span></span>
   * <span data-ttu-id="15410-134">Resource Manager 배포 모델의 가상 컴퓨터용 네트워크 보안 그룹 및 인바운드 NAT 규칙.</span><span class="sxs-lookup"><span data-stu-id="15410-134">Network Security Groups and inbound NAT rules for virtual machines in Resource Manager deployment model.</span></span>
   * <span data-ttu-id="15410-135">트래픽이 사용자에서 VM/응용 프로그램으로 예상되는 포트에서 흐를 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="15410-135">Can traffic flow from users to the VM/application on the expected ports?</span></span>
4. <span data-ttu-id="15410-136">인터넷 에지 장치</span><span class="sxs-lookup"><span data-stu-id="15410-136">Your Internet edge device.</span></span>
   * <span data-ttu-id="15410-137">트래픽 흐름을 방지하도록 방화벽 규칙이 제대로 적용되고 있나요?</span><span class="sxs-lookup"><span data-stu-id="15410-137">Are firewall rules in place preventing traffic from flowing correctly?</span></span>

<span data-ttu-id="15410-138">사이트-사이트 VPN 또는 ExpressRoute 연결을 통해 응용 프로그램에 액세스하는 클라이언트 컴퓨터에 대해, 문제를 일으키는 주요 영역은 응용 프로그램 및 Azure 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="15410-138">For client computers that are accessing the application over a site-to-site VPN or ExpressRoute connection, the main areas that can cause problems are the application and the Azure virtual machine.</span></span>

<span data-ttu-id="15410-139">문제 및 해당 보정의 원인을 확인하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-139">To determine the source of the problem and its correction, follow these steps.</span></span>

## <a name="step-1-access-application-from-target-vm"></a><span data-ttu-id="15410-140">1단계: 대상 VM에서 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="15410-140">Step 1: Access application from target VM</span></span>
<span data-ttu-id="15410-141">응용 프로그램이 실행 중인 VM에서 해당 클라이언트 프로그램으로 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-141">Try to access the application with the appropriate client program from the VM on which it is running.</span></span> <span data-ttu-id="15410-142">로컬 호스트 이름, 로컬 IP 주소 또는 루프백 주소(127.0.0.1)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-142">Use the local host name, the local IP address, or the loopback address (127.0.0.1).</span></span>

![VM에서 직접 응용 프로그램 시작](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

<span data-ttu-id="15410-144">예를 들어 응용 프로그램이 웹 서버인 경우, VM에서 브라우저를 열고 해당 VM에서 호스트되는 웹 페이지에 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-144">For example, if the application is a web server, open a browser on the VM and try to access a web page hosted on the VM.</span></span>

<span data-ttu-id="15410-145">응용 프로그램에 액세스할 수 있는 경우 [2단계](#step2)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-145">If you can access the application, go to [Step 2](#step2).</span></span>

<span data-ttu-id="15410-146">응용 프로그램에 액세스할 수 없는 경우, 다음 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-146">If you cannot access the application, verify the following settings:</span></span>

* <span data-ttu-id="15410-147">응용 프로그램이 목표 가상 컴퓨터에서 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="15410-147">The application is running on the target virtual machine.</span></span>
* <span data-ttu-id="15410-148">응용 프로그램이 예상된 TCP 및 UDP 포트에서 수신 중입니다.</span><span class="sxs-lookup"><span data-stu-id="15410-148">The application is listening on the expected TCP and UDP ports.</span></span>

<span data-ttu-id="15410-149">Windows 및 Linux 기반 가상 컴퓨터 둘 다에서 **netstat -a** 명령을 사용하여 활성 수신 포트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-149">On both Windows and Linux-based virtual machines, use the **netstat -a** command to show the active listening ports.</span></span> <span data-ttu-id="15410-150">응용 프로그램이 수신해야 할 예상되는 포트에 대한 출력을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-150">Examine the output for the expected ports on which your application should be listening.</span></span> <span data-ttu-id="15410-151">응용 프로그램을 다시 시작하거나 필요에 따라 예상되는 포트를 사용하도록 구성하여 다시 로컬로 응용 프로그램에 액세스해 보세요.</span><span class="sxs-lookup"><span data-stu-id="15410-151">Restart the application or configure it to use the expected ports as needed and try to access the application locally again.</span></span>

## <span data-ttu-id="15410-152"><a id="step2"></a>2단계: 동일한 가상 네트워크의 다른 VM에서 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="15410-152"><a id="step2"></a>Step 2: Access application from another VM in the same virtual network</span></span>
<span data-ttu-id="15410-153">VM의 호스트 이름 또는 Azure 할당 공용, 개인 또는 공급자 IP 주소를 사용하여 다른 VM이지만 동일한 가상 네트워크에서 응용 프로그램에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-153">Try to access the application from a different VM but in the same virtual network, using the VM's host name or its Azure-assigned public, private, or provider IP address.</span></span> <span data-ttu-id="15410-154">클래식 배포 모델을 사용하여 만든 가상 컴퓨터의 경우 클라우드 서비스의 공용 IP 주소를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-154">For virtual machines created using the classic deployment model, do not use the public IP address of the cloud service.</span></span>

![다른 VM에서 응용 프로그램 시작](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

<span data-ttu-id="15410-156">예를 들어 응용 프로그램이 웹 서버인 경우, 동일한 가상 네트워크에 있는 다른 VM의 브라우저에서 웹 페이지 액세스를 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-156">For example, if the application is a web server, try to access a web page from a browser on a different VM in the same virtual network.</span></span>

<span data-ttu-id="15410-157">응용 프로그램에 액세스할 수 있는 경우 [3단계](#step3)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-157">If you can access the application, go to [Step 3](#step3).</span></span>

<span data-ttu-id="15410-158">응용 프로그램에 액세스할 수 없는 경우, 다음 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-158">If you cannot access the application, verify the following settings:</span></span>

* <span data-ttu-id="15410-159">대상 VM의 호스트 방화벽이 인바운드 요청 및 아웃 바운드 응답 트래픽을 허용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="15410-159">The host firewall on the target VM is allowing the inbound request and outbound response traffic.</span></span>
* <span data-ttu-id="15410-160">대상 VM에서 실행되는 침입 탐지 또는 네트워크 모니터링 소프트웨어가 트래픽을 허용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="15410-160">Intrusion detection or network monitoring software running on the target VM is allowing the traffic.</span></span>
* <span data-ttu-id="15410-161">Cloud Services 끝점 또는 네트워크 보안 그룹은 다음과 같이 트래픽을 허용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15410-161">Cloud Services endpoints or Network Security Groups are allowing the traffic:</span></span>
  * [<span data-ttu-id="15410-162">클래식 모델 - 클라우드 서비스 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="15410-162">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [<span data-ttu-id="15410-163">Resource Manager 모델 - 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="15410-163">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* <span data-ttu-id="15410-164">부하 분산 장치 또는 방화벽과 같은 테스트 VM 및 VM 간의 경로에서 사용자의 VM에서 실행 중인 개별 구성 요소가 트래픽을 허용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="15410-164">A separate component running in your VM in the path between the test VM and your VM, such as a load balancer or firewall, is allowing the traffic.</span></span>

<span data-ttu-id="15410-165">Windows 기반 가상 컴퓨터에서, 방화벽 규칙이 사용자의 응용 프로그램의 인바운드 및 아웃 바운드 트래픽을 제외할지 여부를 확인하려면 고급 보안이 포함된 Windows 방화벽을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-165">On a Windows-based virtual machine, use Windows Firewall with Advanced Security to determine whether the firewall rules exclude your application's inbound and outbound traffic.</span></span>

## <span data-ttu-id="15410-166"><a id="step3"></a>3단계: 가상 네트워크 외부에서 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="15410-166"><a id="step3"></a>Step 3: Access application from outside the virtual network</span></span>
<span data-ttu-id="15410-167">VM에서 응용 프로그램이 실행되고 있는 경우 가상 네트워크 외부의 컴퓨터에서 응용 프로그램에 대한 액세스를 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-167">Try to access the application from a computer outside the virtual network as the VM on which the application is running.</span></span> <span data-ttu-id="15410-168">다른 네트워크를 원래의 클라이언트 컴퓨터로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-168">Use a different network as your original client computer.</span></span>

![가상 네트워크 외부의 컴퓨터에서 응용 프로그램 시작](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

<span data-ttu-id="15410-170">예를 들면, 응용 프로그램이 웹 서버인 경우, 가상 네트워크에 있지 않은 컴퓨터에서 실행 중인 브라우져에서 웹페이지 액세스를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-170">For example, if the application is a web server, try to access the web page from a browser running on a computer that is not in the virtual network.</span></span>

<span data-ttu-id="15410-171">응용 프로그램에 액세스할 수 없는 경우, 다음 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-171">If you cannot access the application, verify the following settings:</span></span>

* <span data-ttu-id="15410-172">클래식 배포 모델을 사용하여 만든 VM</span><span class="sxs-lookup"><span data-stu-id="15410-172">For VMs created using the classic deployment model:</span></span>
  
  * <span data-ttu-id="15410-173">VM의 끝점 구성에서 수신 트래픽을 허용하는지, 특히 프로토콜(TCP 또는 UDP), 공용 및 개인 포트 번호를 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-173">Verify that the endpoint configuration for the VM is allowing the incoming traffic, especially the protocol (TCP or UDP) and the public and private port numbers.</span></span>
  * <span data-ttu-id="15410-174">끝점의 ACL(액세스 제어 목록)이 인트라넷에서 들어오는 트래픽을 차단하지 않는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-174">Verify that access control lists (ACLs) on the endpoint are not preventing incoming traffic from the Internet.</span></span>
  * <span data-ttu-id="15410-175">자세한 내용은 [가상 컴퓨터로 끝점을 설정하는 방법](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-175">For more information, see [How to Set Up Endpoints to a Virtual Machine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
* <span data-ttu-id="15410-176">Resource Manager 배포 모델을 사용하여 만든 VM</span><span class="sxs-lookup"><span data-stu-id="15410-176">For VMs created using the Resource Manager deployment model:</span></span>
  
  * <span data-ttu-id="15410-177">VM의 인바운드 NAT 규칙 구성에서 수신 트래픽을 허용하는지, 특히 프로토콜(TCP 또는 UDP), 공용 및 개인 포트 번호를 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-177">Verify that the inbound NAT rule configuration for the VM is allowing the incoming traffic, especially the protocol (TCP or UDP) and the public and private port numbers.</span></span>
  * <span data-ttu-id="15410-178">네트워크 보안 그룹이 인바운드 요청 및 아웃바운드 요청 트래픽을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-178">Verify that Network Security Groups are allowing the inbound request and outbound response traffic.</span></span>
  * <span data-ttu-id="15410-179">자세한 내용은 [NSG(네트워크 보안 그룹)란?](../articles/virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="15410-179">For more information, see [What is a Network Security Group (NSG)?](../articles/virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="15410-180">가상 컴퓨터 또는 끝점이 부하 분산 집합의 구성원인 경우:</span><span class="sxs-lookup"><span data-stu-id="15410-180">If the virtual machine or endpoint is a member of a load-balanced set:</span></span>

* <span data-ttu-id="15410-181">프로브 프로토콜(TCP 또는 UDP) 및 포트 번호가 올바른지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-181">Verify that the probe protocol (TCP or UDP) and port number are correct.</span></span>
* <span data-ttu-id="15410-182">프로브 프로토콜 및 포트가 부하 분산 집합 프로토콜 및 포트와 다른 경우:</span><span class="sxs-lookup"><span data-stu-id="15410-182">If the probe protocol and port is different than the load-balanced set protocol and port:</span></span>
  * <span data-ttu-id="15410-183">응용 프로그램이 프로브 프로토콜(TCP 또는 UDP) 및 포트 번호에서 수신 대기 중인지 확인합니다(대상 VM에서 **netstat –a** 사용).</span><span class="sxs-lookup"><span data-stu-id="15410-183">Verify that the application is listening on the probe protocol (TCP or UDP) and port number (use **netstat –a** on the target VM).</span></span>
  * <span data-ttu-id="15410-184">대상 VM의 호스트 방화벽이 인바운드 프로브 요청 및 아웃바운드 프로브 응답 트래픽을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-184">Verify that the host firewall on the target VM is allowing the inbound probe request and outbound probe response traffic.</span></span>

<span data-ttu-id="15410-185">응용 프로그램에 액세스 할 수 있는 경우, 인터넷 에지 장치가 다음을 허용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-185">If you can access the application, ensure that your Internet edge device is allowing:</span></span>

* <span data-ttu-id="15410-186">아웃 바운드 응용 프로그램이 클라이언트 컴퓨터에서 부터 Azure 가상 컴퓨터에 도달하는 트래픽 요청</span><span class="sxs-lookup"><span data-stu-id="15410-186">The outbound application request traffic from your client computer to the Azure virtual machine.</span></span>
* <span data-ttu-id="15410-187">Azure 가상 컴퓨터에서 발생하는 인바운드 응용 프로그램 응답 트래픽</span><span class="sxs-lookup"><span data-stu-id="15410-187">The inbound application response traffic from the Azure virtual machine.</span></span>

## <a name="step-4-if-you-cannot-access-the-application-use-ip-verify-to-check-the-settings"></a><span data-ttu-id="15410-188">4단계: 응용 프로그램에 액세스할 수 없는 경우 IP 확인을 사용하여 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15410-188">Step 4 If you cannot access the application, use IP Verify to check the settings.</span></span> 

<span data-ttu-id="15410-189">자세한 내용은 [Azure 네트워크 모니터링 개요](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="15410-189">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="15410-190">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="15410-190">Additional resources</span></span>
[<span data-ttu-id="15410-191">Windows 기반 Azure 가상 컴퓨터에 대한 원격 데스크톱 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="15410-191">Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[<span data-ttu-id="15410-192">Linux 기반 Azure 가상 컴퓨터에 SSH(보안 셸) 연결 문제 해결</span><span class="sxs-lookup"><span data-stu-id="15410-192">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

