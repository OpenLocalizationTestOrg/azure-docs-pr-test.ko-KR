## <a name="scenario"></a>시나리오
toobetter는 toocreate UDRs이이 문서의 사용 방법 아래 hello 시나리오를 보여 줍니다.

![이미지 설명](./media/virtual-network-create-udr-scenario-include/figure1.png)

이 시나리오에서는 hello에 대 한 하나의 UDR 만들어집니다 *프런트 엔드 서브넷* 및 hello에 대 한 다른 UDR *백 엔드 서브넷* 아래 설명 된 대로: 

* **UDR-FrontEnd**. hello 프런트 엔드 UDR 됩니다 적용된 toohello *프런트 엔드* 서브넷 경로 하나 포함:    
  * **RouteToBackend**. 이 경로 모든 트래픽을 toohello 백 엔드 서브넷 toohello 송신할 **FW1** 가상 컴퓨터.
* **UDR-BackEnd**. hello 백 엔드 UDR 적용된 toohello 됩니다 *백 엔드* 서브넷 하나의 경로 포함 하 고:    
  * **RouteToFrontend**. 이 경로 모든 트래픽을 toohello 프런트 엔드 서브넷 toohello 송신할 **FW1** 가상 컴퓨터.

hello 조합의 이러한 경로 하나의 서브넷 tooanother에서 전송 하는 모든 트래픽이 라우팅된 toohello 됩니다 방법을 사용 하면 **FW1** 가상 어플라이언스로 사용 되 고 있는 가상 컴퓨터. 해당 VM에 대 한 IP 전달에 tooturn 또한 해야, tooother Vm의 대상이 tooensure 트래픽을 받을 수 있습니다.

