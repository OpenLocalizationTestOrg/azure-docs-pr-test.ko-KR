1. Azure 사이트 복구 UnifiedSetup.exe hello를 시작 합니다.
2. **시작 하기 전에**선택, **배포 아웃 추가 프로세스 서버 tooscale 추가**합니다.

  ![프로세스 서버 추가](./media/site-recovery-add-process-server/ps-page-1.png)

3. **구성 서버 세부 정보**hello hello 구성 서버 IP 주소를 지정 하 고 hello 암호입니다.

  ![프로세스 서버 2 추가](./media/site-recovery-add-process-server/ps-page-2.png)
4. **인터넷 설정을**, hello 구성 서버에서 실행 중인 공급자를 통해 tooAzure 사이트 복구를 연결 하는 hello 인터넷 hello 하는 방법을 지정 합니다.

  ![프로세스 서버 3 추가](./media/site-recovery-add-process-server/ps-page-3.png)

   * Tooconnect hello 컴퓨터에서 현재 설정 hello 프록시를 사용 하려는 경우 선택 **기존 프록시 설정 사용 하 여 연결**합니다.
   * Hello 공급자 tooconnect을 직접 하려는 경우 선택 **프록시 없이 직접 연결**합니다.
   * Hello 기존 프록시 인증이 필요 하거나 hello 공급자 연결에 대 한 사용자 지정 프록시 toouse을 하려는 경우 선택 **사용자 지정 프록시 설정 사용 하 여 연결**합니다.

     * 사용자 지정 프록시를 사용 하는 경우 toospecify hello 주소, 포트 및 자격 증명 필요 합니다.
     * 프록시를 사용 하는 경우 해야 이미 허용한 액세스 toohello 서비스 url입니다.

5. **필수 구성 요소 확인**, 설치를 실행할 수 있는지는 확인 toomake 실행 됩니다. Hello에 대 한 경고가 나타나면 **동기화 확인이 글로벌 시간과**, hello 시스템 시계에 hello 시간을 확인 (**날짜 및 시간** 설정) hello 표준 시간대로 동일 hello 됩니다.

     ![프로세스 서버 4 추가](./media/site-recovery-add-process-server/ps-page-4.png)

6. **환경 정보**tooreplicate VMware Vm 거 여부를 선택 합니다. 복제할 경우 설치 프로그램에서 PowerCLI 6.0이 설치되어 있는지 확인합니다.

     ![프로세스 서버 5 추가](./media/site-recovery-add-process-server/ps-page-5.png)

7. **설치 위치**tooinstall hello 이진 파일을 hello 캐시를 저장 하는 경우 선택 합니다. 선택한 hello 드라이브에 5GB 이상의 사용 가능한 디스크 공간이 있어야 합니다. 하지만 600 g B 이상의 여유 공간이 있는 드라이브에 캐시 것이 좋습니다.
     ![프로세스 서버 5 추가](./media/site-recovery-add-process-server/ps-page-6.png)

8. **네트워크 선택**는 hello 구성 서버 보냅니다를 hello 수신기 (네트워크 어댑터 및 SSL 포트)를 지정 하 고 복제 데이터를 수신 합니다. 포트 9443 복제 트래픽의 주고받을에 사용 되는 hello 기본 포트는 하지만이 포트 번호 toosuit 사용자 환경 요구 사항을 수정할 수 있습니다. 또한 toohello 포트 9443에에서 웹 서버 tooorchestrate 복제 작업에 의해 사용 되는 포트 443을를 열 수도 있습니다. 복제 트래픽을 보내거나 받는 데 443 포트를 사용하면 안 됩니다.

     ![프로세스 서버 6 추가](./media/site-recovery-add-process-server/ps-page-7.png)
9. **요약**hello 정보 검토 하 고 클릭 **설치**합니다. 설치가 완료되면 암호가 생성됩니다. 복제를 사용하도록 설정할 때 필요하므로 암호를 복사하고 안전한 위치에 보관합니다.

     ![프로세스 서버 7 추가](./media/site-recovery-add-process-server/ps-page-8.png)
