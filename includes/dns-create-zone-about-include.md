DNS 영역에는 특정 도메인에 대 한 사용 되는 toohost hello DNS 레코드입니다. Azure DNS에서 도메인 호스팅 toostart toocreate DNS 영역 해당 도메인 이름을 사용 해야 합니다. 그러면 이 DNS 영역 안에 도메인의 각 DNS 레코드가 생성됩니다.

예를 들어 contoso.com' hello 도메인' 예: (메일 서버)에 대 한 ' mail.contoso.com' 및 'www.contoso.com' (웹 사이트)에 대 한 여러 DNS 레코드를 포함할 수 있습니다.

Azure DNS에서 DNS 영역을 만드는 경우:

* hello 영역의 hello 이름을 hello 리소스 그룹 내에서 고유 해야 합니다. 및 hello 영역 이미 존재 하지 않아야 합니다. 그렇지 않으면 hello 작업이 실패합니다.
* hello 영역 이름이 같은 다른 리소스 그룹 또는 다른 Azure 구독을 다시 사용할 수 있습니다.
* 여러 영역을 공유 hello 이름이 같은 각 인스턴스 주소에 할당 되어 다른 이름 서버입니다. 주소 집합을 하나만 hello 도메인 이름 등록 기관으로 구성할 수 있습니다.

> [!NOTE]
> 않아도 tooown 도메인 이름 toocreate 해당 도메인 이름 사용 하 여 DNS 영역을 Azure DNS에 있습니다. 그러나 hello 도메인 이름 등록 기관에 도메인 이름 hello에 대 한 올바른 이름 서버 hello 대로 tooown hello 도메인 tooconfigure hello Azure DNS 이름 서버 필요지 않습니다.
> 
> 자세한 내용은 참조 [도메인 tooAzure DNS 위임](../articles/dns/dns-domain-delegation.md)합니다.
