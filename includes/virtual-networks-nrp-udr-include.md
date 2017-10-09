## <a name="route-tables"></a>경로 테이블
경로 테이블 리소스에 사용 된 경로 toodefine 트래픽이 Azure 인프라 내에서 어떻게 이동 하는지 포함 되어 있습니다. 사용자 정의 경로 (UDR) toosend을 특정된 서브넷 tooa 가상 어플라이언스로 (ID)는 방화벽 또는 침입 감지 시스템 등의 모든 트래픽이 사용할 수 있습니다. 경로 테이블 toosubnets를 연결할 수 있습니다. 

경로 테이블 hello 다음과 같은 속성을 포함 합니다.

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **routes** |Hello 경로 테이블의 경로 정의 하는 사용자의 컬렉션 |[사용자 정의 경로](#User-defined-routes) |
| **서브넷** |서브넷 hello 경로 테이블의 컬렉션 너무 적용|[서브넷](#Subnets) |

### <a name="user-defined-routes"></a>사용자 정의 경로
대상 주소에 기반 UDRs toospecify 트래픽를 보낼 위치를 만들 수 있습니다. Hello 기본 게이트웨이 정의 네트워크 패킷의 hello 대상 주소를 기반으로 하는 경로 생각할 수 있습니다.

UDRs hello 다음과 같은 속성을 포함 합니다. 

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **addressPrefix** |주소 접두사 또는 hello 대상에 대 한 전체 IP 주소 |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |장치 hello 트래픽 종류에는 너무에 전송 됩니다.|VirtualAppliance, VPN 게이트웨이, 인터넷 |
| **nextHopIpAddress** |다음 홉 hello에 대 한 IP 주소 |192.168.1.4 |

JSON 형식의 샘플 경로 테이블:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>추가 리소스
* [UDR](../articles/virtual-network/virtual-networks-udr-overview.md)에 대해 자세히 알아보세요.
* 읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt502549.aspx) 경로 테이블에 대 한 합니다.
* 읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt502539.aspx) 사용자에 대 한 경로 (UDRs)을 정의 합니다.

