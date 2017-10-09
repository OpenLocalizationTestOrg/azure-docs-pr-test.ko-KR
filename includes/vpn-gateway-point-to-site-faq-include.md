### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a><span data-ttu-id="7985b-101">지점 및 사이트 간 연결에 사용할 수 있는 클라이언트 운영 체제는 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="7985b-101">What client operating systems can I use with Point-to-Site?</span></span>

<span data-ttu-id="7985b-102">다음 클라이언트 운영 체제 hello 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-102">hello following client operating systems are supported:</span></span>

* <span data-ttu-id="7985b-103">Windows 7(32비트 및 64비트)</span><span class="sxs-lookup"><span data-stu-id="7985b-103">Windows 7 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="7985b-104">Windows Server 2008 R2(64비트 전용)</span><span class="sxs-lookup"><span data-stu-id="7985b-104">Windows Server 2008 R2 (64-bit only)</span></span>
* <span data-ttu-id="7985b-105">Windows 8(32비트 및 64비트)</span><span class="sxs-lookup"><span data-stu-id="7985b-105">Windows 8 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="7985b-106">Windows 8.1(32비트 및 64비트)</span><span class="sxs-lookup"><span data-stu-id="7985b-106">Windows 8.1 (32-bit and 64-bit)</span></span>
* <span data-ttu-id="7985b-107">Windows Server 2012(64비트 전용)</span><span class="sxs-lookup"><span data-stu-id="7985b-107">Windows Server 2012 (64-bit only)</span></span>
* <span data-ttu-id="7985b-108">Windows Server 2012 R2(64비트 전용)</span><span class="sxs-lookup"><span data-stu-id="7985b-108">Windows Server 2012 R2 (64-bit only)</span></span>
* <span data-ttu-id="7985b-109">Windows 10</span><span class="sxs-lookup"><span data-stu-id="7985b-109">Windows 10</span></span>

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a><span data-ttu-id="7985b-110">SSTP를 지원하는 지점 및 사이트 간 연결에 소프트웨어 VPN 클라이언트를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7985b-110">Can I use any software VPN client for Point-to-Site that supports SSTP?</span></span>

<span data-ttu-id="7985b-111">아니요.</span><span class="sxs-lookup"><span data-stu-id="7985b-111">No.</span></span> <span data-ttu-id="7985b-112">지원 제한만 toohello Windows 운영 체제 버전 위에 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-112">Support is limited only toohello Windows operating system versions listed above.</span></span>

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a><span data-ttu-id="7985b-113">지점 및 사이트 간 구성에서 VPN 클라이언트 끝점을 몇 개까지 지정할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7985b-113">How many VPN client endpoints can I have in my Point-to-Site configuration?</span></span>

<span data-ttu-id="7985b-114">지원 too128 VPN 클라이언트 toobe 수 tooconnect tooa 가상 네트워크를 hello에서 동일한 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-114">We support up too128 VPN clients toobe able tooconnect tooa virtual network at hello same time.</span></span>

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a><span data-ttu-id="7985b-115">지점 및 사이트 간 연결에 내부 PKI 루트 CA를 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7985b-115">Can I use my own internal PKI root CA for Point-to-Site connectivity?</span></span>

<span data-ttu-id="7985b-116">예.</span><span class="sxs-lookup"><span data-stu-id="7985b-116">Yes.</span></span> <span data-ttu-id="7985b-117">이전에는 자체 서명한 루트 인증서만 사용할 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-117">Previously, only self-signed root certificates could be used.</span></span> <span data-ttu-id="7985b-118">여전히 20개의 루트 인증서를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-118">You can still upload 20 root certificates.</span></span>

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a><span data-ttu-id="7985b-119">지점 및 사이트 간 기능을 사용하여 프록시와 방화벽을 트래버스할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7985b-119">Can I traverse proxies and firewalls using Point-to-Site capability?</span></span>

<span data-ttu-id="7985b-120">예.</span><span class="sxs-lookup"><span data-stu-id="7985b-120">Yes.</span></span> <span data-ttu-id="7985b-121">방화벽을 통해 tootunnel SSTP (Secure Socket Tunneling Protocol)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-121">We use SSTP (Secure Socket Tunneling Protocol) tootunnel through firewalls.</span></span> <span data-ttu-id="7985b-122">이 터널은 HTTP 연결로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-122">This tunnel will appear as an HTTPs connection.</span></span>

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a><span data-ttu-id="7985b-123">지점 및 사이트에 대해 구성 된 클라이언트 컴퓨터를 다시 시작 하는 경우 hello VPN 자동으로 다시 연결 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-123">If I restart a client computer configured for Point-to-Site, will hello VPN automatically reconnect?</span></span>

<span data-ttu-id="7985b-124">기본적으로 hello 클라이언트 컴퓨터는 다시 설정 하지 않도록 hello VPN 연결이 자동으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-124">By default, hello client computer will not reestablish hello VPN connection automatically.</span></span>

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a><span data-ttu-id="7985b-125">자동 다시 연결 지점 및 사이트 지원의 역할과에서 DDNS VPN 클라이언트 hello?</span><span class="sxs-lookup"><span data-stu-id="7985b-125">Does Point-to-Site support auto-reconnect and DDNS on hello VPN clients?</span></span>

<span data-ttu-id="7985b-126">자동 다시 연결과 DDNS는 현재 지점 및 사이트 간 VPN에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-126">Auto-reconnect and DDNS are currently not supported in Point-to-Site VPNs.</span></span>

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a><span data-ttu-id="7985b-127">사용할 수 있습니까 사이트 간 및 지점 및 사이트 간 구성이 공존할 수 hello에 대 한 동일한 가상 네트워크?</span><span class="sxs-lookup"><span data-stu-id="7985b-127">Can I have Site-to-Site and Point-to-Site configurations coexist for hello same virtual network?</span></span>

<span data-ttu-id="7985b-128">예.</span><span class="sxs-lookup"><span data-stu-id="7985b-128">Yes.</span></span> <span data-ttu-id="7985b-129">게이트웨이에 경로 기반 VPN 유형이 있는 경우 이 솔루션이 모두 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-129">Both these solutions will work if you have a RouteBased VPN type for your gateway.</span></span> <span data-ttu-id="7985b-130">Hello 클래식 배포 모델에 대 한 동적 게이트웨이가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-130">For hello classic deployment model, you need a dynamic gateway.</span></span> <span data-ttu-id="7985b-131">수행할 하지 지원 지점 및 사이트 간 게이트웨이 hello를 사용 하 여 또는 정적 라우팅 VPN 게이트웨이 대 한 `-VpnType PolicyBased` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7985b-131">We do not support Point-to-Site for static routing VPN gateways or gateways using hello `-VpnType PolicyBased` cmdlet.</span></span>

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a><span data-ttu-id="7985b-132">Hello에는 지점 및 사이트 클라이언트 tooconnect toomultiple 가상 네트워크를 구성할 수 동시?</span><span class="sxs-lookup"><span data-stu-id="7985b-132">Can I configure a Point-to-Site client tooconnect toomultiple virtual networks at hello same time?</span></span>

<span data-ttu-id="7985b-133">예, 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-133">Yes, it is possible.</span></span> <span data-ttu-id="7985b-134">하지만 hello 가상 네트워크는 겹치는 IP 접두사를 사용할 수 없습니다 및 hello 지점 및 사이트 간 주소 공간 hello 가상 네트워크 간에 겹치지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-134">But hello virtual networks cannot have overlapping IP prefixes and hello Point-to-Site address spaces must not overlap between hello virtual networks.</span></span>

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a><span data-ttu-id="7985b-135">사이트 간 연결 또는 지점 및 사이트 간 연결을 통해 어느 정도의 처리량을 제공할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="7985b-135">How much throughput can I expect through Site-to-Site or Point-to-Site connections?</span></span>

<span data-ttu-id="7985b-136">것은 어려운 toomaintain hello VPN 터널의 hello 정확한 처리량입니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-136">It's difficult toomaintain hello exact throughput of hello VPN tunnels.</span></span> <span data-ttu-id="7985b-137">IPsec과 SSTP는 암호화 중심 VPN 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-137">IPsec and SSTP are crypto-heavy VPN protocols.</span></span> <span data-ttu-id="7985b-138">또한 프레미스 및 hello 인터넷 간 대역폭과 hello 대기 시간에 처리량이 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7985b-138">Throughput is also limited by hello latency and bandwidth between your premises and hello Internet.</span></span>
