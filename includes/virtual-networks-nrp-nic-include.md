## <a name="nic"></a>NIC
네트워크 인터페이스 카드 (NIC) 리소스 VNet 리소스의 네트워크 연결 tooan 기존 서브넷을 제공합니다. Tooassociate 독립 실행형 개체로 NIC를 만들 수 있지만 필요한 것 tooanother 개체 tooactually 연결을 제공 합니다. NIC VM tooa 서브넷, 공용 IP 주소 또는 부하 분산 장치 사용된 tooconnect를 수 있습니다.  

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **virtualMachine** |VM hello NIC에 연결 된입니다. |/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1 |
| **macAddress** |NIC hello에 대 한 MAC 주소 |4와 30 사이의 임의 값 |
| **networkSecurityGroup** |연결 된 NSG toohello NIC |/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1 |
| **dnsSettings** |NIC hello에 대 한 DNS 설정 |[PIP](#Public-IP-address) |

네트워크 인터페이스 카드 또는 NIC를 관련된 tooa 가상 컴퓨터 (VM) 일 수 있는 네트워크 인터페이스를 나타냅니다. VM은 NIC를 하나 이상 포함할 수 있습니다.

![단일 VM의 NIC](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a>IP 구성
Nic가 명명 된 자식 개체 **ipConfigurations** hello 다음과 같은 속성을 포함 합니다.

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **subnet** |서브넷 hello NIC에 연결 됩니다. |/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1 |
| **privateIPAddress** |Hello 서브넷의 NIC hello에 대 한 IP 주소 |10.0.0.8 |
| **privateIPAllocationMethod** |IP 할당 방법 |동적 또는 정적 |
| **enableIPForwarding** |라우팅에 대 한 hello NIC를 사용할 수 있는지 여부 |true 또는 false |
| **primary** |Hello NIC 인지 hello hello VM에 대 한 기본 NIC |true 또는 false |
| **publicIPAddress** |Hello NIC와 관련 된 PIP |[DNS 설정](#DNS-settings) |
| **loadBalancerBackendAddressPools** |끝 주소 풀 hello NIC와 연결 된 백업 | |
| **loadBalancerInboundNatRules** |부하 분산 장치 NAT 규칙 hello NIC와 연결 된 인바운드 | |

JSON 형식의 샘플 공용 IP 주소:

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a>추가 리소스
* 읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163579.aspx) Nic에 대 한 합니다.

