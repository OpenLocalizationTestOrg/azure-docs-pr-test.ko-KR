### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>Hello 공용 IP 주소에 대 한 DNS 레이블을 구성합니다

hello 인터넷에서에서 SQL Server 데이터베이스 엔진 tooconnect toohello 공용 IP 주소에 대 한 DNS 레이블을 만드는 것이 좋습니다. IP 주소를 통해 연결할 수 있고 DNS 레이블을 hello를 보다 쉽게 tooidentify A 레코드를 만듭니다 요약이 hello 공용 IP 주소를 원본으로 사용 합니다.

> [!NOTE]
> DNS 레이블을 필요 없는 hello 내 계획 tooonly 연결 toohello SQL Server 인스턴스가 동일한 가상 네트워크 또는 로컬로 합니다.

DNS 레이블을 toocreate 먼저 선택 **가상 컴퓨터** hello 포털에서입니다. 에 SQL Server VM toobring 해당 속성을 선택 합니다.

1. Hello 가상 컴퓨터 개요에서를 선택 하면 **공용 IP 주소**합니다.

    ![공용 IP 주소](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. 공용 IP 주소에 대 한 hello 속성을 확장 하 고 **구성**합니다.

1. DNS 레이블 이름을 입력합니다. 이 이름은 A 레코드 대신 IP 주소를 통해 이름으로 사용 되는 tooconnect tooyour SQL Server VM을 직접 일 수 있는입니다.

1. Hello 클릭 **저장** 단추입니다.

    ![dns 레이블](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>다른 컴퓨터에서 toohello 데이터베이스 엔진 연결

1. 연결 된 toohello 컴퓨터에서 인터넷을 열고 SQL Server Management Studio (SSMS). SQL Server Management Studio가 없는 경우 [여기](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)에서 다운로드할 수 있습니다.

1. Hello에 **tooServer 연결** 또는 **tooDatabase 엔진 연결** 대화 상자에서 편집 hello **서버 이름** 값입니다. Hello IP 주소 또는 (hello 이전 태스크에서 확인) hello 가상 컴퓨터의 전체 DNS 이름을 입력 합니다. 쉼표를 추가하고 SQL Server의 TCP 포트를 제공할 수도 있습니다. 예: `mysqlvmlabel.eastus.cloudapp.azure.com,1433`.

1. Hello에 **인증** 상자 **SQL Server 인증**합니다.

1. Hello에 **로그인** 상자 올바른 SQL 로그인의 hello 이름을 입력 합니다.

1. Hello에 **암호** 상자, hello 로그인의 hello 암호를 입력 합니다.

1. **Connect**를 클릭합니다.

    ![ssms 연결](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)