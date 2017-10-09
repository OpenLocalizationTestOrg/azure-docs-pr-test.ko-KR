<!--author=alkohli last changed: 02/06/17-->

#### <a name="tooinstall-an-update-from-hello-azure-portal"></a>tooinstall hello Azure 포털의 업데이트

1. Hello StorSimple 서비스 페이지에서 장치를 선택 합니다. 너무 이동**장치** > **유지 관리**합니다.
2. Hello hello 페이지의 아래쪽에 있는 클릭 **업데이트 스캔**합니다. 작업은 사용 가능한 업데이트에 대 한 tooscan을 만들어집니다. Hello 작업이 성공적으로 완료 되었을 때 알림을 받습니다.
3. Hello에 **소프트웨어 업데이트** hello에 동일한 섹션 페이지 hello 새 소프트웨어 업데이트가 제공 됩니다. 장치에 대 한 업데이트를 적용 하기 전에 hello 릴리스 정보를 검토 하는 것이 좋습니다.
4. Hello hello 페이지의 아래쪽에 있는 클릭 **업데이트 설치**, 차례로 **확인**합니다.
5. Hello에 **업데이트 설치** 대화 상자는 hello 권장 사항에 따라 있는지 확인 한 후 선택 **hello 위의 요구 사항 이해 했으며 장치 준비 tooupgrade am** hello 확인을 클릭 하 고 단추입니다.
   
    ![확인 메시지](./media/storsimple-install-update2-via-portal/InstallUpdate12_2M.png)
6. 일련의 필수 조건 검사가 시작됩니다. 이들 검사는 다음과 같습니다.
   
   * **컨트롤러 상태 검사** tooverify 장치 컨트롤러를 hello 둘 다는 정상 상태이 고 온라인입니다.
   * **하드웨어 구성 요소 상태 검사** tooverify StorSimple 장치에서 하드웨어 구성 요소를 hello 모든 요소가 정상 상태입니다.
   * **데이터 0 확인** tooverify 장치에서 DATA 0은 사용 하도록 설정 합니다. 이 인터페이스를 사용하지 않는 경우 다음을 사용하도록 설정하고 다시 시도해야 합니다.
   * **데이터 2 및 DATA 3 검사** tooverify 네트워크 인터페이스 DATA 2 및 DATA 3은 사용할 수 없습니다. 이러한 인터페이스를 사용할 수 있으면이 사용 하지 않도록 설정을 하십시오 tooupdate 장치 해야 있습니다. 이 검사는 GA 소프트웨어를 실행하는 장치에서 업데이트 하는 경우에 수행됩니다. 0.1, 0.2, 또는 0.3 버전을 실행하는 장치에는 이 확인이 필요하지 않습니다.
   * **게이트웨이 검사** 모든 장치에서 버전 이전 tooUpdate 1을 실행 합니다. 이 검사 전 업데이트 1 소프트웨어를 실행 하는 모든 hello 장치에서 수행 하지만 이외의 DATA 0 네트워크 인터페이스에 대해 구성 된 게이트웨이 있는 hello 장치에 실패 합니다.
     
     hello 업데이트는 모든 검사를 성공적으로 완료 하는 경우에 적용 됩니다. Hello 검사가 진행 되는 경우 알림을 받습니다.
     
     ![사전 검사 알림](./media/storsimple-install-update2-via-portal/InstallUpdate12_3M.png)
     
     hello 예를 들면 hello 검사 하지 못했습니다. Hello 두 장치 컨트롤러가 모두 정상 상태이 고 온라인 되는지 확인 해야 합니다. Toocheck hello 상태 hello 하드웨어 구성 요소를 해야합니다. 이 예시에서는 컨트롤러 0과 컨트롤러 1 구성 요소에 주의가 필요합니다. 혼자서 이러한 문제를 해결 수 없는 경우 Microsoft 지원 toocontact을 할 수 있습니다.
     
       ![검사 실패](./media/storsimple-install-update2-via-portal/HCS_PreUpgradeChecksFailed-include.png)
7. Hello 검사를 성공적으로 완료 한 후 업데이트 작업이 생성 됩니다. Hello 업데이트 작업이 성공적으로 만들어지면 알림이 표시 됩니다.
   
    ![업데이트 작업 만들기](./media/storsimple-install-update2-via-portal/InstallUpdate12_44M.png)
   
    hello 업데이트를 장치에 적용 합니다.
    
8. hello 업데이트 작업의 toomonitor hello 진행률 클릭 **작업 보기**합니다. Hello에 **작업** 페이지 hello 업데이트 진행률을 볼 수 있습니다.
9. hello 업데이트는 몇 시간 toocomplete 합니다. Hello 업데이트 작업을 선택 하 고 클릭 **세부 정보** 언제 든 지 hello 작업의 tooview hello 세부 정보입니다.
10. Hello 작업이 완료 되 면 이동 toohello **유지 관리** 페이지 및 너무 아래로 스크롤하여**소프트웨어 업데이트**합니다.

