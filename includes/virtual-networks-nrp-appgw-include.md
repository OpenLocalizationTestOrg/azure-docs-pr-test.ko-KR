## <a name="application-gateway"></a><span data-ttu-id="9e5c8-101">응용 프로그램 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="9e5c8-101">Application Gateway</span></span>
<span data-ttu-id="9e5c8-102">응용 프로그램 게이트웨이는 레이어 7 부하 분산에 기반을 둔 Azure-관리 HTTP 부하 분산 솔루션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-102">Application Gateway provides an Azure-managed HTTP load balancing solution based on layer 7 load balancing.</span></span> <span data-ttu-id="9e5c8-103">응용 프로그램 부하 분산 HTTP 기반 네트워크 트래픽에 대 한 라우팅 규칙의 hello 사용할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-103">Application load balancing allows hello use of routing rules for network traffic based on HTTP.</span></span> 
<BR>

| <span data-ttu-id="9e5c8-104">속성</span><span class="sxs-lookup"><span data-stu-id="9e5c8-104">Property</span></span> | <span data-ttu-id="9e5c8-105">설명</span><span class="sxs-lookup"><span data-stu-id="9e5c8-105">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9e5c8-106">**backendAddressPools**</span><span class="sxs-lookup"><span data-stu-id="9e5c8-106">**backendAddressPools**</span></span> |<span data-ttu-id="9e5c8-107">hello 목록 hello 백 엔드 서버의 IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-107">hello list of IP addresses of hello back end servers.</span></span> <span data-ttu-id="9e5c8-108">나열 된 IP 주소를 hello toohello 가상 네트워크 서브넷에 속해야 하거나 또는 공용 VIP/IP 또는 개인 IP 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-108">hello IP addresses listed should either belong toohello virtual network subnet, or should be a public IP/VIP or private IP</span></span> |
| <span data-ttu-id="9e5c8-109">**backendHttpSettingsCollection**</span><span class="sxs-lookup"><span data-stu-id="9e5c8-109">**backendHttpSettingsCollection**</span></span> |<span data-ttu-id="9e5c8-110">모든 풀에는 포트, 프로토콜, 쿠키 기반 선호도와 같은 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-110">Every pool has settings like port, protocol, and cookie based affinity.</span></span> <span data-ttu-id="9e5c8-111">이러한 설정은 동률된 tooa 풀 및 hello 풀 내에서 적용 된 tooall 서버</span><span class="sxs-lookup"><span data-stu-id="9e5c8-111">These settings are tied tooa pool and are applied tooall servers within hello pool</span></span> |
| <span data-ttu-id="9e5c8-112">**frontendPorts**</span><span class="sxs-lookup"><span data-stu-id="9e5c8-112">**frontendPorts**</span></span> |<span data-ttu-id="9e5c8-113">이 포트는 hello 응용 프로그램 게이트웨이에서 열린 hello 공용 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-113">This port is hello public port opened on hello application gateway.</span></span> <span data-ttu-id="9e5c8-114">트래픽이이 포트에 도달 하 고 가져옵니다 리디렉션됩니다 tooone hello 백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="9e5c8-114">Traffic hits this port, and then gets redirected tooone of hello back end servers</span></span> |
| <span data-ttu-id="9e5c8-115">**httpListeners**</span><span class="sxs-lookup"><span data-stu-id="9e5c8-115">**httpListeners**</span></span> |<span data-ttu-id="9e5c8-116">수신기에 프런트 엔드 포트, 프로토콜 (Http 또는 Https의 경우,이 대/소문자 구분), 및 hello SSL 인증서 이름 (오프 로드 SSL 구성) 하는 경우</span><span class="sxs-lookup"><span data-stu-id="9e5c8-116">Listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and hello SSL certificate name (if configuring SSL offload)</span></span> |
| <span data-ttu-id="9e5c8-117">**requestRoutingRules**</span><span class="sxs-lookup"><span data-stu-id="9e5c8-117">**requestRoutingRules**</span></span> |<span data-ttu-id="9e5c8-118">hello 규칙 hello 수신기 및 hello 백 엔드 서버 풀을 바인딩하고 백 엔드 풀 서버 hello 트래픽을 디렉션할 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-118">hello rule binds hello listener and hello back end server pool and defines which back end server pool hello traffic should be directed.</span></span> <span data-ttu-id="9e5c8-119">현재 라운드 로빈 방식으로만 작동</span><span class="sxs-lookup"><span data-stu-id="9e5c8-119">Currently works only as Round-robin</span></span> |

<span data-ttu-id="9e5c8-120">응용 프로그램 게이트웨이 JSON 템플릿의 예제:</span><span class="sxs-lookup"><span data-stu-id="9e5c8-120">Example of an application gateway Json template:</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "location": {
          "type": "string",
          "metadata": {
            "description": "Location toodeploy to"
          }
        },
        "addressPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/16",
          "metadata": {
            "description": "Address prefix for hello Virtual Network"
          }
        },
        "subnetPrefix": {
          "type": "string",
          "defaultValue": "10.0.0.0/28",
          "metadata": {
            "description": "Subnet prefix"
          }
        },
        "skuName": {
          "type": "string",
          "allowedValues": [
            "Standard_Small",
            "Standard_Medium",
            "Standard_Large"
          ],
          "defaultValue": "Standard_Medium",
          "metadata": {
            "description": "Sku Name"
          }
        },
        "capacity": {
          "type": "int",
          "defaultValue": 2,
          "metadata": {
            "description": "Number of instances"
          }
        },
        "backendIpAddress1": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 1"
          }
        },
        "backendIpAddress2": {
          "type": "string",
          "metadata": {
            "description": "IP Address for Backend Server 2"
          }
        }
      },
      "variables": {
        "applicationGatewayName": "applicationGateway1",
        "publicIPAddressName": "publicIp1",
        "virtualNetworkName": "virtualNetwork1",
        "subnetName": "appGatewaySubnet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]",
        "publicIPRef": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]",
        "applicationGatewayID": "[resourceId('Microsoft.Network/applicationGateways',variables('applicationGatewayName'))]",
        "apiVersion": "2015-05-01-preview"
      },
      "resources": [
        {
          "apiVersion": "[variables('apiVersion')]",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "[variables('publicIPAddressName')]",
          "location": "[parameters('location')]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic"
          }
        },
        {
          "apiVersion": "[variables('apiVersion')]",
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
          "apiVersion": "[variables('apiVersion')]",
          "name": "[variables('applicationGatewayName')]",
          "type": "Microsoft.Network/applicationGateways",
          "location": "[parameters('location')]",
          "dependsOn": [
            "[concat('Microsoft.Network/virtualNetworks/', variables    ('virtualNetworkName'))]",
            "[concat('Microsoft.Network/publicIPAddresses/', variables    ('publicIPAddressName'))]"
          ],
          "properties": {
            "sku": {
              "name": "[parameters('skuName')]",
              "tier": "Standard",
              "capacity": "[parameters('capacity')]"
            },
            "gatewayIPConfigurations": [
              {
                "name": "appGatewayIpConfig",
                "properties": {
                  "subnet": {
                    "id": "[variables('subnetRef')]"
                  }
                }
              }
            ],
            "frontendIPConfigurations": [
              {
                "name": "appGatewayFrontendIP",
                "properties": {
                  "PublicIPAddress": {
                    "id": "[variables('publicIPRef')]"
                  }
                }
              }
            ],
            "frontendPorts": [
              {
                "name": "appGatewayFrontendPort",
                "properties": {
                  "Port": 80
                }
              }
            ],
            "backendAddressPools": [
              {
                "name": "appGatewayBackendPool",
                "properties": {
                  "BackendAddresses": [
                    {
                      "IpAddress": "[parameters('backendIpAddress1')]"
                    },
                    {
                      "IpAddress": "[parameters('backendIpAddress2')]"
                    }
                  ]
                }
              }
            ],
            "backendHttpSettingsCollection": [
              {
                "name": "appGatewayBackendHttpSettings",
                "properties": {
                  "Port": 80,
                  "Protocol": "Http",
                  "CookieBasedAffinity": "Disabled"
                }
              }
            ],
            "httpListeners": [
              {
                "name": "appGatewayHttpListener",
                "properties": {
                  "FrontendIPConfiguration": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendIPConfigurations/appGatewayFrontendIP')]"
                  },
                  "FrontendPort": {
                    "Id": "[concat(variables('applicationGatewayID'), '/    frontendPorts/appGatewayFrontendPort')]"
                  },
                  "Protocol": "Http",
                  "SslCertificate": null
                }
              }
            ],
            "requestRoutingRules": [
              {
                "Name": "rule1",
                "properties": {
                  "RuleType": "Basic",
                  "httpListener": {
                    "id": "[concat(variables('applicationGatewayID'), '/    httpListeners/appGatewayHttpListener')]"
                  },
                  "backendAddressPool": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendAddressPools/appGatewayBackendPool')]"
                  },
                  "backendHttpSettings": {
                    "id": "[concat(variables('applicationGatewayID'), '/    backendHttpSettingsCollection/    appGatewayBackendHttpSettings')]"
                  }
                }
              }
            ]
          }
        }
      ]    
    }


### <a name="additional-resources"></a><span data-ttu-id="9e5c8-121">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="9e5c8-121">Additional resources</span></span>
<span data-ttu-id="9e5c8-122">자세한 내용은 [ 응용 프로그램 게이트웨이 REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9e5c8-122">Read [ application gateway REST API](https://msdn.microsoft.com/library/azure/mt299388.aspx) for more information.</span></span>

