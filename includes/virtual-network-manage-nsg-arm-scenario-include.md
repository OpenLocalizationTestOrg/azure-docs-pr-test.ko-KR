## <a name="sample-scenario"></a>샘플 시나리오
toobetter 방법을 toomanage Nsg이이 문서에서는 아래 hello 시나리오를 보여 줍니다.

![VNet 시나리오](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

이 시나리오에서는 hello에서 각 서브넷에 NSG 만들어집니다 **TestVNet** 아래에 설명 된 대로 가상 네트워크: 

* **NSG-FrontEnd**. hello 프런트 엔드 NSG 됩니다 적용된 toohello *프런트 엔드* 서브넷 하 고 두 개의 규칙 포함:    
  * **rdp-rule**. 이 규칙을 사용 하면 RDP 트래픽 toohello *프런트 엔드* 서브넷입니다.
  * **web-rule**. 이 규칙을 사용 하면 HTTP 트래픽을 toohello *프런트 엔드* 서브넷입니다.
* **NSG-BackEnd**. hello 백 엔드 NSG에는 적용 된 toohello 됩니다 *백 엔드* 서브넷 하 고 두 개의 규칙 포함:    
  * **sql-rule**. 이 규칙은 SQL 트래픽을 hello 에서만에서 허용 *프런트 엔드* 서브넷입니다.
  * **web-rule**. 이 규칙 거부 hello에서 모든 인터넷 바운드 트래픽은 *백 엔드* 서브넷입니다.

이러한 규칙의 hello 조합 만들기는 DMZ와 비슷한 시나리오 hello 백 엔드 서브넷 hello 프런트 엔드 서브넷에서 SQL 트래픽에 대 한 들어오는 트래픽의 받을 수 없는 액세스 toohello 인터넷에는 hello 프런트 엔드 서브넷 hello와 통신할 수 있지만 인터넷, 들어오는 HTTP 요청을 수신 하 고 있습니다.

위에서 설명한 toodeploy hello 시나리오에 따라 [이 링크](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), 클릭 **tooAzure 배포**hello 기본 매개 변수 값, 필요한 경우 바꾼 hello 포털의 hello 지침을 따릅니다. Hello 샘플 지침 hello 템플릿 아래에 설명 된 사용 되는 toodeploy 리소스 그룹 이름 **RG NSG**합니다. 

