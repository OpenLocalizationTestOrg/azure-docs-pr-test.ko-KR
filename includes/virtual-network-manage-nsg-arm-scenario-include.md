## <a name="sample-scenario"></a>샘플 시나리오
NSG를 관리하는 방법을 보다 잘 설명하기 위해 이 문서에서는 아래 시나리오를 사용합니다.

![VNet 시나리오](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

이 시나리오에서는 아래에 설명된 대로 **TestVNet** 가상 네트워크의 각 서브넷에 대한 NSG를 만듭니다. 

* **NSG-FrontEnd**. 프런트 엔드 NSG는 *FrontEnd* 서브넷에 적용되며 다음 두 개의 규칙을 포함합니다.    
  * **rdp-rule**. 이 규칙은 *FrontEnd* 서브넷에 대한 RDP 트래픽을 허용합니다.
  * **web-rule**. 이 규칙은 *FrontEnd* 서브넷에 대한 HTTP 트래픽을 허용합니다.
* **NSG-BackEnd**. 백 엔드 NSG는 *BackEnd* 서브넷에 적용되며 다음 두 개의 규칙을 포함합니다.    
  * **sql-rule**. 이 규칙은 *FrontEnd* 서브넷의 SQL 트래픽만 허용합니다.
  * **web-rule**. 이 규칙은 *BackEnd* 서브넷의 모든 인터넷 바인딩된 트래픽을 거부합니다.

이러한 규칙의 조합은 DMZ와 비슷한 시나리오를 만듭니다. 이 경우 백 엔드 서브넷은 프런트 엔드 서브넷의 SQL 트래픽에 대해 들어오는 트래픽만 수신할 수 있고 인터넷에 액세스할 수 없는 반면 프런트 엔드 서브넷은 인터넷과 통신하고 들어오는 HTTP 요청만 수신할 수 있습니다.

위에 설명된 시나리오를 배포하려면 [이 링크](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG)에 따라 **Azure에 배포**를 클릭하고 필요한 경우 기본 매개 변수 값을 대체하고 포털의 지침을 따릅니다. 아래 샘플 지침에서는 리소스 그룹 이름 **RG-NSG**를 배포하는 데 템플릿을 사용했습니다. 

