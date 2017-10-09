## <a name="scenario"></a>시나리오
toobetter는 toocreate Nsg이이 문서의 사용 방법 아래 hello 시나리오를 보여 줍니다.

![VNet 시나리오](./media/virtual-networks-create-nsg-scenario-include/figure1.png)

이 시나리오에서는 hello에서 각 서브넷에 NSG 만들어집니다 **TestVNet** 아래에 설명 된 대로 가상 네트워크: 

* **NSG-FrontEnd**. hello 프런트 엔드 NSG 됩니다 적용된 toohello *프런트 엔드* 서브넷 하 고 두 개의 규칙 포함:    
  * **rdp-rule**. 이 규칙을 사용 하면 RDP 트래픽 toohello *프런트 엔드* 서브넷입니다.
  * **web-rule**. 이 규칙을 사용 하면 HTTP 트래픽을 toohello *프런트 엔드* 서브넷입니다.
* **NSG-BackEnd**. hello 백 엔드 NSG에는 적용 된 toohello 됩니다 *백 엔드* 서브넷 하 고 두 개의 규칙 포함:    
  * **sql-rule**. 이 규칙은 SQL 트래픽을 hello 에서만에서 허용 *프런트 엔드* 서브넷입니다.
  * **web-rule**. 이 규칙 거부 hello에서 모든 인터넷 바운드 트래픽은 *백 엔드* 서브넷입니다.

hello 이러한 규칙의 조합을 만들 여기서 hello 백 엔드 서브넷 sql hello 프런트 엔드 서브넷에서 들어오는 트래픽의 받을 수 있으며 인터넷 hello 프런트 엔드 서브넷 인터넷 hello와 통신할 수 없는 액세스 toohello, DMZ와 비슷한 시나리오 및 들어오는 HTTP 요청을 수신 합니다.

