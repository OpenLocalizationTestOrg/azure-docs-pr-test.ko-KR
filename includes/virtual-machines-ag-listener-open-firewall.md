<span data-ttu-id="dd426-101">이 단계에서는 다른 및 hello 부하 분산 끝점 (이전에 지정 된 대로: 59999)에 대 한 방화벽 규칙 tooopen hello 프로브 포트를 만들 tooopen hello 가용성 그룹 수신기 포트 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-101">In this step, you create a firewall rule tooopen hello probe port for hello load-balanced endpoint (59999, as specified earlier) and another rule tooopen hello availability group listener port.</span></span> <span data-ttu-id="dd426-102">Tooopen hello 프로브 포트와 수신기 포트 hello에 hello 필요한 hello 가용성 그룹 복제본이 포함 된 Vm에 hello 부하 분산 된 끝점을 만든 때문에 해당 Vm입니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-102">Because you created hello load-balanced endpoint on hello VMs that contain availability group replicas, you need tooopen hello probe port and hello listener port on hello respective VMs.</span></span>

1. <span data-ttu-id="dd426-103">복제본을 호스팅하는 VM에서 **고급 보안이 포함된 Windows 방화벽**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-103">On VMs that host replicas, start **Windows Firewall with Advanced Security**.</span></span>

2. <span data-ttu-id="dd426-104">**인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 **새 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-104">Right-click **Inbound Rules**, and then click **New Rule**.</span></span>

3. <span data-ttu-id="dd426-105">Hello에 **규칙 유형** 페이지에서 **포트**, 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-105">On hello **Rule Type** page, select **Port**, and then click **Next**.</span></span>

4. <span data-ttu-id="dd426-106">Hello에 **프로토콜 및 포트** 페이지에서 **TCP**, 형식 **59999** hello에 **특정 로컬 포트** 상자를 선택한 다음 클릭**다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-106">On hello **Protocol and Ports** page, select **TCP**, type **59999** in hello **Specific local ports** box, and then click **Next**.</span></span>

5. <span data-ttu-id="dd426-107">Hello에 **동작** 페이지에서 유지 **hello 연결 허용** 을 선택한 다음 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-107">On hello **Action** page, keep **Allow hello connection** selected, and then click **Next**.</span></span>

6. <span data-ttu-id="dd426-108">Hello에 **프로필** 페이지 hello 기본 설정을 적용 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-108">On hello **Profile** page, accept hello default settings, and then click **Next**.</span></span>

7. <span data-ttu-id="dd426-109">Hello에 **이름** 페이지 hello **이름** 텍스트 상자와 같은 규칙 이름을 지정 합니다 **항상 수신기 프로브 포트**, 클릭 하 고 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-109">On hello **Name** page, in hello **Name** text box, specify a rule name, such as **Always On Listener Probe Port**, and then click **Finish**.</span></span>

8. <span data-ttu-id="dd426-110">이전 단계 (지정 된 대로 hello 스크립트의 매개 변수 hello $EndpointPort의 앞부분에 나오는) hello 가용성 그룹 수신기 포트에 대 한 hello를 반복 하 고와 같은 적절 한 규칙 이름을 지정 합니다 **항상 수신기 포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="dd426-110">Repeat hello preceding steps for hello availability group listener port (as specified earlier in hello $EndpointPort parameter of hello script), and then specify an appropriate rule name, such as **Always On Listener Port**.</span></span>

