### <a name="record-names"></a>레코드 이름

Azure DNS에서는 상대 이름을 사용하여 레코드를 지정합니다. A *정규화* 도메인 이름 (FQDN)를 포함 하지만 hello 영역 이름은 *상대* 이름이 없습니다. 예를 들어 hello 상대 레코드 이름을 hello 영역 '만든 contoso.com'에서 ' w w w' hello 정규화 레코드 이름 'www.contoso.com'를 제공합니다.

*구로* 레코드는 hello 루트에 DNS 레코드 (또는 *구로*) DNS 영역입니다. 예를 들어 contoso.com' hello DNS 영역'에 루트 record도 hello 정규화 된 이름을 갖는 '만든 contoso.com' (이 라고도 *naked* 도메인).  규칙에 따라 hello 상대 이름이 ' @'가 사용 되는 toorepresent 루트 레코드입니다.

### <a name="record-types"></a>레코드 유형

각 DNS 레코드에는 이름 및 형식이 있습니다. 레코드는 포함 된 toohello 데이터에 따라 다양 한 형식으로 구성 됩니다. hello 가장 일반적인 형식이 'A' 인 레코드 이름 tooan IPv4 주소에 매핑합니다. 또 다른 일반적인 유형 이름 tooa 메일 서버에 매핑하는 'MX' 레코드입니다.

Azure DNS는 A, AAAA, CNAME, MX, NS, PTR, SOA, SRV, TXT 등 일반적인 DNS 레코드 형식을 모두 지원합니다. [SPF 레코드는 TXT 레코드를 사용하여 표현됩니다](../articles/dns/dns-zones-records.md#spf-records).

### <a name="record-sets"></a>레코드 집합

필요한 경우가 있습니다 toocreate 지정한 이름과 형식을 가진 둘 이상의 DNS 레코드. 예를 들어 hello 'www.contoso.com' 웹 사이트가 서로 다른 두 IP 주소에서 호스팅되는 가정 합니다. hello 웹 사이트의 각 IP 주소에 대 한 A 레코드에 서로 다른 두 필요합니다. 다음은 레코드 집합의 예제입니다.

    www.contoso.com.        3600    IN    A    134.170.185.46
    www.contoso.com.        3600    IN    A    134.170.188.221

Azure DNS는 *레코드 집합*을 사용하여 모든 DNS 레코드를 관리합니다. 레코드 집합 (라고도 *리소스* 레코드 집합)는 동일 이름을 지정 하 고 hello의 hello 있는 영역에서 DNS 레코드의 hello 컬렉션 동일한 형식입니다. 대부분의 레코드 집합은 단일 레코드를 포함합니다. 그러나 예와 위에서 하나 hello 같은 레코드 집합에 레코드가 여러 개 포함, 일반적이 지 않습니다.

예, hello 영역 만든 ' contoso.com'에서 이미 'w w w' A 레코드를 만든 경우를 가정해 볼 toohello IP를 가리키는 주소 '134.170.185.46' (hello 첫 번째 레코드 위의).  toocreate hello 두 번째 레코드 추가한 toohello 기존 레코드를 기록 하 추가 레코드 집합을 만들지 않고을 설정 합니다.

SOA hello 및 CNAME 레코드 종류는 예외입니다. hello DNS 표준 hello 이러한 형식에 대 한 이름과 같은 이름을 가진 여러 레코드를 허용 하지 않습니다., 따라서 이러한 레코드 집합의 단일 레코드 포함할만 있습니다.
