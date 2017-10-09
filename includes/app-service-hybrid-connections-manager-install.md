
1. <span data-ttu-id="c40f9-101">Hello에 **하이브리드 연결** 블레이드에서 만들어지면 방금 hello 하이브리드 연결을 클릭 한 다음 클릭 **수신기 설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-101">In hello **Hybrid connections** blade, click hello hybrid connection you just created, then click **Listener Setup**.</span></span>
   
    ![수신기 설정 클릭](./media/app-service-hybrid-connections-manager-install/D04ClickListenerSetup.png)
2. <span data-ttu-id="c40f9-103">hello **하이브리드 연결 속성** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-103">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="c40f9-104">아래 **온-프레미스 하이브리드 연결 관리자**, 선택 **다운로드 하 고 수동으로 구성**다운로드 하는 hello HybridConnectionManager.msi 패키지를 저장 하 고 hello 게이트웨이 연결 문자열을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-104">Under **On-premises Hybrid Connection Manager**, choose **download and configure manually**, save hello downloaded HybridConnectionManager.msi package, and copy hello gateway connection string.</span></span>
   
    ![Tooinstall 여기를 클릭합니다](./media/app-service-hybrid-connections-manager-install/D05ClickToInstallHCM.png)
3. <span data-ttu-id="c40f9-106">관리자 명령 프롬프트에서 다음 명령 toostart hello 설치 관리자는 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-106">From an administrator command prompt, type hello following command toostart hello installer:</span></span>
   
        start HybridConnectionManager.msi
4. <span data-ttu-id="c40f9-107">Hello 설치 관리자 실행을 클릭 **나중**, 다음 toohello %ProgramFiles%\Microsoft\HybridConnectionManager 폴더를 탐색, HCMConfigWizard.exe를 실행 하 고 클릭 **예** hello에 **사용자 계정 제어** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c40f9-107">After hello installer runs, click **Not now**, then browse toohello %ProgramFiles%\Microsoft\HybridConnectionManager folder, run HCMConfigWizard.exe and click **Yes** in hello **User Account Control** dialog.</span></span>
5. <span data-ttu-id="c40f9-108">앞에서 복사한 hello 하이브리드 연결 문자열을 붙여 넣고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-108">Paste hello hybrid connection string that you copied earlier and click **OK**.</span></span> 
   
    ![설치](./media/app-service-hybrid-connections-manager-install/D08aHCMInstallManual.png)
6. <span data-ttu-id="c40f9-110">Hello 설치 완료 되 면 클릭 **닫기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-110">When hello install completes, click **Close**.</span></span>
   
    ![닫기 클릭](./media/app-service-hybrid-connections-manager-install/D09HCMInstallComplete.png)
   
    <span data-ttu-id="c40f9-112">Hello에 **하이브리드 연결** 블레이드, hello **상태** 열 이제 표시 **연결 됨**합니다.</span><span class="sxs-lookup"><span data-stu-id="c40f9-112">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![연결됨 상태](./media/app-service-hybrid-connections-manager-install/D10HCStatusConnected.png)

