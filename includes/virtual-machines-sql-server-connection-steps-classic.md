### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>Hello 가상 컴퓨터의 DNS 이름을 hello 결정
tooconnect toohello 다른 컴퓨터에서 SQL Server 데이터베이스 엔진, hello DNS 도메인 이름 ()를 알고 있어야 hello 가상 컴퓨터의 이름입니다. (이 hello 이름 hello 인터넷 사용 하 여 tooidentify hello 가상 컴퓨터. Hello IP 주소를 사용할 수 있지만 Azure에서 중복성 이나 유지 관리에 대 한 리소스 이동할 때 hello IP 주소가 변경 될 수 있습니다. 기 hello DNS 이름은 안정적인 것 tooa 새 IP 주소를 리디렉션됩니다.)  

1. Hello Azure 포털에서에서 (또는 hello 이전 단계의) 선택 **가상 컴퓨터 (클래식)**합니다.
2. SQL VM을 선택합니다.
3. Hello에 **가상 컴퓨터** 블레이드, 복사 hello **DNS 이름** hello 가상 컴퓨터에 대 한 합니다.
   
    ![DNS 이름](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>다른 컴퓨터에서 toohello 데이터베이스 엔진 연결
1. 컴퓨터에서 연결 toohello 인터넷, SQL Server Management Studio를 엽니다.
2. Hello에 **tooServer 연결** 또는 **tooDatabase 엔진 연결** 대화 상자의 hello **서버 이름** (hello에서 결정 하는 hello 가상 컴퓨터의 hello DNS 이름을 입력 합니다 이전 작업)과의 hello 형식에 공용 끝점 포트 번호 *DNSName, portnumber* 같은 **mysqlvm.cloudapp.net,57500**합니다.
   
    ![SSMS를 사용하여 연결](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    Hello 공용 끝점 포트 번호를 기억 하지 못하는 경우 이전에 만든, hello에서 찾을 수 있습니다 **끝점** hello 부문의 **가상 컴퓨터** 블레이드입니다.
   
    ![공용 포트](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. Hello에 **인증** 상자 **SQL Server 인증**합니다.
4. Hello에 **로그인** 상자 이전 작업에서 만든 로그인의 hello 이름을 입력 합니다.
5. Hello에 **암호** 상자에서 이전 태스크에서 만드는 hello 로그인의 hello 암호를 입력 합니다.
6. **Connect**를 클릭합니다.

