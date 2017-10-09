## <a name="vpn-gateway"></a>VPN 게이트웨이
VPN 게이트웨이 리소스 toocreate를 자신의 온-프레미스 데이터 센터와 Azure 간에 보안 연결이 있습니다. 다음과 같은 세 가지 방법으로 VPN 게이트웨이 리소스를 구성할 수 있습니다.

* **지점 tooSite** – 모든 컴퓨터에서 VPN 클라이언트를 사용 하 여 VNET에서 호스트 하 여 Azure 리소스에 안전 하 게 액세스할 수 있습니다. 
* **다중 사이트 연결** – 안전 하 게에서 연결할 수 온-프레미스 데이터 센터 tooresources VNET에서를 실행 합니다. 
* **VNET tooVNET** – 안전 하 게 연결할 수 Azure VNET에서 hello 내에서 동일한 지역 또는 지리적 중복 toobuild 작업 영역 간에 합니다.

VPN 게이트웨이의 키 속성은 다음과 같습니다.

* **게이트웨이 유형** - 동적으로 라우팅되거나 정적으로 라우팅된 게이트웨이입니다. 
* **VPN 클라이언트 주소 풀이 접두사** – IP 주소 할당 toobe tooclients 지점 toosite 구성에 연결 합니다.

