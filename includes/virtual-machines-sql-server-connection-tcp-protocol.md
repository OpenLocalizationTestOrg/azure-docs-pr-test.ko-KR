1. 검색할 가상 컴퓨터 연결 된 toohello 원격 데스크톱을 사용 하는 동안 **Configuration Manager**:

    ![SSCM 열기](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. SQL Server 구성 관리자에서 hello 콘솔 창에서 확장 **SQL Server 네트워크 구성**합니다.

1. Hello 콘솔 창에서 클릭 **MSSQLSERVER에 대 한 프로토콜** (hello 기본 인스턴스 이름)입니다. Hello 세부 정보 창에서 마우스 오른쪽 단추로 클릭 **TCP** 클릭 **사용** 아직 활성화 되지 않은 경우.

    ![TCP 사용](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Hello 콘솔 창에서 클릭 **SQL Server 서비스**합니다. Hello 세부 정보 창에서 마우스 오른쪽 단추로 클릭  **SQL Server (*인스턴스 이름을*) * * (hello 기본 인스턴스는 **SQL Server (MSSQLSERVER)**)를 클릭 하 고 **다시 시작** , SQL Server의 hello 인스턴스 toostop 및 다시 시작 합니다.

    ![데이터베이스 엔진 다시 시작](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. SQL Server 구성 관리자를 닫습니다.

SQL Server 데이터베이스 엔진 hello에 대 한 프로토콜을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 [서버 네트워크 프로토콜 설정 또는 해제](http://msdn.microsoft.com/library/ms191294.aspx)합니다.
