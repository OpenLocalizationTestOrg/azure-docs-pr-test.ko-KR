## <a name="network-security-group"></a>네트워크 보안 그룹
NSG 리소스 작업에 대 한 보안 경계 hello 만들 수 있음, 구현 하 여 허용 및 거부 규칙입니다. 이러한 규칙 될 수 있습니다 tooa VM, 서브넷 또는 NIC를 적용 합니다.

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **서브넷** |서브넷 id hello NSG의 목록에 적용 됩니다. |/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd |
| **securityRules** |Hello NSG 구성 하는 보안 규칙의 목록 |아래 [보안 규칙](#Security-rule) 참조 |
| **defaultSecurityRules** |모든 NSG에 있는 기본 보안 규칙 목록 |아래 [기본 보안 규칙](#Default-security-rules) 참조 |

* **보안 규칙** - NSG에 대해 여러 보안 규칙을 정의할 수 있습니다. 각 규칙은 서로 다른 유형의 트래픽을 허용하거나 거부할 수 있습니다.

### <a name="security-rule"></a>보안 규칙
보안 규칙은 nsg 아래의 hello 속성을 포함 하는 자식 리소스입니다.

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **description** |Hello 규칙에 대 한 설명 |서브넷 X에서 모든 VM에 인바운드 트래픽 허용 |
| **protocol** |Hello 규칙에 대 한 프로토콜 toomatch |TCP, UDP, 또는 * |
| **sourcePortRange** |원본 포트 범위 toomatch hello 규칙에 대 한 |80, 100-200, * |
| **destinationPortRange** |대상 포트 범위 toomatch hello 규칙에 대 한 |80, 100-200, * |
| **sourceAddressPrefix** |소스 주소 접두사 toomatch hello 규칙에 대 한 |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |대상 주소 접두사 toomatch hello 규칙에 대 한 |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **direction** |Hello 규칙에 대 한 트래픽 toomatch의 방향 |인바운드 또는 아웃바운드 |
| **우선 순위** |Hello 규칙에 대 한 우선 순위입니다. 규칙은 우선 순위대로 검사되고, 규칙이 적용된 후에는 일치 여부를 알기 위해 규칙이 더 이상 테스트되지 않습니다. |10, 100, 65000 |
| **access** |유형의 액세스 tooapply hello 규칙과 일치 하는 경우 |허용 또는 거부 |

JSON 형식의 샘플 NSG:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>기본 보안 규칙

기본 보안 규칙 hello는 보안 규칙에서 사용할 수 있는 동일한 속성이 있습니다. 이러한 적용할 Nsg toothem 않은 리소스 간의 기본 연결 tooprovide 존재 합니다. 어떤 [기본 보안 규칙](../articles/virtual-network/virtual-networks-nsg.md#default-rules) 이 있는지 알아야 합니다.

### <a name="additional-resources"></a>추가 리소스
* [NSG](../articles/virtual-network/virtual-networks-nsg.md)에 대한 자세한 정보를 참조하세요.
* 읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163615.aspx) Nsg에 대 한 합니다.
* 읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163580.aspx) 보안 규칙에 대 한 합니다.
