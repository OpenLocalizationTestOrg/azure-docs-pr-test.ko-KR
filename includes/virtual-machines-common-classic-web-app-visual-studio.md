

Azure용 웹 응용 프로그램 프로젝트를 만들면 Azure에서 가상 컴퓨터를 프로비전할 수 있습니다. 추가 소프트웨어로 hello 가상 컴퓨터를 구성 하거나 hello 가상 컴퓨터 디버깅 또는 진단 목적으로 사용할 수 있습니다.

toocreate 웹 응용 프로그램을 만들 때 가상 컴퓨터는 다음이 단계를 따르십시오.

1. Visual Studio에서 클릭 **파일** > **새로** > **프로젝트** > **웹**를 선택한 후 **ASP.NET 웹 응용 프로그램** (hello 아래 **Visual C#** 또는 **Visual Basic** 노드).
2. Hello에 **새 ASP.NET 프로젝트** hello Azure hello 대화 상자 (hello 오른쪽 아래 모서리)의 섹션, 해야 해당 hello 고 원하는 웹 응용 프로그램의 대화 상자에서 선택 hello **hello클라우드에서호스트**확인란을 선택 (이 확인란은 레이블이 지정 된 **원격 리소스 만들기** 일부 설치에서).
   
    ![][0]
3. 이 예제에서는 Microsoft Azure hello 드롭 다운 목록에서 선택 **가상 컴퓨터 (v1)**, hello를 클릭 한 다음 **확인** 단추입니다.
4. 로그인할지 묻는 tooAzure에 로그인 합니다. hello **가상 컴퓨터 만들기** 대화 상자가 나타납니다.
   
    ![][2]
5. Hello에 **DNS 이름** 상자 hello 가상 컴퓨터에 대 한 이름을 입력 합니다. hello DNS 이름은 Azure 내에서 고유 해야 합니다. 입력 한 hello 이름이 사용할 수 없는 경우 빨간색 느낌표가 표시 됩니다.
6. Hello에 **이미지** 목록 toobase hello 가상 컴퓨터에서 원하는 hello 이미지를 선택 합니다. Hello 표준 Azure 가상 컴퓨터 이미지 또는 tooAzure를 업로드 한 이미지 중 하나를 선택할 수 있습니다.
7. Hello 둡니다 **IIS 사용 및 웹 배포** tooinstall 다른 웹 서버를 제외 하면 확인란 합니다. 웹 배포 사용 하지 않도록 설정 하는 경우 Visual Studio에서 수 toopublish 수 없습니다. IIS 및 웹 배포 tooany hello 패키지 된 Windows Server 이미지를 사용자 지정 이미지를 포함 하 여 추가할 수 있습니다.
8. Hello에 **크기** 목록 hello 가상 컴퓨터의 hello 크기를 선택 합니다.
9. 이 가상 컴퓨터에 대 한 로그인 자격 증명 hello를 지정 합니다. 자격 증명을 기록해, tooaccess hello 원격 데스크톱을 통해 컴퓨터에 필요 하므로.
10. Hello에 **위치** 목록 hello 지역 toohost hello 가상 컴퓨터를 선택 합니다.
11. Hello 클릭 **확인** 단추 toostart hello 가상 컴퓨터를 만드는 중입니다. Hello hello 연산의 hello 진행 상황을 따를 수 **출력** 창.
    
    ![][3]
12. Hello 가상 컴퓨터가 프로비저닝되 면 게시 된 스크립트에 만들어집니다는 **PublishScripts** 솔루션에서 노드. hello 게시 스크립트가 실행 되 고 프로 비전 가상 컴퓨터를 Azure에서. hello **출력** hello 상태 창에 표시 합니다. hello 스크립트 hello hello 가상 컴퓨터를 작업 tooset 다음을 수행 합니다.
    
    * 존재 하지 않는 경우 hello 가상 컴퓨터를 만듭니다.
    * 로 시작 하는 이름으로 저장소 계정을 만듭니다 `devtest`, hello 지정 된 영역에 저장소 계정을 아직 없는 경우에 합니다.
    * Hello 가상 컴퓨터에 대 한 컨테이너로 클라우드 서비스를 만들고 hello 웹 응용 프로그램에 대 한 웹 역할을 만듭니다.
    * Hello 가상 컴퓨터에 웹 배포를 구성합니다.
    * Hello 가상 컴퓨터에서 IIS 및 ASP.NET을 구성합니다.
    
    ![][4]
13. (선택 사항) Toohello 새 가상 컴퓨터를 연결할 수 있습니다. **서버 탐색기**, hello 확장 **가상 컴퓨터** 노드를 hello 노드를 만든 hello 가상 컴퓨터에 대 한 바로 가기 메뉴를 선택 **원격데스크톱을사용하여연결**. 또는에서 **클라우드 탐색기** 선택할 수 있습니다 **포털에서 열기** 바로 가기 메뉴를 hello 되 고 있는 toohello 가상 컴퓨터에 연결 합니다.
    
    ![][5]

## <a name="next-steps"></a>다음 단계
자세한 정보를 읽을 toocustomize hello 게시 스크립트를 작성 하려는 경우 [Windows PowerShell 스크립트를 사용 하 여 tooPublish tooDev 및 시험 환경](http://msdn.microsoft.com/library/dn642480.aspx)합니다.

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
