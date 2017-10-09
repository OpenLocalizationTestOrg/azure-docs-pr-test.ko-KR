## <a name="scenario"></a><span data-ttu-id="dd862-101">시나리오</span><span class="sxs-lookup"><span data-stu-id="dd862-101">Scenario</span></span>
<span data-ttu-id="dd862-102">이 문서에서는 tooa 가상 컴퓨터 (VM)를 할당 한 고정 공용 IP 주소를 사용 하는 배포 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd862-102">This document will walk through a deployment that uses a static public IP address allocated tooa virtual machine (VM).</span></span> <span data-ttu-id="dd862-103">이 시나리오에는 고유의 고정 공용 IP 주소를 사용하는 단일 VM이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd862-103">In this scenario, you have a single VM with its own static public IP address.</span></span> <span data-ttu-id="dd862-104">이라는 서브넷의 일부인 VM hello **프런트 엔드** 정적 개인 IP 주소 사용 권한과 (**192.168.1.101**) 해당 서브넷에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd862-104">hello VM is part of a subnet named **FrontEnd** and also has a static private IP address (**192.168.1.101**) in that subnet.</span></span>

<span data-ttu-id="dd862-105">hello SSL 인증서가 연결 된 tooan IP SSL 연결을 필요로 하는 웹 서버에 대 한 고정 IP 주소를 할 수 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="dd862-105">You may need a static IP address for web servers that require SSL connections in which hello SSL certificate is linked tooan IP address.</span></span> 

![이미지 설명](./media/virtual-network-deploy-static-pip-scenario-include/figure1.png)

<span data-ttu-id="dd862-107">위의 hello 그림에 표시 된 toodeploy hello 환경 아래 hello 단계를 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd862-107">You can follow hello steps below toodeploy hello environment shown in hello figure above.</span></span>

