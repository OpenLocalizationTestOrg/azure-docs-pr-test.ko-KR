## <a name="load-balancer"></a><span data-ttu-id="5e81e-101">부하 분산 장치</span><span class="sxs-lookup"><span data-stu-id="5e81e-101">Load Balancer</span></span>
<span data-ttu-id="5e81e-102">부하 분산 장치는 tooscale 응용 프로그램을 사용할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-102">A load balancer is used when you want tooscale your applications.</span></span> <span data-ttu-id="5e81e-103">일반적인 배포 시나리오에는 여러 VM 인스턴스에서 실행 중인 응용 프로그램이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-103">Typical deployment scenarios involve applications running on multiple VM instances.</span></span> <span data-ttu-id="5e81e-104">hello VM 인스턴스는 프런트 toodistribute 네트워크 트래픽 toohello 다양 한 인스턴스 도움이 되는 부하 분산 장치를 통해.</span><span class="sxs-lookup"><span data-stu-id="5e81e-104">hello VM instances are fronted by a load balancer that helps toodistribute network traffic toohello various instances.</span></span> 

![단일 VM의 NIC](./media/resource-groups-networking/figure8.png)

| <span data-ttu-id="5e81e-106">속성</span><span class="sxs-lookup"><span data-stu-id="5e81e-106">Property</span></span> | <span data-ttu-id="5e81e-107">설명</span><span class="sxs-lookup"><span data-stu-id="5e81e-107">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5e81e-108">*frontendIPConfigurations*</span><span class="sxs-lookup"><span data-stu-id="5e81e-108">*frontendIPConfigurations*</span></span> |<span data-ttu-id="5e81e-109">부하 분산 장치는 하나 이상의 프런트 엔드 IP 주소(VIP(가상 IP)라고 함)를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-109">a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="5e81e-110">이러한 IP 주소 ingress hello 트래픽에 대 한 역할을 수행 하며 공용 IP 또는 개인 IP 수</span><span class="sxs-lookup"><span data-stu-id="5e81e-110">These IP addresses serve as ingress for hello traffic and can be public IP or private IP</span></span> |
| <span data-ttu-id="5e81e-111">*backendAddressPools*</span><span class="sxs-lookup"><span data-stu-id="5e81e-111">*backendAddressPools*</span></span> |<span data-ttu-id="5e81e-112">다음은 VM Nic toowhich 부하 분산 됩니다 hello와 연결 된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="5e81e-112">these are IP addresses associated with hello VM NICs toowhich load will be distributed</span></span> |
| <span data-ttu-id="5e81e-113">*loadBalancingRules*</span><span class="sxs-lookup"><span data-stu-id="5e81e-113">*loadBalancingRules*</span></span> |<span data-ttu-id="5e81e-114">규칙 속성에 지정 된 프런트 엔드 IP 매핑합니다 조합 포트 및 포트 조합 tooa 백 엔드 IP 주소 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-114">a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="5e81e-115">부하 분산 장치 리소스의 단일 정의를 사용하여 각각 가상 컴퓨터에 연결된 프런트 엔드 IP와 포트 및 백 엔드 IP와 포트 조합을 반영하는 여러 부하 분산 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-115">With a single definition of a load balancer resource, you can define multiple load balancing rules, each rule reflecting a combination of a front end IP and port and back end IP and port associated with virtual machines.</span></span> <span data-ttu-id="5e81e-116">hello 규칙은 하나의 포트 hello 백 엔드 풀의 hello 프런트 엔드 풀 toomany 가상 컴퓨터에서</span><span class="sxs-lookup"><span data-stu-id="5e81e-116">hello rule is one port in hello front end pool toomany virtual machines in hello back end pool</span></span> |
| <span data-ttu-id="5e81e-117">*프로브*</span><span class="sxs-lookup"><span data-stu-id="5e81e-117">*Probes*</span></span> |<span data-ttu-id="5e81e-118">프로브를 사용 하면 tookeep VM 인스턴스의 hello 상태를 추적 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-118">probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="5e81e-119">상태 검색이 실패 하면 가상 컴퓨터 인스턴스에 hello 수행 될 순환 순서에서 자동으로</span><span class="sxs-lookup"><span data-stu-id="5e81e-119">If a health probe fails, hello virtual machine instance will be taken out of rotation automatically</span></span> |
| <span data-ttu-id="5e81e-120">*inboundNatRules*</span><span class="sxs-lookup"><span data-stu-id="5e81e-120">*inboundNatRules*</span></span> |<span data-ttu-id="5e81e-121">Hello를 정의 하는 NAT 규칙 hello 프런트 엔드 IP를 통해 흐르는 트래픽 인바운드 및 toohello 백 엔드 IP tooa 특정 가상 컴퓨터 인스턴스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e81e-121">NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP tooa specific virtual machine instance.</span></span> <span data-ttu-id="5e81e-122">NAT 규칙은 하나의 포트 hello 백 엔드 풀의 hello 프런트 엔드 풀 tooone 가상 컴퓨터에</span><span class="sxs-lookup"><span data-stu-id="5e81e-122">NAT rule is one port in hello front end pool tooone virtual machine in hello back end pool</span></span> |

<span data-ttu-id="5e81e-123">Json 형식의 부하 분산 장치 템플릿 예:</span><span class="sxs-lookup"><span data-stu-id="5e81e-123">Example of load balancer template in Json format:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "dnsNameforLBIP": {
          "type": "string",
          "metadata": {
            "description": "Unique DNS name"
          }
        },
        "location": {
          "type": "string",
          "allowedValues": [
            "East US",
            "West US",
            "West Europe",
            "East Asia",
            "Southeast Asia"
          ],
          "metadata": {
            "description": "Location toodeploy"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address Prefix"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/24",
          "metadata": {
            "description": "Subnet Prefix"
          }
        },
        "publicIPAddressType": {
          "type": "string",
          "defaultValue": "Dynamic",
          "allowedValues": [
            "Dynamic",
            "Static"
          ],
          "metadata": {
            "description": "Public IP type"
          }
        }
      },
      "variables": {
        "virtualNetworkName": "virtualNetwork1",
        "publicIPAddressName": "publicIp1",
        "subnetName": "subnet1",
        "loadBalancerName": "loadBalancer1",
        "nicName": "networkInterface1",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
        "nicId": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
        "backEndIPConfigID": "[concat(variables('nicId'),'/ipConfigurations/ipconfig1')]"
      },
      "resources": [
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[parameters('location')]",
      "properties": {
        "publicIPAllocationMethod": "[parameters('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsNameforLBIP')]"
        }
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[parameters('location')]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[parameters('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[parameters('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "subnet": {
                "id": "[variables('subnetRef')]"
              },
              "loadBalancerBackendAddressPools": [
                {
                  "id": "[concat(variables('lbID'), '/backendAddressPools/LoadBalancerBackend')]"
                }
              ],
              "loadBalancerInboundNatRules": [
                {
                  "id": "[concat(variables('lbID'),'/inboundNatRules/RDP')]"
                }
              ]
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-05-01-preview",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[parameters('location')]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[variables('publicIPAddressID')]"
              }
            }
          }
        ],
        "backendAddressPools": [
          {
            "name": "loadBalancerBackEnd"
          }
        ],
        "inboundNatRules": [
          {
            "name": "RDP",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPort": 3389,
              "backendPort": 3389,
              "enableFloatingIP": false
            }
          }
        ]
      }
    }
      ]
    }

### <a name="additional-resources"></a><span data-ttu-id="5e81e-124">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="5e81e-124">Additional resources</span></span>
<span data-ttu-id="5e81e-125">자세한 내용은 [부하 분산 장치 REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5e81e-125">Read [load balancer REST API](https://msdn.microsoft.com/library/azure/mt163651.aspx) for more information.</span></span>

