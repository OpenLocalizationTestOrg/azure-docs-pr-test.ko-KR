## <a name="public-ip-address"></a>공용 IP 주소
공용 IP 주소 리소스는 예약된 인터넷 연결 IP 주소 또는 동적 인터넷 연결 IP 주소를 제공합니다. Tooassociate 독립 실행형 개체로 공용 IP 주소를 만들 수 있지만 필요한 것 tooanother 개체 tooactually hello 주소를 사용 합니다. 공용 IP 주소 tooa 부하 분산 장치, 응용 프로그램 게이트웨이 또는 NIC tooprovide 인터넷 액세스 toothose 리소스를 연결할 수 있습니다.  

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **publicIPAllocationMethod** |Hello IP 주소가 정의 *정적* 또는 *동적*합니다. |고정, 동적 |
| **idleTimeoutInMinutes** |Hello 유휴 시간 제한, 기본값은 4 분을 정의합니다. 이 시간 내 지정된 된 세션에 대 한 더 많은 패킷이 수신 되 면 hello 세션이 종료 됩니다. |4와 30 사이의 임의 값 |
| **ipAddress** |IP 주소 할당 tooobject 합니다. 읽기 전용 속성입니다. |104.42.233.77 |

### <a name="dns-settings"></a>DNS 설정
공용 IP 주소는 명명 된 자식 개체 **dnsSettings** hello 다음과 같은 속성을 포함 합니다.

| 속성 | 설명 | 샘플 값 |
| --- | --- | --- |
| **domainNameLabel** |이름 확인에 사용되는 호스트 이름입니다. |www, ftp, vm1 |
| **fqdn** |Hello 공용 IP에 대 한 정규화 된 이름입니다. |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Toohello IP 주소를 확인 하 고 DNS PTR 레코드에 등록 하는 정규화 된 도메인 이름입니다. |www.contoso.com. |

JSON 형식의 샘플 공용 IP 주소:

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

### <a name="additional-resources"></a>추가 리소스
* [공용 IP 주소](../articles/virtual-network/virtual-networks-reserved-public-ip.md)에 대해 자세히 알아보세요.
* [인스턴스 수준 공용 IP](../articles/virtual-network/virtual-networks-instance-level-public-ip.md)주소에 대해 알아봅니다.
* 읽기 hello [REST API 참조 설명서](https://msdn.microsoft.com/library/azure/mt163638.aspx) 공용 IP 주소입니다.

