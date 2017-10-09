<span data-ttu-id="7aed7-101">시작 또는 Azure 가상 컴퓨터 (VM)에서 실행 되는 tooan 응용 프로그램을 연결 하는 경우에 여러 가지가 이유가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-101">There are various reasons when you cannot start or connect tooan application running on an Azure virtual machine (VM).</span></span> <span data-ttu-id="7aed7-102">이유는 hello 응용 프로그램 실행 되 고 있지를 포함 하거나, 차단 또는 올바르게 하지 트래픽 toohello 응용 프로그램을 전달 하는 규칙을 네트워킹 수신 대기 포트 hello 예상 hello 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-102">Reasons include hello application not running or listening on hello expected ports, hello listening port blocked, or networking rules not correctly passing traffic toohello application.</span></span> <span data-ttu-id="7aed7-103">이 문서에서는 체계적인 방법 toofind 및 올바른 hello 문제를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-103">This article describes a methodical approach toofind and correct hello problem.</span></span>

<span data-ttu-id="7aed7-104">Tooyour VM 연결 문제가 발생 하는 경우 RDP 또는 SSH를 사용 하 여 먼저 문서 hello 다음 중 하나를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-104">If you are having issues connecting tooyour VM using RDP or SSH, see one of hello following articles first:</span></span>

* [<span data-ttu-id="7aed7-105">원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7aed7-105">Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* <span data-ttu-id="7aed7-106">[SSH (보안 셸) 연결 tooa Linux 기반 Azure 가상 컴퓨터 문제를 해결](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-106">[Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

> [!NOTE]
> <span data-ttu-id="7aed7-107">Azure에는 리소스를 만들고 작업하는 [Resource Manager와 클래식](../articles/resource-manager-deployment-model.md)이라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../articles/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7aed7-108">이 문서에서는 두 모델을 사용 하 여 있지만 대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-108">This article covers using both models, but Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="7aed7-109">이 문서에서 언제 든 지 자세한 도움말을 보려는 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure hello 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-109">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="7aed7-110">또는 Azure 기술 지원 인시던트를 제출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="7aed7-111">Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-111">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="quick-start-troubleshooting-steps"></a><span data-ttu-id="7aed7-112">빠른 시작 문제 해결 단계</span><span class="sxs-lookup"><span data-stu-id="7aed7-112">Quick-start troubleshooting steps</span></span>
<span data-ttu-id="7aed7-113">Tooan 응용 프로그램을 연결 하는 데 문제가 있으면 hello 일반 문제 해결 단계를 수행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-113">If you have problems connecting tooan application, try hello following general troubleshooting steps.</span></span> <span data-ttu-id="7aed7-114">각 단계를 수행 하면 연결 tooyour 응용 프로그램을 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-114">After each step, try connecting tooyour application again:</span></span>

* <span data-ttu-id="7aed7-115">Hello 가상 컴퓨터를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="7aed7-115">Restart hello virtual machine</span></span>
* <span data-ttu-id="7aed7-116">Hello 끝점 다시 / 방화벽 규칙/네트워크 보안 그룹 (NSG) 규칙</span><span class="sxs-lookup"><span data-stu-id="7aed7-116">Recreate hello endpoint / firewall rules / network security group (NSG) rules</span></span>
  * [<span data-ttu-id="7aed7-117">Resource Manager 모델 - 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="7aed7-117">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [<span data-ttu-id="7aed7-118">클래식 모델 - 클라우드 서비스 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="7aed7-118">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* <span data-ttu-id="7aed7-119">다른 Azure 가상 네트워크 등 다른 위치에서 연결</span><span class="sxs-lookup"><span data-stu-id="7aed7-119">Connect from different location, such as a different Azure virtual network</span></span>
* <span data-ttu-id="7aed7-120">Hello 가상 컴퓨터를 다시 배포</span><span class="sxs-lookup"><span data-stu-id="7aed7-120">Redeploy hello virtual machine</span></span>
  * [<span data-ttu-id="7aed7-121">Windows VM 다시 배포</span><span class="sxs-lookup"><span data-stu-id="7aed7-121">Redeploy Windows VM</span></span>](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [<span data-ttu-id="7aed7-122">Linux VM 다시 배포</span><span class="sxs-lookup"><span data-stu-id="7aed7-122">Redeploy Linux VM</span></span>](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* <span data-ttu-id="7aed7-123">Hello 가상 컴퓨터를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-123">Recreate hello virtual machine</span></span>

<span data-ttu-id="7aed7-124">자세한 내용은 [끝점 연결 문제 해결(RDP/SSH/HTTP 등의 오류)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aed7-124">For more information, see [Troubleshooting Endpoint Connectivity (RDP/SSH/HTTP, etc. failures)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).</span></span>

## <a name="detailed-troubleshooting-overview"></a><span data-ttu-id="7aed7-125">자세한 문제 해결 개요</span><span class="sxs-lookup"><span data-stu-id="7aed7-125">Detailed troubleshooting overview</span></span>
<span data-ttu-id="7aed7-126">Azure 가상 컴퓨터에서 실행 되는 응용 프로그램의 tootroubleshoot hello 액세스는 네 가지 주요 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-126">There are four main areas tootroubleshoot hello access of an application that is running on an Azure virtual machine.</span></span>

![응용 프로그램을 시작할 수 없는 문제 해결](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. <span data-ttu-id="7aed7-128">hello hello Azure 가상 컴퓨터에서 실행 중인 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-128">hello application running on hello Azure virtual machine.</span></span>
   * <span data-ttu-id="7aed7-129">자체 hello 응용 프로그램이 올바르게 실행?</span><span class="sxs-lookup"><span data-stu-id="7aed7-129">Is hello application itself running correctly?</span></span>
2. <span data-ttu-id="7aed7-130">hello Azure 가상 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-130">hello Azure virtual machine.</span></span>
   * <span data-ttu-id="7aed7-131">Hello VM 자체 정상적으로 실행 및 toorequests 응답?</span><span class="sxs-lookup"><span data-stu-id="7aed7-131">Is hello VM itself running correctly and responding toorequests?</span></span>
3. <span data-ttu-id="7aed7-132">Azure 네트워크 끝점.</span><span class="sxs-lookup"><span data-stu-id="7aed7-132">Azure network endpoints.</span></span>
   * <span data-ttu-id="7aed7-133">Hello 클래식 배포 모델의 가상 컴퓨터에 대 한 클라우드 서비스 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-133">Cloud service endpoints for virtual machines in hello Classic deployment model.</span></span>
   * <span data-ttu-id="7aed7-134">Resource Manager 배포 모델의 가상 컴퓨터용 네트워크 보안 그룹 및 인바운드 NAT 규칙.</span><span class="sxs-lookup"><span data-stu-id="7aed7-134">Network Security Groups and inbound NAT rules for virtual machines in Resource Manager deployment model.</span></span>
   * <span data-ttu-id="7aed7-135">사용자가 toohello 예상 hello 포트에서 VM 응용 프로그램에서에서 흐름 트래픽 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7aed7-135">Can traffic flow from users toohello VM/application on hello expected ports?</span></span>
4. <span data-ttu-id="7aed7-136">인터넷 에지 장치</span><span class="sxs-lookup"><span data-stu-id="7aed7-136">Your Internet edge device.</span></span>
   * <span data-ttu-id="7aed7-137">트래픽 흐름을 방지하도록 방화벽 규칙이 제대로 적용되고 있나요?</span><span class="sxs-lookup"><span data-stu-id="7aed7-137">Are firewall rules in place preventing traffic from flowing correctly?</span></span>

<span data-ttu-id="7aed7-138">사이트 간 VPN 또는 express 경로 연결을 통해 hello 응용 프로그램에 액세스 하는 클라이언트 컴퓨터에 대 한 문제를 일으킬 수 있는 hello 주요 영역 hello 응용 프로그램 되며 hello Azure 가상 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="7aed7-138">For client computers that are accessing hello application over a site-to-site VPN or ExpressRoute connection, hello main areas that can cause problems are hello application and hello Azure virtual machine.</span></span>

<span data-ttu-id="7aed7-139">toodetermine hello 소스 hello 문제 및 수정 사항이, 다음이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-139">toodetermine hello source of hello problem and its correction, follow these steps.</span></span>

## <a name="step-1-access-application-from-target-vm"></a><span data-ttu-id="7aed7-140">1단계: 대상 VM에서 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="7aed7-140">Step 1: Access application from target VM</span></span>
<span data-ttu-id="7aed7-141">Tooaccess hello에서에서 응용 프로그램 hello 적절 한 클라이언트 프로그램으로 실행 되는 hello VM 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-141">Try tooaccess hello application with hello appropriate client program from hello VM on which it is running.</span></span> <span data-ttu-id="7aed7-142">Hello 로컬 호스트 이름, hello 로컬 IP 주소 또는 hello 루프백 주소 (127.0.0.1)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-142">Use hello local host name, hello local IP address, or hello loopback address (127.0.0.1).</span></span>

![hello VM에서 직접 응용 프로그램을 시작 합니다.](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

<span data-ttu-id="7aed7-144">예를 들어 hello 응용 프로그램은 웹 서버를 hello VM에서 브라우저를 열고 및 tooaccess hello VM에서 호스팅되는 웹 페이지를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-144">For example, if hello application is a web server, open a browser on hello VM and try tooaccess a web page hosted on hello VM.</span></span>

<span data-ttu-id="7aed7-145">Hello 응용 프로그램에 액세스할 수 있으면 너무 이동[2 단계](#step2)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-145">If you can access hello application, go too[Step 2](#step2).</span></span>

<span data-ttu-id="7aed7-146">Hello 응용 프로그램에 액세스할 수 없는 경우 다음 설정을 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-146">If you cannot access hello application, verify hello following settings:</span></span>

* <span data-ttu-id="7aed7-147">hello 응용 프로그램 hello 대상 가상 컴퓨터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-147">hello application is running on hello target virtual machine.</span></span>
* <span data-ttu-id="7aed7-148">hello 응용 프로그램이 예상 hello TCP 및 UDP 포트에서 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-148">hello application is listening on hello expected TCP and UDP ports.</span></span>

<span data-ttu-id="7aed7-149">Windows 및 Linux 기반 가상 컴퓨터를 사용 하 여 hello **netstat-a** tooshow hello 활성 수신 대기 포트 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-149">On both Windows and Linux-based virtual machines, use hello **netstat -a** command tooshow hello active listening ports.</span></span> <span data-ttu-id="7aed7-150">응용 프로그램를 수신 해야 하는 예상 hello 포트에 대 한 hello 출력을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-150">Examine hello output for hello expected ports on which your application should be listening.</span></span> <span data-ttu-id="7aed7-151">Hello 응용 프로그램을 다시 시작 필요에 따라 toouse 예상 hello 포트 구성 하 고 tooaccess hello 응용 프로그램을 로컬 다시 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-151">Restart hello application or configure it toouse hello expected ports as needed and try tooaccess hello application locally again.</span></span>

## <span data-ttu-id="7aed7-152"><a id="step2"></a>2 단계: hello에 다른 VM에서 응용 프로그램을 액세스 동일한 가상 네트워크</span><span class="sxs-lookup"><span data-stu-id="7aed7-152"><a id="step2"></a>Step 2: Access application from another VM in hello same virtual network</span></span>
<span data-ttu-id="7aed7-153">다른 VM에서 tooaccess hello 응용 프로그램을 시도 하지만 동일한 hello hello VM의 호스트 이름 또는 Azure에서 할당 된 public, private 또는 공급자 IP 주소를 사용 하 여 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-153">Try tooaccess hello application from a different VM but in hello same virtual network, using hello VM's host name or its Azure-assigned public, private, or provider IP address.</span></span> <span data-ttu-id="7aed7-154">Hello 클래식 배포 모델을 사용 하 여 만든 가상 컴퓨터에 대 한 hello hello 클라우드 서비스의 공용 IP 주소를 사용 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-154">For virtual machines created using hello classic deployment model, do not use hello public IP address of hello cloud service.</span></span>

![다른 VM에서 응용 프로그램 시작](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

<span data-ttu-id="7aed7-156">예를 들어 hello 응용 프로그램은 웹 서버, try tooaccess 웹 페이지에 있는 다른 VM에 있는 브라우저에서 동일한 가상 네트워크를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-156">For example, if hello application is a web server, try tooaccess a web page from a browser on a different VM in hello same virtual network.</span></span>

<span data-ttu-id="7aed7-157">Hello 응용 프로그램에 액세스할 수 있으면 너무 이동[3 단계](#step3)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-157">If you can access hello application, go too[Step 3](#step3).</span></span>

<span data-ttu-id="7aed7-158">Hello 응용 프로그램에 액세스할 수 없는 경우 다음 설정을 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-158">If you cannot access hello application, verify hello following settings:</span></span>

* <span data-ttu-id="7aed7-159">hello 인바운드 요청과 아웃 바운드 응답 트래픽에 hello 대상 VM에서 hello 호스트 방화벽에서 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-159">hello host firewall on hello target VM is allowing hello inbound request and outbound response traffic.</span></span>
* <span data-ttu-id="7aed7-160">침입 탐지 또는 hello 대상 VM에서 실행 되는 소프트웨어를 모니터링 하는 네트워크 hello 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-160">Intrusion detection or network monitoring software running on hello target VM is allowing hello traffic.</span></span>
* <span data-ttu-id="7aed7-161">클라우드 서비스 끝점 또는 네트워크 보안 그룹 hello 트래픽을 허용:</span><span class="sxs-lookup"><span data-stu-id="7aed7-161">Cloud Services endpoints or Network Security Groups are allowing hello traffic:</span></span>
  * [<span data-ttu-id="7aed7-162">클래식 모델 - 클라우드 서비스 끝점 관리</span><span class="sxs-lookup"><span data-stu-id="7aed7-162">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [<span data-ttu-id="7aed7-163">Resource Manager 모델 - 네트워크 보안 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="7aed7-163">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* <span data-ttu-id="7aed7-164">VM 및 부하 분산 장치 또는 방화벽 같은 VM hello 테스트 간의 hello 경로 있는 VM에서 실행 되는 별도 구성 요소 hello 트래픽을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-164">A separate component running in your VM in hello path between hello test VM and your VM, such as a load balancer or firewall, is allowing hello traffic.</span></span>

<span data-ttu-id="7aed7-165">Windows 기반 가상 컴퓨터에서 hello 방화벽 규칙을 응용 프로그램의 인바운드 및 아웃 바운드 트래픽을 제외 여부에 toodetermine 고급 보안이 있는 Windows 방화벽을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-165">On a Windows-based virtual machine, use Windows Firewall with Advanced Security toodetermine whether hello firewall rules exclude your application's inbound and outbound traffic.</span></span>

## <span data-ttu-id="7aed7-166"><a id="step3"></a>3 단계: hello 가상 네트워크 외부에서 응용 프로그램에 액세스</span><span class="sxs-lookup"><span data-stu-id="7aed7-166"><a id="step3"></a>Step 3: Access application from outside hello virtual network</span></span>
<span data-ttu-id="7aed7-167">Tooaccess hello 응용 프로그램 hello 가상 네트워크 외부 컴퓨터에서 hello 응용 프로그램이 실행 되는 hello VM으로 시도 하세요.</span><span class="sxs-lookup"><span data-stu-id="7aed7-167">Try tooaccess hello application from a computer outside hello virtual network as hello VM on which hello application is running.</span></span> <span data-ttu-id="7aed7-168">다른 네트워크를 원래의 클라이언트 컴퓨터로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-168">Use a different network as your original client computer.</span></span>

![hello 가상 네트워크 외부 컴퓨터에서 응용 프로그램을 시작 합니다.](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

<span data-ttu-id="7aed7-170">예를 들어 hello 응용 프로그램 웹 서버인 경우 hello 가상 네트워크에 있지 않은 컴퓨터에서 실행 되는 브라우저에서 tooaccess hello 웹 페이지를 보십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-170">For example, if hello application is a web server, try tooaccess hello web page from a browser running on a computer that is not in hello virtual network.</span></span>

<span data-ttu-id="7aed7-171">Hello 응용 프로그램에 액세스할 수 없는 경우 다음 설정을 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-171">If you cannot access hello application, verify hello following settings:</span></span>

* <span data-ttu-id="7aed7-172">Vm에 대 한 hello 클래식 배포 모델을 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-172">For VMs created using hello classic deployment model:</span></span>
  
  * <span data-ttu-id="7aed7-173">Hello hello 들어오는 트래픽을, 특히 hello 프로토콜 (TCP 또는 UDP) 및 hello 공용 및 개인 포트 번호를 허용 하는 VM에 대 한 해당 hello 끝점 구성을 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="7aed7-173">Verify that hello endpoint configuration for hello VM is allowing hello incoming traffic, especially hello protocol (TCP or UDP) and hello public and private port numbers.</span></span>
  * <span data-ttu-id="7aed7-174">Hello 끝점에 대 한 액세스 제어 목록 (Acl)을 hello 인터넷에서에서 들어오는 트래픽을 방해 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-174">Verify that access control lists (ACLs) on hello endpoint are not preventing incoming traffic from hello Internet.</span></span>
  * <span data-ttu-id="7aed7-175">자세한 내용은 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-175">For more information, see [How tooSet Up Endpoints tooa Virtual Machine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
* <span data-ttu-id="7aed7-176">Hello 리소스 관리자 배포 모델을 사용 하 여 만든 vm:</span><span class="sxs-lookup"><span data-stu-id="7aed7-176">For VMs created using hello Resource Manager deployment model:</span></span>
  
  * <span data-ttu-id="7aed7-177">hello hello hello 들어오는 트래픽을, 특히 hello 프로토콜 (TCP 또는 UDP) 및 hello 공용 및 개인 포트 번호를 허용 하는 VM에 대 한 인바운드 NAT 규칙 구성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-177">Verify that hello inbound NAT rule configuration for hello VM is allowing hello incoming traffic, especially hello protocol (TCP or UDP) and hello public and private port numbers.</span></span>
  * <span data-ttu-id="7aed7-178">Hello 인바운드 요청과 아웃 바운드 응답 트래픽은 네트워크 보안 그룹은 하도록 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-178">Verify that Network Security Groups are allowing hello inbound request and outbound response traffic.</span></span>
  * <span data-ttu-id="7aed7-179">자세한 내용은 [NSG(네트워크 보안 그룹)란?](../articles/virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="7aed7-179">For more information, see [What is a Network Security Group (NSG)?](../articles/virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="7aed7-180">Hello 가상 컴퓨터 또는 끝점에 부하 분산 된 집합의 구성원 인 경우</span><span class="sxs-lookup"><span data-stu-id="7aed7-180">If hello virtual machine or endpoint is a member of a load-balanced set:</span></span>

* <span data-ttu-id="7aed7-181">Hello 프로브 프로토콜 (TCP 또는 UDP) 및 포트 번호가 올바른지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="7aed7-181">Verify that hello probe protocol (TCP or UDP) and port number are correct.</span></span>
* <span data-ttu-id="7aed7-182">Hello 프로브 경우 프로토콜 및 포트는 hello 부하 분산 집합 프로토콜 및 포트와 다른:</span><span class="sxs-lookup"><span data-stu-id="7aed7-182">If hello probe protocol and port is different than hello load-balanced set protocol and port:</span></span>
  * <span data-ttu-id="7aed7-183">Hello 응용 프로그램이 hello 프로브 프로토콜 (TCP 또는 UDP) 및 포트 번호에서 수신 확인 (사용 하 여 **netstat – a** 대상 VM hello에서).</span><span class="sxs-lookup"><span data-stu-id="7aed7-183">Verify that hello application is listening on hello probe protocol (TCP or UDP) and port number (use **netstat –a** on hello target VM).</span></span>
  * <span data-ttu-id="7aed7-184">VM에서 인바운드 프로브 요청 hello 캡슐화 된 트래픽과 아웃 바운드 프로브 응답을 허용 하는 hello 대상에서 해당 hello 호스트 방화벽을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-184">Verify that hello host firewall on hello target VM is allowing hello inbound probe request and outbound probe response traffic.</span></span>

<span data-ttu-id="7aed7-185">Hello 응용 프로그램에 액세스할 수 있으면 인터넷 가장자리 장치를 허용 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-185">If you can access hello application, ensure that your Internet edge device is allowing:</span></span>

* <span data-ttu-id="7aed7-186">클라이언트 컴퓨터 toohello Azure 가상 컴퓨터에서에서 아웃 바운드 응용 프로그램 요청 트래픽의 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-186">hello outbound application request traffic from your client computer toohello Azure virtual machine.</span></span>
* <span data-ttu-id="7aed7-187">안녕 hello Azure 가상 컴퓨터의에서 응답 트래픽은 인바운드 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="7aed7-187">hello inbound application response traffic from hello Azure virtual machine.</span></span>

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a><span data-ttu-id="7aed7-188">4를 단계 IP 확인 toocheck hello 설정을 사용 하 여 hello 응용 프로그램에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7aed7-188">Step 4 If you cannot access hello application, use IP Verify toocheck hello settings.</span></span> 

<span data-ttu-id="7aed7-189">자세한 내용은 [Azure 네트워크 모니터링 개요](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7aed7-189">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7aed7-190">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7aed7-190">Additional resources</span></span>
[<span data-ttu-id="7aed7-191">원격 데스크톱 연결 tooa Windows 기반 Azure 가상 컴퓨터 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7aed7-191">Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[<span data-ttu-id="7aed7-192">SSH (보안 셸) 연결 tooa Linux 기반 Azure 가상 컴퓨터 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7aed7-192">Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine</span></span>](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

