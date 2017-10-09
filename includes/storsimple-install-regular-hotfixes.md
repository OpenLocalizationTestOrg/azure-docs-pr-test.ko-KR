<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a>StorSimple 용 Windows PowerShell을 통해 tooinstall 정기적인 핫픽스
1. Toohello 장치 직렬 콘솔을 연결 합니다. 자세한 내용은 참조 [1 단계: toohello 직렬 콘솔 연결](../articles/storsimple/storsimple-update-device.md#step1)합니다.
2. Hello 직렬 콘솔 메뉴에서 옵션 1, 선택 **전체 권한으로 로그인**합니다. Hello 암호를 입력 합니다. hello 기본 암호는 **Password1**합니다.
3. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > 이 명령은 tooregular 핫픽스만을 적용 됩니다. 컨트롤러 하나에서만 이 명령을 실행하면 두 컨트롤러가 모두 업데이트됩니다.
    > 컨트롤러 장애 조치 hello 업데이트 과정; 표시 될 수도 있습니다. 그러나 시스템 가용성이 나 작동 hello 장애 조치 변경 되지 않습니다.

4. 메시지가 표시 되 면 hello 경로 toohello 네트워크 공유 폴더 hello 핫픽스 파일이 포함 된를 제공 합니다.
5. 확인하라는 메시지가 표시됩니다. 형식 **Y** tooproceed hello 핫픽스를 설치 합니다.

