## <a name="public-ip-address"></a><span data-ttu-id="f6fbe-101">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="f6fbe-101">Public IP address</span></span>
<span data-ttu-id="f6fbe-102">공용 IP 주소 리소스는 예약된 인터넷 연결 IP 주소 또는 동적 인터넷 연결 IP 주소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="f6fbe-103">Tooassociate 독립 실행형 개체로 공용 IP 주소를 만들 수 있지만 필요한 것 tooanother 개체 tooactually hello 주소를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="f6fbe-104">공용 IP 주소 tooa 부하 분산 장치, 응용 프로그램 게이트웨이 또는 NIC tooprovide 인터넷 액세스 toothose 리소스를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="f6fbe-105">속성</span><span class="sxs-lookup"><span data-stu-id="f6fbe-105">Property</span></span> | <span data-ttu-id="f6fbe-106">설명</span><span class="sxs-lookup"><span data-stu-id="f6fbe-106">Description</span></span> | <span data-ttu-id="f6fbe-107">샘플 값</span><span class="sxs-lookup"><span data-stu-id="f6fbe-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6fbe-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="f6fbe-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="f6fbe-109">Hello IP 주소가 정의 *정적* 또는 *동적*합니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="f6fbe-110">고정, 동적</span><span class="sxs-lookup"><span data-stu-id="f6fbe-110">static, dynamic</span></span> |
| <span data-ttu-id="f6fbe-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="f6fbe-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="f6fbe-112">Hello 유휴 시간 제한, 기본값은 4 분을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="f6fbe-113">이 시간 내 지정된 된 세션에 대 한 더 많은 패킷이 수신 되 면 hello 세션이 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="f6fbe-114">4와 30 사이의 임의 값</span><span class="sxs-lookup"><span data-stu-id="f6fbe-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="f6fbe-115">**ipAddress**</span><span class="sxs-lookup"><span data-stu-id="f6fbe-115">**ipAddress**</span></span> |<span data-ttu-id="f6fbe-116">IP 주소 할당 tooobject 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-116">IP address assigned tooobject.</span></span> <span data-ttu-id="f6fbe-117">읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-117">This is a read-only property.</span></span> |<span data-ttu-id="f6fbe-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="f6fbe-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="f6fbe-119">DNS 설정</span><span class="sxs-lookup"><span data-stu-id="f6fbe-119">DNS settings</span></span>
<span data-ttu-id="f6fbe-120">공용 IP 주소는 명명 된 자식 개체 **dnsSettings** hello 다음과 같은 속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="f6fbe-121">속성</span><span class="sxs-lookup"><span data-stu-id="f6fbe-121">Property</span></span> | <span data-ttu-id="f6fbe-122">설명</span><span class="sxs-lookup"><span data-stu-id="f6fbe-122">Description</span></span> | <span data-ttu-id="f6fbe-123">샘플 값</span><span class="sxs-lookup"><span data-stu-id="f6fbe-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f6fbe-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="f6fbe-124">**domainNameLabel**</span></span> |<span data-ttu-id="f6fbe-125">이름 확인에 사용되는 호스트 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-125">Host named used for name resolution.</span></span> |<span data-ttu-id="f6fbe-126">www, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="f6fbe-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="f6fbe-127">**fqdn**</span><span class="sxs-lookup"><span data-stu-id="f6fbe-127">**fqdn**</span></span> |<span data-ttu-id="f6fbe-128">Hello 공용 IP에 대 한 정규화 된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="f6fbe-129">www.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="f6fbe-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="f6fbe-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="f6fbe-130">**reverseFqdn**</span></span> |<span data-ttu-id="f6fbe-131">Toohello IP 주소를 확인 하 고 DNS PTR 레코드에 등록 하는 정규화 된 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="f6fbe-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-132">www.contoso.com.</span></span> |

<span data-ttu-id="f6fbe-133">JSON 형식의 샘플 공용 IP 주소:</span><span class="sxs-lookup"><span data-stu-id="f6fbe-133">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="f6fbe-134">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="f6fbe-134">Additional resources</span></span>
* <span data-ttu-id="f6fbe-135">[공용 IP 주소](../articles/virtual-network/virtual-networks-reserved-public-ip.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="f6fbe-136">[인스턴스 수준 공용 IP](../articles/virtual-network/virtual-networks-instance-level-public-ip.md)주소에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="f6fbe-137">읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163638.aspx) 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="f6fbe-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

