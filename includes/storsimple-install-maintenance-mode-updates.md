<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell을 통해 tooinstall 유지 관리 모드 업데이트
1. 아직 수행 하지 않은 경우 선택 옵션 1, 및 hello 장치 직렬 콘솔에 액세스 **전체 권한으로 로그인**합니다. 
2. Hello 암호를 입력 합니다. hello 기본 암호는 **Password1**합니다.
3. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
     `Get-HcsUpdateAvailability` 
4. 사용 가능한 업데이트가 있으면 및 중단 또는 중단 없는 hello 업데이트 되는지 여부를 알려 줍니다. tooapply 강제 업데이트를 유지 관리 모드로 tooput hello 장치가 필요합니다. 지침은 [2단계: 유지 관리 모드 전환](../articles/storsimple/storsimple-update-device.md#step2) 을 참조하세요.
5. 장치가 유지 관리 모드에 있을 때 hello 명령 프롬프트에 입력 합니다.`Start-HcsUpdate`
6. 확인하라는 메시지가 표시됩니다. Hello 업데이트를 확인 하 고 나면 현재 액세스 중인 hello 컨트롤러에 설치 됩니다. Hello 업데이트가 설치 된 후 hello 컨트롤러 다시 시작 됩니다. 
7. Hello 업데이트 상태를 모니터링 합니다. 형식:
   
    `Get-HcsUpdateStatus`
   
    경우 hello `RunInProgress` 은 `True`, hello 업데이트 진행 중입니다. 경우 `RunInProgress` 은 `False`, 해당 hello 업데이트가 완료 되었는지 나타냅니다.  
8. Hello 업데이트 hello 현재 컨트롤러에 설치 될 때 다시 시작 된 toohello 다른 컨트롤러를 연결 하 고 1 ~ 6 단계를 수행 합니다.
9. 두 컨트롤러를 모두 업데이트한 후 유지 관리 모드를 종료합니다. 지침은 [4단계: 유지 관리 모드 종료](../articles/storsimple/storsimple-update-device.md#step4) 를 참조하세요.

