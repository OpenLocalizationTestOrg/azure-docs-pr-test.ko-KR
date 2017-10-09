<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-maintenance-mode-hotfixes-via-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell을 통해 유지 관리 모드 핫픽스 tooinstall
> [!IMPORTANT]
> 유지 관리 모드에서 tooapply hello 핫픽스를 먼저 컨트롤러 하나에 필요 하 고에 다른 컨트롤러를 hello 합니다.
> 
> 

1. 유지 관리 모드로 hello 장치를 배치 합니다. 참조 [2 단계: 입력 유지 관리 모드](../articles/storsimple/storsimple-update-device.md#step2) 방법에 대 한 지침은 tooenter 유지 관리 모드입니다.
2. 형식 tooapply hello 핫픽스:
   
     `Start-HcsHotfix` 
3. 메시지가 표시 되 면 hello 경로 toohello 네트워크 공유 폴더 hello 핫픽스 파일이 포함 된를 제공 합니다.
4. 확인하라는 메시지가 표시됩니다. 형식 **Y** tooproceed hello 핫픽스를 설치 합니다.
5. 후 다른 컨트롤러 toohello 로그온 컨트롤러 하나에 hello 핫픽스를 적용 한 있습니다. Hello 이전 컨트롤러에 대해 수행한 것 처럼 hello 핫픽스를 적용 합니다.
6. Hello 핫픽스를 적용 한 후 유지 관리 모드를 종료 합니다. 지침은 [4단계: 유지 관리 모드 종료](../articles/storsimple/storsimple-update-device.md#step4) 를 참조하세요.

