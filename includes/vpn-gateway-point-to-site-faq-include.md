### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a><span data-ttu-id="4d6db-101">지점 및 사이트 간 연결에 사용할 수 있는 클라이언트 운영 체제는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-101">What client operating systems can I use with Point-to-Site?</span></span>

<span data-ttu-id="4d6db-102">다음과 같은 클라이언트 운영 체제가 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-102">The following client operating systems are supported:</span></span>

* <span data-ttu-id="4d6db-103">Windows 7(32비트 및 64비트)</span><span class="sxs-lookup"><span data-stu-id="4d6db-103">Windows 7 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="4d6db-104">Windows Server 2008 R2(64비트 전용)</span><span class="sxs-lookup"><span data-stu-id="4d6db-104">Windows Server 2008 R2 (64-bit only)</span></span>
* <span data-ttu-id="4d6db-105">Windows 8(32비트 및 64비트)</span><span class="sxs-lookup"><span data-stu-id="4d6db-105">Windows 8 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="4d6db-106">Windows 8.1(32비트 및 64비트)</span><span class="sxs-lookup"><span data-stu-id="4d6db-106">Windows 8.1 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="4d6db-107">Windows Server 2012(64비트 전용)</span><span class="sxs-lookup"><span data-stu-id="4d6db-107">Windows Server 2012 (64-bit only)</span></span>
* <span data-ttu-id="4d6db-108">Windows Server 2012 R2(64비트 전용)</span><span class="sxs-lookup"><span data-stu-id="4d6db-108">Windows Server 2012 R2 (64-bit only)</span></span>
* <span data-ttu-id="4d6db-109">Windows 10</span><span class="sxs-lookup"><span data-stu-id="4d6db-109">Windows 10</span></span>

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a><span data-ttu-id="4d6db-110">SSTP를 지원하는 지점 및 사이트 간 연결에 소프트웨어 VPN 클라이언트를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-110">Can I use any software VPN client for Point-to-Site that supports SSTP?</span></span>

<span data-ttu-id="4d6db-111">아니요.</span><span class="sxs-lookup"><span data-stu-id="4d6db-111">No.</span></span> <span data-ttu-id="4d6db-112">위에 나열된 Windows 운영 체제 버전만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-112">Support is limited only to the Windows operating system versions listed above.</span></span>

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a><span data-ttu-id="4d6db-113">지점 및 사이트 간 구성에서 VPN 클라이언트 끝점을 몇 개까지 지정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-113">How many VPN client endpoints can I have in my Point-to-Site configuration?</span></span>

<span data-ttu-id="4d6db-114">최대 128개의 VPN 클라이언트에서 가상 네트워크에 동시에 연결할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-114">We support up to 128 VPN clients to be able to connect to a virtual network at the same time.</span></span>

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a><span data-ttu-id="4d6db-115">지점 및 사이트 간 연결에 내부 PKI 루트 CA를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-115">Can I use my own internal PKI root CA for Point-to-Site connectivity?</span></span>

<span data-ttu-id="4d6db-116">예.</span><span class="sxs-lookup"><span data-stu-id="4d6db-116">Yes.</span></span> <span data-ttu-id="4d6db-117">이전에는 자체 서명한 루트 인증서만 사용할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-117">Previously, only self-signed root certificates could be used.</span></span> <span data-ttu-id="4d6db-118">여전히 20개의 루트 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-118">You can still upload 20 root certificates.</span></span>

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a><span data-ttu-id="4d6db-119">지점 및 사이트 간 기능을 사용하여 프록시와 방화벽을 트래버스할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-119">Can I traverse proxies and firewalls using Point-to-Site capability?</span></span>

<span data-ttu-id="4d6db-120">예.</span><span class="sxs-lookup"><span data-stu-id="4d6db-120">Yes.</span></span> <span data-ttu-id="4d6db-121">SSTP(보안 소켓 터널링 프로토콜)을 사용하여 방화벽을 통해 터널링합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-121">We use SSTP (Secure Socket Tunneling Protocol) to tunnel through firewalls.</span></span> <span data-ttu-id="4d6db-122">이 터널은 HTTP 연결로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-122">This tunnel will appear as an HTTPs connection.</span></span>

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-the-vpn-automatically-reconnect"></a><span data-ttu-id="4d6db-123">지점 및 사이트 간 연결에 대해 구성된 클라이언트 컴퓨터를 다시 시작하면 VPN이 자동으로 다시 연결됩니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-123">If I restart a client computer configured for Point-to-Site, will the VPN automatically reconnect?</span></span>

<span data-ttu-id="4d6db-124">기본적으로 클라이언트 컴퓨터에서는 VPN 연결을 자동으로 다시 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-124">By default, the client computer will not reestablish the VPN connection automatically.</span></span>

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-the-vpn-clients"></a><span data-ttu-id="4d6db-125">지점 및 사이트 간 연결은 VPN 클라이언트에서 자동 다시 연결 및 DDNS를 지원합니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-125">Does Point-to-Site support auto-reconnect and DDNS on the VPN clients?</span></span>

<span data-ttu-id="4d6db-126">자동 다시 연결과 DDNS는 현재 지점 및 사이트 간 VPN에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-126">Auto-reconnect and DDNS are currently not supported in Point-to-Site VPNs.</span></span>

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-the-same-virtual-network"></a><span data-ttu-id="4d6db-127">동일한 가상 네트워크에 대해 사이트 간 구성과 지점 및 사이트 간 구성을 함께 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-127">Can I have Site-to-Site and Point-to-Site configurations coexist for the same virtual network?</span></span>

<span data-ttu-id="4d6db-128">예.</span><span class="sxs-lookup"><span data-stu-id="4d6db-128">Yes.</span></span> <span data-ttu-id="4d6db-129">게이트웨이에 경로 기반 VPN 유형이 있는 경우 이 솔루션이 모두 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-129">Both these solutions will work if you have a RouteBased VPN type for your gateway.</span></span> <span data-ttu-id="4d6db-130">클래식 배포 모델의 경우 동적 게이트웨이가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-130">For the classic deployment model, you need a dynamic gateway.</span></span> <span data-ttu-id="4d6db-131">고정 라우팅 VPN 게이트웨이 또는 `-VpnType PolicyBased` cmdlet을 사용하는 게이트웨이의 지점 및 사이트 간 연결은 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-131">We do not support Point-to-Site for static routing VPN gateways or gateways using the `-VpnType PolicyBased` cmdlet.</span></span>

### <a name="can-i-configure-a-point-to-site-client-to-connect-to-multiple-virtual-networks-at-the-same-time"></a><span data-ttu-id="4d6db-132">지점 및 사이트 간 클라이언트를 여러 가상 네트워크에 동시에 연결하도록 구성할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-132">Can I configure a Point-to-Site client to connect to multiple virtual networks at the same time?</span></span>

<span data-ttu-id="4d6db-133">예, 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-133">Yes, it is possible.</span></span> <span data-ttu-id="4d6db-134">하지만 가상 네트워크에서는 겹치는 IP 접두사를 사용할 수 없으며, 지점 및 사이트 간 주소 공간은 가상 네트워크 간에 겹쳐질 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-134">But the virtual networks cannot have overlapping IP prefixes and the Point-to-Site address spaces must not overlap between the virtual networks.</span></span>

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a><span data-ttu-id="4d6db-135">사이트 간 연결 또는 지점 및 사이트 간 연결을 통해 어느 정도의 처리량을 제공할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="4d6db-135">How much throughput can I expect through Site-to-Site or Point-to-Site connections?</span></span>

<span data-ttu-id="4d6db-136">VPN 터널의 정확한 처리량을 유지하는 것은 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-136">It's difficult to maintain the exact throughput of the VPN tunnels.</span></span> <span data-ttu-id="4d6db-137">IPsec과 SSTP는 암호화 중심 VPN 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-137">IPsec and SSTP are crypto-heavy VPN protocols.</span></span> <span data-ttu-id="4d6db-138">또한 처리량은 프레미스와 인터넷 간의 대기 시간과 대역폭에 의해 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d6db-138">Throughput is also limited by the latency and bandwidth between your premises and the Internet.</span></span>