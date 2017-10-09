1. Toohello 로그인 [Azure 클래식 포털](http://manage.windowsazure.com)합니다.  
2. Hello hello 창 맨 아래에 hello 명령 모음에서 **새로**합니다.
3. **계산**에서 **가상 컴퓨터**를 클릭한 후 **갤러리에서**를 클릭합니다.
   
    ![새 가상 컴퓨터 만들기][Image1]
4. Hello에서 **SUSE** 그룹 OpenSUSE 가상 컴퓨터 이미지를 선택한 다음 화살표 toocontinue hello를 클릭 합니다.
5. Hello에 첫 번째 **가상 컴퓨터 구성** 페이지:
   
   * **가상 컴퓨터 이름**(예: "testlinuxvm")을 입력합니다. hello 이름은 3 자에서 15 자 사이의 문자를 포함, 수 문자, 숫자 및 하이픈을 포함 하 고 해야 시작 문자로 하 고 문자 또는 숫자로 끝나야 합니다.
   * Hello 확인 **계층** 선택 하 고는 **크기**합니다. hello 계층에서 선택할 수 있습니다 hello 크기를 결정 합니다. 안녕, 뿐만 아니라 데이터 디스크 수와 같은 구성 옵션 사용의 hello 비용 연결할 수 있는 크기에 영향을 줍니다. 자세한 내용은 [가상 컴퓨터의 크기](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.
   * 입력 **새 사용자 이름**, hello 기본값을 그대로 또는 **azureuser**합니다. 이 이름은 toohello Sudoers 목록 파일에 추가 됩니다.
   * 유형을 결정 **인증** toouse 합니다. 일반적인 암호 지침은 [강력한 암호](http://msdn.microsoft.com/library/ms161962.aspx)를 참조하세요.
6. Hello에 다음 **가상 컴퓨터 구성** 페이지:
   
   * Hello 기본값을 사용 하 여 **새 클라우드 서비스를 만들**합니다.
   * Hello에 **DNS 이름** 고유 DNS 이름 toouse "testlinuxvm" 같은 hello 주소의 일환으로 입력 합니다.
   * Hello에 **지역/선호도 그룹/가상 네트워크** 상자에서이 가상 이미지가 호스팅될 여기서 지역을 선택 합니다.
   * 아래 **끝점**, hello SSH 끝점을 유지 합니다. 있습니다 수 지금, 다른 사용자를 추가 하거나 추가, 변경 또는 hello 가상 컴퓨터를 만든 후이 삭제 합니다.
     
     > [!NOTE]
     > 가상 컴퓨터 toouse 가상 네트워크를 선택 하면 **해야** hello 가상 컴퓨터를 만들 때 hello 가상 네트워크를 지정 합니다. Hello 가상 컴퓨터를 만든 후 가상 컴퓨터 tooa 가상 네트워크를 추가할 수 없습니다. 자세한 내용은 [가상 네트워크 개요](../articles/virtual-network/virtual-networks-overview.md)를 참조하세요.
     > 
     > 
7. Hello에 마지막 **가상 컴퓨터 구성** 페이지, hello 기본 설정을 그대로 유지 한 다음 확인 표시 toofinish hello를 클릭 합니다.

hello 포털 표시 되는 새 가상 컴퓨터에 hello **가상 컴퓨터**합니다. Hello 상태가로 보고 됩니다 동안 **(프로 비전)**, hello 가상 컴퓨터가 설정 되 고 있습니다. Hello 상태가로 보고 됩니다 때 **실행**, toohello 다음 단계로 이동할 수 있습니다.

## <a name="connect-toohello-virtual-machine"></a>Toohello 가상 컴퓨터를 연결 합니다.
SSH 또는 PuTTY tooconnect toohello 가상 컴퓨터에서 연결 하는 hello 컴퓨터에 hello 운영 체제에 따라 사용 합니다.

* Linux를 실행하는 컴퓨터에서 SSH를 사용합니다. Hello 명령 프롬프트에서 다음을 입력 합니다.
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Hello 사용자의 암호를 입력 합니다.
* Windows를 실행하는 컴퓨터에서 PuTTY를 사용합니다. 설치 작업을 없다면 hello에서 다운로드 [PuTTY 다운로드 페이지][PuTTYDownload]합니다.
  
    저장 **putty.exe** tooa 컴퓨터 디렉터리에 있습니다. 명령 프롬프트를 열고 toothat 폴더를 찾아 실행 **putty.exe**합니다.
  
    "Testlinuxvm.cloudapp.net" 같은 hello 호스트 이름을 입력 하 고 "22" hello에 대 한 입력 **포트**합니다.
  
    ![PuTTY 화면][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>가상 컴퓨터 (선택 사항) hello를 업데이트 합니다.
1. 을 사용 하는 가상 컴퓨터를 연결 된 toohello 후 시스템 업데이트 및 패치를 선택적으로 설치할 수 있습니다. 형식 toorun hello 업데이트:
   
    `$ sudo zypper update`
2. 선택 **소프트웨어**, 다음 **온라인 업데이트** toolist 사용 가능한 업데이트 합니다. 선택 **Accept** toostart 설치 hello 및 모든 새로운 사용 가능한 패치 (점을 제외 하 고 선택적 것 hello)를 적용 합니다.
3. 설치가 완료되면 **마침**을 선택합니다.  시스템 이제 toodate 제공 됩니다.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
