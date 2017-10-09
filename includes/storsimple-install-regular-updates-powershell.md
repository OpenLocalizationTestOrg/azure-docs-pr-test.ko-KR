<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell을 통해 tooinstall 정기적으로 업데이트
1. Hello 장치 직렬 콘솔을 열고 선택 옵션 1, **전체 권한으로 로그인**합니다. Hello 암호를 입력 합니다. hello 기본 암호는 *Password1*합니다. 
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
     `Get-HcsUpdateAvailability`
   
    사용 가능한 업데이트가 있으면 및 중단 또는 중단 없는 hello 업데이트 되는지 여부를 알려 줍니다.
3. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
     `Start-HcsUpdate`
   
    hello 업데이트 프로세스가 시작 됩니다.

> [!IMPORTANT]
> * 이 명령은 tooregular 업데이트에만 적용 됩니다. 컨트롤러 하나에서만 이 명령을 실행하면 두 컨트롤러가 모두 업데이트됩니다. 
> * 컨트롤러 장애 조치 hello 업데이트 과정; 표시 될 수도 있습니다. 그러나 시스템 가용성이 나 작동 hello 장애 조치 변경 되지 않습니다.
> 
> 

