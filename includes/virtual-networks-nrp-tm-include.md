## <a name="traffic-manager-profile"></a><span data-ttu-id="ba26a-101">트래픽 관리자 프로필</span><span class="sxs-lookup"><span data-stu-id="ba26a-101">Traffic Manager Profile</span></span>
<span data-ttu-id="ba26a-102">트래픽 관리자와 자식 끝점 리소스는 Azure 내부와 외부의 끝점에서 DNS 라우팅을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-102">Traffic manager and its child endpoint resource enable DNS routing to endpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="ba26a-103">이러한 트래픽 배포는 라우팅 정책 방법에 의해 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="ba26a-104">또한 트래픽 관리자를 사용하여 끝점 상태를 모니터링할 수 있습니다. 트래픽은 끝점의 상태를 기반으로 적절하게 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-104">Traffic manager also allows endpoint health to be monitored, and traffic diverted appropriately based on the health of an endpoint.</span></span> 

| <span data-ttu-id="ba26a-105">자산</span><span class="sxs-lookup"><span data-stu-id="ba26a-105">Property</span></span> | <span data-ttu-id="ba26a-106">설명</span><span class="sxs-lookup"><span data-stu-id="ba26a-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba26a-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="ba26a-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="ba26a-108">가능한 값은 *성능*, *가중* 및 *우선 순위*입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="ba26a-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="ba26a-109">**dnsConfig**</span></span> |<span data-ttu-id="ba26a-110">프로필에 대한 FQDN</span><span class="sxs-lookup"><span data-stu-id="ba26a-110">FQDN for the profile</span></span> |
| <span data-ttu-id="ba26a-111">**프로토콜**</span><span class="sxs-lookup"><span data-stu-id="ba26a-111">**Protocol**</span></span> |<span data-ttu-id="ba26a-112">모니터링 프로토콜이며 가능한 값은 *HTTP* 및 *HTTPS*입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="ba26a-113">**포트**</span><span class="sxs-lookup"><span data-stu-id="ba26a-113">**Port**</span></span> |<span data-ttu-id="ba26a-114">모니터링 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-114">monitoring port</span></span> |
| <span data-ttu-id="ba26a-115">**Path**</span><span class="sxs-lookup"><span data-stu-id="ba26a-115">**Path**</span></span> |<span data-ttu-id="ba26a-116">모니터링 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-116">monitoring path</span></span> |
| <span data-ttu-id="ba26a-117">**끝점**</span><span class="sxs-lookup"><span data-stu-id="ba26a-117">**Endpoints**</span></span> |<span data-ttu-id="ba26a-118">끝점 리소스에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="ba26a-119">끝점</span><span class="sxs-lookup"><span data-stu-id="ba26a-119">Endpoint</span></span>
<span data-ttu-id="ba26a-120">끝점은 트래픽 관리자 프로필의 자식 리소스이며,</span><span class="sxs-lookup"><span data-stu-id="ba26a-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="ba26a-121">트래픽 관리자 프로필 리소스에 구성된 정책을 기반으로 사용자 트래픽이 배포되는 서비스 또는 웹 끝점을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-121">It represents a service or web endpoint to which user traffic is distributed based on the configured policy in the Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="ba26a-122">자산</span><span class="sxs-lookup"><span data-stu-id="ba26a-122">Property</span></span> | <span data-ttu-id="ba26a-123">설명</span><span class="sxs-lookup"><span data-stu-id="ba26a-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ba26a-124">**형식**</span><span class="sxs-lookup"><span data-stu-id="ba26a-124">**Type**</span></span> |<span data-ttu-id="ba26a-125">끝점의 형식이며, 가능한 값은 *Azure 끝점*, *외부 끝점* 및 *중첩된 끝점*입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-125">the type of the endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="ba26a-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="ba26a-126">**targetResourceId**</span></span> |<span data-ttu-id="ba26a-127">서비스 또는 웹 끝점의 공용 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="ba26a-128">Azure 또는 외부 끝점일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="ba26a-129">**무게**</span><span class="sxs-lookup"><span data-stu-id="ba26a-129">**Weight**</span></span> |<span data-ttu-id="ba26a-130">트래픽 관리에 사용되는 끝점 가중치입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="ba26a-131">**우선 순위**</span><span class="sxs-lookup"><span data-stu-id="ba26a-131">**Priority**</span></span> |<span data-ttu-id="ba26a-132">장애 조치(Failover) 동작을 정의하는 데 사용되는 끝점의 우선 순위입니다.</span><span class="sxs-lookup"><span data-stu-id="ba26a-132">priority of the endpoint, used to define a failover action</span></span> |

<span data-ttu-id="ba26a-133">트래픽 관리자의 Json 형식 샘플:</span><span class="sxs-lookup"><span data-stu-id="ba26a-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="ba26a-134">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="ba26a-134">Additional resources</span></span>
<span data-ttu-id="ba26a-135">자세한 내용은 [트래픽 관리자에 대한 REST API 설명서](https://msdn.microsoft.com/library/azure/mt163664.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba26a-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

