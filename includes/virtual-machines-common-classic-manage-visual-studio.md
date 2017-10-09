Visual Studio에서 서버 탐색기를 사용하여 Azure에 가상 컴퓨터를 만들 수 있습니다.

## <a name="create-an-azure-virtual-machine-in-server-explorer"></a>서버 탐색기에서 Azure 가상 컴퓨터 만들기
Hello에 가상 컴퓨터를 만들 수 있지만 [Azure 관리 포털](http://go.microsoft.com/fwlink/?LinkID=253103), 서버 탐색기에서 명령을 사용 하 여 Azure에서 가상 컴퓨터를 만들 수도 있습니다. 일반적인 부하 분산 된 공용 끝점 뒤 tooprovide 프런트 종료 하는 예를 들어, 가상 컴퓨터를 사용할 수입니다.

### <a name="toocreate-a-new-virtual-machine"></a>toocreate 새 가상 컴퓨터
1. 서버 탐색기를 열고 hello **Azure** 노드와 클릭 **가상 컴퓨터**합니다.
2. Hello 상황에 맞는 메뉴에서 클릭 **가상 컴퓨터 만들기**합니다.
   
    hello **새 가상 컴퓨터를 만들고** 마법사가 나타납니다.
   
    ![hello 가상 컴퓨터 만들기 명령](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718342.png)
3. Hello에 **구독 선택** 페이지 hello 가상 컴퓨터를 만들 때 구독 toouse를 선택 하 고 클릭 **다음**합니다.
   
    TooAzure에 서명 하지 않은 경우 클릭 **로그인** toosign에 있습니다. 그런 다음 선택 되어 있지 않은 경우 hello 드롭다운 목록 상자에 Azure 구독을 선택 합니다.
4. Hello에 **가상 컴퓨터 이미지 선택** 페이지를 hello 이미지 유형을 선택 **이미지 유형** 드롭다운 목록 상자를 선택한 후 가상 컴퓨터 이미지 hello에 **이미지 이름** 목록 상자입니다. 완료되면 **확인**을 클릭합니다.
   
    ![가상 컴퓨터 이미지 페이지 선택](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744137.png)
   
    Hello 이미지 유형만 선택할 수 있습니다.
   
   * **공용 이미지** 는 Windows Server 및 SQL Server와 같은 서버 소프트웨어와 운영 체제의 가상 컴퓨터 이미지를 나열합니다.
   * **MSDN 이미지** 는 Visual Studio 및 Microsoft Dynamics와 같은 소프트웨어 사용 가능한 tooMSDN 구독자의 가상 컴퓨터 이미지를 나열 합니다.
   * **개인 이미지** 는 사용자가 만든 특수화 및 일반화된 가상 컴퓨터 이미지를 나열합니다.
     
     참조, toolearn는 약 특수화 및 가상 컴퓨터를 일반화 [VM 이미지](https://azure.microsoft.com/blog/2014/04/14/vm-image-blog-post/)합니다. 참조 [어떻게 tooCapture 템플릿으로 Windows 가상 컴퓨터 tooUse](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) tooturn tooquickly를 사용할 수 있는 템플릿으로 가상 컴퓨터를 새로 만드는 가상 컴퓨터를 미리 구성 된에 대 한 정보에 대 한 합니다.
     
     가상 컴퓨터 이미지 이름 toosee 정보 hello 이미지에 대 한 hello 오른쪽에 hello 페이지의 클릭 수 있습니다.
     
     > [!NOTE]
     > 가상 컴퓨터 이미지 toohello를 추가할 수 없습니다 **공용 이미지** 또는 **MSDN 이미지** 은 읽기 전용 이므로 나열 합니다. 만드는 모든 가상 컴퓨터가 추가 toohello **개인 이미지** 목록입니다.
     > 
     > 
     
     Visual Studio 수준 구독이 있는 MSDN 구독자인 경우에 Visual Studio 및 다른 여러 이미지를 포함하는 미리 작성된 Azure 가상 컴퓨터를 만들 수 있습니다. 자세한 내용은 [MSDN 구독자를 위한 Images Visual Studio 2013 갤러리 이미지를 사용하여 Visual Studio에서 가상 컴퓨터 만들기](http://visualstudio2013msdngalleryimage.azurewebsites.net) 및 [MSDN 구독](https://www.visualstudio.com/products/msdn-subscriptions-vs)을 참조하세요.|
5. Hello에 **가상 컴퓨터 기본 설정** 페이지 컴퓨터 이름을 입력 하 고 다음 hello 크기, 사용자 이름 및 암호를 포함 하 여 hello 가상 컴퓨터에 대 한 hello 사양을 추가 합니다. 완료되면 **확인**을 클릭합니다.
   
    Hello 새 이름을 사용 합니다 및 암호 toolog 있습니다 경우 다운 하는 것이 좋습니다 toowrite 되기 때문에 원격 데스크톱을 사용 하 여 hello 컴퓨터를 제거 합니다. 크기 및 기타 설정을 hello에 Visual Studio에서 Azure 가상 컴퓨터를 만든 후 변경할 수 있습니다 [Azure 관리 포털](http://go.microsoft.com/fwlink/?LinkID=253103)합니다.
   
   > [!NOTE]
   > Hello 가상 컴퓨터에 대해 더 큰 크기를 선택 하면 추가 요금이 적용 될 수 있습니다. 자세한 내용은 [가상 컴퓨터 가격 정보](https://azure.microsoft.com/pricing/details/virtual-machines/) 를 참조하세요.
   > 
   > 
6. Visual Studio에서 만든 가상 컴퓨터는 클라우드 서비스를 필요로 합니다. Hello에 **클라우드 서비스 설정** 페이지 hello 가상 컴퓨터용 클라우드 서비스를 선택 하거나 클릭 **< 새로 만들기 … >** 클라우드 서비스 또는 새 toouse 원하는 아직 없는 경우 hello 드롭다운 목록에서 하나입니다. 저장소 계정은도 필요 하므로 저장소 계정을 선택 (만들거나, 새 저장소 계정) hello에 **저장소 계정** 드롭다운 목록 상자입니다. 참조 [Azure 저장소 소개 tooMicrosoft](../articles/storage/common/storage-introduction.md) 자세한 정보에 대 한 합니다.
7. (이 선택 사항) 가상 네트워크 toospecify hello 가상 네트워크와 서브넷 드롭다운 목록 상자에서 선택 합니다.
   
    가용성 집합의 구성원 인 가상 컴퓨터는 배포 된 toodifferent 오류 도메인입니다. 자세한 내용은 [Azure 가상 네트워크](https://azure.microsoft.com/services/virtual-network/) 를 참조하세요.
8. Toobelong tooan 가용성 가상 컴퓨터 집합 (옵션) hello를 선택 합니다 **가용성 집합 지정** 확인란을 선택 하 고 가용성 hello 드롭다운 목록 상자에 집합을 선택 합니다. 완료 되 면 선택 hello **다음** 단추입니다.
   
    가상 컴퓨터 tooan 추가 가용성 집합은 네트워크 오류, 로컬 디스크 하드웨어 오류 및 계획 된 가동 중지 시간 동안 사용 가능한 상태로 유지 하는 응용 프로그램을 쉽게 합니다. Toouse hello 필요한 [Azure 관리 포털](http://go.microsoft.com/fwlink/?LinkID=253103) toocreate 가상 네트워크, 서브넷 및 가용성을 설정 합니다. 참조 [가상 컴퓨터의 가용성 관리 hello](https://azure.microsoft.com/documentation/articles/manage-availability-virtual-machines/) 자세한 정보에 대 한 합니다.
9. Hello에 **끝점** 페이지에서 원하는 가상 컴퓨터의 사용 가능한 toousers hello 공용 끝점을 지정 합니다. 예를 들어 선택할 수 있습니다 tooenable HTTP (포트 80) 또한 toohello 원격 데스크톱 및 PowerShell 끝점을 기본적으로 활성화 됩니다. 끝점, tooadd hello에 하나를 선택 합니다. **포트 이름** 드롭다운 목록 상자를 선택한 후 hello **추가** 단추입니다. 끝점을 tooremove 선택 hello 빨간색 **X** hello 끝점 목록에서 다음 toohello 이름입니다.
   
    ![hello hello 가상 컴퓨터 마법사의 페이지를 끝점입니다.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC718351.png)
   
    가상 컴퓨터에 대해 선택한 hello 클라우드 서비스에 사용할 수 있는 hello 끝점에 따라 다릅니다. 자세한 내용은 [Azure 서비스 끝점](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) 을 참조하세요.
   
   > [!NOTE]
   > 공용 끝점을 사용 하면 가상 컴퓨터가 사용 가능한 toohello에서 서비스 인터넷 합니다. 있는지 tooinstall 수 고 올바르게 구성 hello 끝점 및 서비스가 가상 컴퓨터에 hello 끝점에 대 한 액세스 제어 설정 목록 (Acl)와 같은 합니다. 참조 [어떻게 tooSet 끝점 tooa 가상 컴퓨터](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/) 자세한 정보에 대 한 합니다.
   > 
   > 
10. Hello 가상 컴퓨터 설정을 구성을 마친 후 선택 hello **만들기** 단추 toocreate hello 가상 컴퓨터.
    
     Azure에서 가상 컴퓨터 hello, hello **Azure 활동 로그** 표시 hello hello 가상 컴퓨터 만들기 작업의 진행 상황입니다.
    
     ![가상 컴퓨터 활동 로그 - 진행 중입니다.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744138.png)
    
     tooview 전용 가상 컴퓨터 정보를 hello 선택 **가상 컴퓨터** hello 탭 **Azure 활동 로그**합니다.
    
     ![가상 컴퓨터 활동 로그 - 완료했습니다.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744139.png)
    
     Hello 작업이 성공적으로 완료 되 면 hello 새 가상 컴퓨터 hello 표시 **가상 컴퓨터** 서버 탐색기에서 노드. Hello를 클릭 하 여 로그인 할 수 **원격 데스크톱을 사용 하 여 연결** 바로 가기 합니다.
    
     ![서버 탐색기에 표시되는 가상 컴퓨터입니다.](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744140.png)

## <a name="manage-your-virtual-machines"></a>가상 컴퓨터 관리
Hello 가상 컴퓨터 구성 페이지에서 또한 아래로 tooshutting, 연결, 새로 고침 및 검사점 toohello 추가 가상 컴퓨터를 선택, 확인 하거나 hello 가상 컴퓨터에 대 한 설정을 변경할 수도 있습니다. 다음을 수행할 수 있습니다.

* Hello 가상 컴퓨터 크기를 변경 합니다.
* 선택 hello 가용성 toouse hello 가상 컴퓨터를 설정합니다.
* 공용 끝점에 대한 설정을 추가, 제거 또는 변경합니다.
* 가상 컴퓨터 확장을 추가, 제거 또는 구성합니다.
* Hello 가상 컴퓨터와 관련 된 hello 디스크에 대 한 정보 보기입니다.

### <a name="view-or-change-virtual-machine-settings"></a>가상 컴퓨터 설정 보기 또는 변경
1. 서버 탐색기에서 hello에 가상 컴퓨터를 선택 합니다. **Azure 가상 컴퓨터** 노드.
2. Hello 바로 가기 메뉴에서 선택 **구성** tooview hello 가상 컴퓨터 구성 페이지입니다.
   
    ![hello Azure 가상 컴퓨터 구성 페이지](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744141.png)
3. Hello 가상 컴퓨터 정보를 확인 하거나 변경 합니다.

### <a name="save-or-restore-hello-status-of-your-virtual-machine"></a>저장 하거나 가상 컴퓨터의 hello 상태를 복원 합니다.
가상 컴퓨터를 구성 하 고 소프트웨어를 설치 하면 가상 컴퓨터 검사점을 만들어 진행률 저장 하는 것이 좋습니다 tooregularly이 합니다. 검사점에는 스냅숏, 또는 hello 현재 상태의 가상 컴퓨터의 이미지입니다. Hello 가상 컴퓨터에 문제가 발생 하거나 tooreconfigure hello 가상 컴퓨터를 처음부터 다시 시작 하지 않고 tooa 이전 검사점으로 복원 하 여 시간을 절약할 수 있습니다.

### <a name="toocreate-a-virtual-machine-checkpoint"></a>가상 컴퓨터 검사점 toocreate
1. 서버 탐색기에서 hello에 가상 컴퓨터를 선택 합니다. **Azure 가상 컴퓨터** 노드.
2. Hello 바로 가기 메뉴에서 선택 **구성** tooview hello 가상 컴퓨터 구성 페이지입니다.
3. Hello 구성 페이지에서 선택 hello **이미지 캡처** 단추입니다.
   
    ![Azure 구성 페이지 캡처 단추](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744142.png)
   
    hello **가상 컴퓨터 캡처** 대화 상자가 나타납니다.
   
    ![Azure 캡처 가상 컴퓨터 대화 상자](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744143.png)
4. 이미지 레이블 및 설명을 제공합니다. 기본 레이블 및 설명이 제공되지만 원하는 경우 덮어쓸 수 있습니다.
5. 이 가상 컴퓨터에 이미 Sysprep를 실행 하는 경우 선택 hello **hello 가상 컴퓨터에서 Sysprep를 실행 했습니다** 상자입니다.
   
    Sysprep은 도구는 특히, 다른 사람이 사용할 수 있는 템플릿으로 만드는 Windows hello 가상 컴퓨터의 버전에서 시스템 관련 데이터를 제거 합니다. 참조 [어떻게 tooCapture 템플릿으로 Windows 가상 컴퓨터 tooUse](https://azure.microsoft.com/documentation/articles/virtual-machines-capture-image-windows-server/) 자세한 정보에 대 한 합니다. Sysprep를 실행 하기 전에 hello VM 백업 합니다.
6. Hello 캡처 설정의 구성을 마친 후 선택 hello **캡처** 단추 toocreate hello 검사점입니다.
   
    Azure에서 hello 검사점, hello **Azure 활동 로그** 표시 hello hello 작업의 진행 상황입니다.
   
    ![가상 컴퓨터 검사점 캡처하기](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744144.png)
   
    Hello 검사점 작업이 완료 되 면 hello에 표시 됩니다 **Azure 활동 로그**합니다.
   
    ![완료된 검사점 작업](./media/virtual-machines-common-classic-create-manage-visual-studio/IC744145.png)

## <a name="toomanage-virtual-machine-checkpoints"></a>toomanage 가상 컴퓨터 검사점
### <a name="toorestore-a-virtual-machine-tooa-previously-saved-state"></a>이전에 저장 된 가상 컴퓨터 tooa toorestore 상태
* 에 설명 된 hello 단계에 따라 [단계별: 수행 클라우드 복원 Microsoft Azure 가상 컴퓨터의 PowerShell-2 부를 사용 하 여](http://blogs.technet.com/b/keithmayer/archive/2014/02/04/step-by-step-perform-cloud-restores-of-windows-azure-virtual-machines-using-powershell-part-2.aspx)합니다.

### <a name="toodelete-a-checkpoint"></a>toodelete 검사점
1. Toohello 이동 [Azure 관리 포털](http://go.microsoft.com/fwlink/?LinkID=253103)합니다.
2. Hello 가상 컴퓨터 구성 페이지에서 선택 hello **이미지** hello hello 페이지 맨 아래에 탭 합니다.
3. Hello 검사점 toodelete, 원하는 고 hello를 눌러 선택 **삭제** hello hello 페이지 맨 아래에 단추입니다.

## <a name="shut-down-your-virtual-machine"></a>가상 컴퓨터 종료
1. 서버 탐색기에서 원하는 hello에 다운 tooshut hello 가상 컴퓨터를 선택 **Azure 가상 컴퓨터** 노드.
2. Hello를 선택 하거나 hello 바로 가기 메뉴에서 **종료** 명령, 또는 선택 **구성** tooview hello 가상 컴퓨터 구성 페이지를 선택한 후 hello **종료**단추입니다.

## <a name="next-steps"></a>다음 단계
가상 컴퓨터 만들기에 대 한 더 toolearn 참조 [는 Linux 가상 컴퓨터 실행을 만들](../articles/virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 및 [hello Azure preview 포털에서 Windows를 실행 중인 가상 컴퓨터를 만드는](../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.

