### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Hello 데이터베이스 엔진의 기본 인스턴스 hello에 대 한 hello Windows 방화벽에서 TCP 포트를 열어야 합니다.
1. 원격 데스크톱으로 toohello 가상 컴퓨터를 연결 합니다. Toohello VM 연결 방법에 대 한 자세한 내용은 참조 하십시오. [SQL VM 원격 데스크톱으로 열고](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop)합니다.
2. Hello 시작 화면에서 로그인 되 면 입력 **WF.msc**, 한 다음 ENTER 키를 누릅니다.
   
    ![Hello 방화벽 프로그램을 시작 합니다.](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. Hello에 **고급 보안이 포함 된 Windows 방화벽**hello 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 **인바운드 규칙**, 클릭 하 고 **새 규칙** hello 작업 창에서.
   
    ![새 규칙](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. Hello에 **새 인바운드 규칙 마법사** 대화 상자의 **규칙 유형**선택, **포트**, 클릭 하 고 **다음**합니다.
5. Hello에 **프로토콜 및 포트** 대화 상자에서 사용 하 여 hello 기본 **TCP**합니다. Hello에 **특정 로컬 포트** 상자 다음 형식 hello에 대 한 포트 번호의 hello hello 데이터베이스 엔진 인스턴스의 (**1433** hello 기본 인스턴스 또는 hello hello 끝점 단계에서 개인 포트에 대해 선택한 사항에 대 한).
   
    ![TCP 포트 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. **다음**을 누릅니다.
7. Hello에 **동작** 대화 상자에서 **hello 연결 허용**, 클릭 하 고 **다음**합니다.
   
    **보안 정보:** Selecting **보안 hello 연결을 허용** 추가 보안을 제공할 수 있습니다. 사용자 환경에서 tooconfigure 추가 보안 옵션을 원하는 경우이 옵션을 선택 합니다.
   
    ![연결 허용](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. Hello에 **프로필** 대화 상자에서 **공용**, **개인**, 및 **도메인**합니다. 그런 후 **Next**를 클릭합니다.
   
    **보안 정보:** Selecting **공용** 를 통해 액세스할 수 있도록 인터넷 hello 합니다. 가능하면 더 제한적인 프로필을 선택하세요.
   
    ![공개 프로필](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. Hello에 **이름** 대화 상자에서 이름 및이 규칙에 대 한 설명을 입력 하 고 클릭 **마침**합니다.
   
    ![규칙 이름](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

필요한 경우 다른 구성 요소의 추가 포트를 엽니다. 자세한 내용은 참조 [hello Windows 방화벽 tooAllow SQL Server 액세스를 구성](http://msdn.microsoft.com/library/cc646023.aspx)합니다.

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>SQL Server toolisten hello TCP 프로토콜에서 구성

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>혼합 모드 인증을 위해 SQL Server 구성
SQL Server 데이터베이스 엔진 hello 도메인 환경이 없는 Windows 인증을 사용할 수 없습니다. 다른 컴퓨터에서 데이터베이스 엔진 tooconnect toohello 혼합된 모드 인증에 대 한 SQL Server를 구성 합니다. 혼합 모드 인증은 SQL Server 인증과 Windows 인증을 모두 허용합니다.

> [!NOTE]
> Azure 가상 네트워크를, 구성된 도메인 환경으로 구성한 경우, 혼합 모드 인증은 구성할 필요가 없습니다.
> 
> 

1. Hello 시작 페이지에서 가상 컴퓨터를 연결 된 toohello 하는 동안 입력 **SQL Server Management Studio** hello 선택한 아이콘을 클릭 합니다.
   
    처음으로 Management Studio hello 사용자가 Management Studio 환경을 만들어야 열 번호입니다. 어느 정도 시간이 걸릴 수 있습니다.
2. Management Studio 제공 hello **tooServer 연결** 대화 상자. Hello에 **서버 이름** 상자 hello 개체 탐색기로 hello 가상 컴퓨터 tooconnect toohello 데이터베이스 엔진의 hello 이름을 입력 합니다 (사용할 수 있습니다 hello 가상 컴퓨터 이름 대신 **(local)** 또는 단일 기간의 hello로 **서버 이름**). 선택 **Windows 인증**, 둡니다  ***your_VM_name*\your_local_administrator** hello에 **사용자 이름** 상자입니다. **Connect**를 클릭합니다.
   
    ![TooServer 연결](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. SQL Server Management Studio 개체 탐색기에서 hello (hello 가상 컴퓨터 이름), SQL Server의 hello 인스턴스 이름을 마우스 오른쪽 단추로 클릭 하 고 클릭 **속성**합니다.
   
    ![서버 속성](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Hello에 **보안** 페이지의 **서버 인증**선택, **SQL Server 및 Windows 인증 모드**, 클릭 하 고 **확인** .
   
    ![인증 모드 선택](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. Hello SQL Server Management Studio 대화 상자에서 클릭 **확인** tooacknowledge hello 요구 사항 toorestart SQL Server.
6. 개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭한 후 **다시 시작**을 클릭합니다. SQL Server 에이전트가 실행 중인 경우 에이전트도 다시 시작해야 합니다.
   
    ![다시 시작](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. Hello SQL Server Management Studio 대화 상자에서 클릭 **예** tooagree toorestart SQL Server 되도록 합니다.

### <a name="create-sql-server-authentication-logins"></a>SQL Server 인증 로그인 만들기
다른 컴퓨터에서 tooconnect toohello 데이터베이스 엔진, SQL Server 인증 로그인을 하나 이상 만들어야 합니다.

1. SQL Server Management Studio 개체 탐색기에서 toocreate hello에 대 한 새 로그인 원하는 hello 서버 인스턴스의 hello 폴더를 확장 합니다.
2. 마우스 오른쪽 단추로 클릭 hello **보안** 폴더를 너무 가리킨**새로**, 선택한 **로그인...** .
   
    ![새 로그인](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. Hello에 **로그인-신규** 대화 상자의 hello **일반** 페이지에서 hello에 hello 새 사용자의 hello 이름을 입력 **로그인 이름** 상자입니다.
4. **SQL Server 인증**을 선택합니다.
5. Hello에 **암호** 상자에 새 사용자 hello에 대 한 암호를 입력 합니다. Hello에 해당 암호를 다시 입력 **암호 확인** 상자입니다.
6. 필요한 hello 암호 적용 옵션을 선택 (**암호 정책 강제 적용**, **암호 만료 강제 적용**, 및 **사용자는 다음 로그인 시 암호를 변경 해야**). 이 로그인을 직접 사용 하는 경우에 hello 다음 로그인 시 암호 변경 toorequire를 설치할 필요가 없습니다.
7. Hello에서 **기본 데이터베이스** 목록 hello 로그인에 대 한 기본 데이터베이스를 선택 합니다. **마스터** 이 옵션에 대 한 hello 기본값입니다. 사용자 데이터베이스를 아직 만들지 않은 경우에이 둡니다**마스터**합니다.
   
    ![로그인 속성](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. Hello 처음 로그인을 만들려는 경우 수도 있습니다 toodesignate이 로그인이 SQL Server 관리자 역할. Hello에 그렇다면 **서버 역할** 페이지 **sysadmin**합니다.
   
   > [!NOTE]
   > Hello sysadmin 고정 서버 역할의 멤버가 데이터베이스 엔진 hello를 완전히 제어할 수 있습니다. 따라서 이 역할의 구성원은 신중하게 제한해야 합니다.
   > 
   > 
   
   ![sysadmin](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. 확인을 클릭합니다.

SQL Server 로그인에 대한 자세한 내용은 [로그인 만들기](http://msdn.microsoft.com/library/aa337562.aspx)를 참조하십시오.

