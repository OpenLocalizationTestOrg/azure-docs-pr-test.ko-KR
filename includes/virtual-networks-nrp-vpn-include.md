## <a name="vpn-gateway"></a><span data-ttu-id="987af-101">VPN 게이트웨이</span><span class="sxs-lookup"><span data-stu-id="987af-101">VPN Gateway</span></span>
<span data-ttu-id="987af-102">VPN 게이트웨이 리소스 toocreate를 자신의 온-프레미스 데이터 센터와 Azure 간에 보안 연결이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987af-102">A VPN gateway resource enables you toocreate a secure connection between their on-premises data center and Azure.</span></span> <span data-ttu-id="987af-103">다음과 같은 세 가지 방법으로 VPN 게이트웨이 리소스를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987af-103">A VPN gateway resource can be configured in three different ways:</span></span>

* <span data-ttu-id="987af-104">**지점 tooSite** – 모든 컴퓨터에서 VPN 클라이언트를 사용 하 여 VNET에서 호스트 하 여 Azure 리소스에 안전 하 게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="987af-104">**Point tooSite** – you can securely access your Azure resources hosted in a VNET by using a VPN client from any computer.</span></span> 
* <span data-ttu-id="987af-105">**다중 사이트 연결** – 안전 하 게에서 연결할 수 온-프레미스 데이터 센터 tooresources VNET에서를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="987af-105">**Multi-site connection** – you can securely connect from your on-premises data centers tooresources running in a VNET.</span></span> 
* <span data-ttu-id="987af-106">**VNET tooVNET** – 안전 하 게 연결할 수 Azure VNET에서 hello 내에서 동일한 지역 또는 지리적 중복 toobuild 작업 영역 간에 합니다.</span><span class="sxs-lookup"><span data-stu-id="987af-106">**VNET tooVNET** – you can securely connect across Azure VNETS within hello same region, or across regions toobuild workloads with geo-redundancy.</span></span>

<span data-ttu-id="987af-107">VPN 게이트웨이의 키 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="987af-107">Key properties of a VPN gateway include:</span></span>

* <span data-ttu-id="987af-108">**게이트웨이 유형** - 동적으로 라우팅되거나 정적으로 라우팅된 게이트웨이입니다.</span><span class="sxs-lookup"><span data-stu-id="987af-108">**Gateway type** - dynamically routed or a static routed gateway.</span></span> 
* <span data-ttu-id="987af-109">**VPN 클라이언트 주소 풀이 접두사** – IP 주소 할당 toobe tooclients 지점 toosite 구성에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="987af-109">**VPN Client Address Pool Prefix** – IP addresses toobe assigned tooclients connecting in a point toosite configuration.</span></span>

