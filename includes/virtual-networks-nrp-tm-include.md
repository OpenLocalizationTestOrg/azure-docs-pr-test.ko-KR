## <a name="traffic-manager-profile"></a>트래픽 관리자 프로필
트래픽 관리자 및 해당 자식 끝점 리소스 DNS 라우팅 tooendpoints azure에서 및 Azure 외부에서 사용 하도록 설정 합니다. 이러한 트래픽 배포는 라우팅 정책 방법에 의해 제어됩니다. 트래픽 관리자 끝점 상태 toobe 지속적으로 모니터링 하 고 끝점의 hello 상태를 기반으로 적절 하 게 전달 하는 트래픽을 수도 있습니다. 

| 속성 | 설명 |
| --- | --- |
| **trafficRoutingMethod** |가능한 값은 *성능*, *가중* 및 *우선 순위*입니다. |
| **dnsConfig** |Hello 프로필에 대 한 FQDN |
| **프로토콜** |모니터링 프로토콜이며 가능한 값은 *HTTP* 및 *HTTPS*입니다. |
| **포트** |모니터링 포트입니다. |
| **Path** |모니터링 경로입니다. |
| **끝점** |끝점 리소스에 대한 컨테이너입니다. |

### <a name="endpoint"></a>끝점
끝점은 트래픽 관리자 프로필의 자식 리소스이며, 서비스를 나타냅니다 또는 웹 끝점 toowhich 사용자 트래픽이 트래픽 관리자 프로필 리소스 hello에서 구성 하는 hello 정책을 기반으로 배포 됩니다. 

| 속성 | 설명 |
| --- | --- |
| **형식** |형식 hello hello 끝점의 가능한 값은 *Azure 끝점*, *외부 끝점*, 및 *중첩 끝점* |
| **targetResourceId** |서비스 또는 웹 끝점의 공용 IP 주소입니다. Azure 또는 외부 끝점일 수 있습니다. |
| **무게** |트래픽 관리에 사용되는 끝점 가중치입니다. |
| **우선 순위** |hello 끝점에 사용 되는 toodefine 장애 조치 작업의 우선 순위 |

트래픽 관리자의 Json 형식 샘플: 

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


## <a name="additional-resources"></a>추가 리소스
자세한 내용은 [트래픽 관리자에 대한 REST API 설명서](https://msdn.microsoft.com/library/azure/mt163664.aspx) 를 참조하세요.

