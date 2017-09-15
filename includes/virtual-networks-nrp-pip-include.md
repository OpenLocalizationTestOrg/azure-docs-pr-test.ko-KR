## <a name="public-ip-address"></a><span data-ttu-id="9f2ab-101">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="9f2ab-101">Public IP address</span></span>
<span data-ttu-id="9f2ab-102">공용 IP 주소 리소스는 예약된 인터넷 연결 IP 주소 또는 동적 인터넷 연결 IP 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="9f2ab-103">독립 실행형 개체로 공용 IP 주소를 만들 수 있지만 실제로 주소를 사용하려면 다른 개체에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span></span> <span data-ttu-id="9f2ab-104">부하 분산 장치, 응용 프로그램 게이트웨이 또는 NIC에 공용 IP 주소를 연결하여 해당 리소스에 대한 인터넷 액세스를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span></span>  

| <span data-ttu-id="9f2ab-105">속성</span><span class="sxs-lookup"><span data-stu-id="9f2ab-105">Property</span></span> | <span data-ttu-id="9f2ab-106">설명</span><span class="sxs-lookup"><span data-stu-id="9f2ab-106">Description</span></span> | <span data-ttu-id="9f2ab-107">샘플 값</span><span class="sxs-lookup"><span data-stu-id="9f2ab-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f2ab-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="9f2ab-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="9f2ab-109">IP 주소가 *고정* 또는 *동적*인지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-109">Defines if the IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="9f2ab-110">고정, 동적</span><span class="sxs-lookup"><span data-stu-id="9f2ab-110">static, dynamic</span></span> |
| <span data-ttu-id="9f2ab-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="9f2ab-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="9f2ab-112">유휴 시간 초과를 정의합니다. 기본값은 4분입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-112">Defines the idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="9f2ab-113">이 시간 안에 지정된 세션에 대한 추가 패킷이 수신되지 않을 경우 세션이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-113">If no more packets for a given session is received within this time, the session is terminated.</span></span> |<span data-ttu-id="9f2ab-114">4와 30 사이의 임의 값</span><span class="sxs-lookup"><span data-stu-id="9f2ab-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="9f2ab-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="9f2ab-115">**ipAddress**</span></span> |<span data-ttu-id="9f2ab-116">개체에 할당된 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-116">IP address assigned to object.</span></span> <span data-ttu-id="9f2ab-117">읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-117">This is a read-only property.</span></span> |<span data-ttu-id="9f2ab-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="9f2ab-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="9f2ab-119">DNS 설정</span><span class="sxs-lookup"><span data-stu-id="9f2ab-119">DNS settings</span></span>
<span data-ttu-id="9f2ab-120">공용 IP 주소는 다음과 같은 속성이 포함된 **dnsSettings** 라는 자식 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span></span>

| <span data-ttu-id="9f2ab-121">속성</span><span class="sxs-lookup"><span data-stu-id="9f2ab-121">Property</span></span> | <span data-ttu-id="9f2ab-122">설명</span><span class="sxs-lookup"><span data-stu-id="9f2ab-122">Description</span></span> | <span data-ttu-id="9f2ab-123">샘플 값</span><span class="sxs-lookup"><span data-stu-id="9f2ab-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f2ab-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="9f2ab-124">**domainNameLabel**</span></span> |<span data-ttu-id="9f2ab-125">이름 확인에 사용되는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-125">Host named used for name resolution.</span></span> |<span data-ttu-id="9f2ab-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="9f2ab-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="9f2ab-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="9f2ab-127">**fqdn**</span></span> |<span data-ttu-id="9f2ab-128">공용 IP에 대한 정규화된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-128">Fully qualified name for the public IP.</span></span> |<span data-ttu-id="9f2ab-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="9f2ab-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="9f2ab-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="9f2ab-130">**reverseFqdn**</span></span> |<span data-ttu-id="9f2ab-131">IP 주소로 확인되고 DNS에 PTR 레코드로 등록되는 정규화된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="9f2ab-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-132">www.contoso.com.</span></span> |

<span data-ttu-id="9f2ab-133">JSON 형식의 샘플 공용 IP 주소:</span><span class="sxs-lookup"><span data-stu-id="9f2ab-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="9f2ab-134">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9f2ab-134">Additional resources</span></span>
* <span data-ttu-id="9f2ab-135">[공용 IP 주소](../articles/virtual-network/virtual-networks-reserved-public-ip.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="9f2ab-136">[인스턴스 수준 공용 IP](../articles/virtual-network/virtual-networks-instance-level-public-ip.md)주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="9f2ab-137">공용 IP 주소에 대한 [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163638.aspx) 를 읽으십시오.</span><span class="sxs-lookup"><span data-stu-id="9f2ab-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

