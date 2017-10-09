<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>1 단계: 장치 toochange hello 서비스 데이터 암호화 키를 hello Azure 클래식 포털에서에서 권한 부여
일반적으로 장치 관리자에 게 서비스 관리자에 게 해당 장치 toochange 서비스 데이터 암호화 키 권한 부여를 요청 합니다. 서비스 관리자에 게 hello 장치 toochange hello 키를 승인 합니다.

이 단계는 hello Azure 클래식 포털에서에서 수행 됩니다. 서비스 관리자에 게 권한이 부여 적격 toobe 있는 hello 장치의 표시 된 목록에서 장치를 선택할 수 있습니다. hello 장치가 다음 권한이 있는 toostart hello 서비스 데이터 암호화 키 변경 프로세스입니다.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Toochange 서비스 데이터 암호화 키를 권한이 있는 장치 수 있습니까?
장치에 권한이 부여 된 tooinitiate 서비스 데이터 암호화 키 변경 되기 전 조건 다음 hello를 충족 해야 합니다.

* hello 장치 온라인 toobe 서비스 데이터 암호화 키 변경 권한 부여에 적합 해야 합니다.
* 같은 장치 다시 30 분 후 hello 키 변경 시작 되지 않았습니다 hello 권한을 부여할 수 있습니다.
* Hello 이전에 인증 된 장치에 의해 hello 키 변경 시작 되지 않았습니다는 다른 장치를 인증할 수 있습니다. Hello 새 장치에 권한이 부여 되 후 hello 이전 장치 hello 변경을 시작할 수 없습니다.
* Hello 서비스 데이터 암호화 키의 hello 롤오버가 진행 중인 동안에 장치를 인증할 수 없습니다.
* Hello 서비스에 등록 된 hello 장치 롤오버 않은 hello 암호화 되지 않은 다른 경우에 장치를 인증할 수 있습니다. 이러한 경우 hello 적합 한 장치는 hello hello 서비스 데이터 암호화 키 변경을 완료 한 장치입니다.

> [!NOTE]
> Azure 클래식 포털 hello StorSimple 가상 장치 hello 목록이 될 수 있는 장치에 표시 되지 않습니다 toostart hello 키를 변경할 권한이 부여 됩니다.
> 
> 

Hello 단계 tooselect 다음을 수행 하 고 장치 tooinitiate hello 서비스 데이터 암호화 키 변경 권한을 부여 합니다.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize 장치 toochange hello 키
1. Hello 서비스 대시보드 페이지에서 클릭 **서비스 데이터 암호화 키 변경**합니다.
   
    ![서비스 암호화 키 변경](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. Hello에 **서비스 데이터 암호화 키 변경** 대화 상자를 선택 하 고 장치 tooinitiate hello 서비스 데이터 암호화 키 변경 권한을 부여 합니다. hello 드롭 다운 목록에는 권한을 부여할 수 있는 모든 hello 적격 장치에 있습니다.
3. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png)에서도 확인할 수 있습니다.

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>2 단계: StorSimple tooinitiate hello 서비스 데이터 암호화 키 변경에 대 한 Windows PowerShell 사용
이 단계는 StorSimple 인터페이스 hello에 권한이 StorSimple 장치에 대 한 hello Windows PowerShell에서에서 수행 됩니다.

> [!NOTE]
> Hello 키 롤오버가 완료 될 때까지 어떤 작업도 hello StorSimple 관리자 서비스의 Azure 클래식 포털에서에서 수행할 수 있습니다.
> 
> 

Hello 장치 직렬 콘솔 tooconnect toohello Windows PowerShell 인터페이스를 사용 하는 경우 hello 다음 단계를 수행 합니다.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>tooinitiate hello 서비스 데이터 암호화 키 변경
1. 에 대 한 모든 권한을 toolog 옵션 1 선택 합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Hello cmdlet 성공적으로 완료 되 면 새 서비스 데이터 암호화 키를 받아볼 수 있습니다. 이 키를 복사하고 저장해 두었다가 이 프로세스의 3단계에서 사용합니다. 이 키는 tooupdate hello StorSimple Manager 서비스에 등록 된 장치에 남은 모든 hello를 사용 합니다.
   
   > [!NOTE]
   > 이 프로세스는 StorSimple 장치에 권한을 부여한 후 4시간 이내에 시작되어야 합니다.
   > 
   > 
   
   이 새 키는 toohello 푸시 toobe tooall hello 장치를 서비스 hello 서비스에 등록 된 전송 됩니다. Hello 서비스 대시보드에 경고가 표시 됩니다. hello 서비스는 hello 등록 된 장치에서 모든 hello 작업이 비활성화 됩니다 한 장치 관리자에 게는 다음 tooupdate hello 서비스 데이터 암호화 키 hello에 다른 장치 합니다. 그러나 hello (toohello 클라우드 데이터를 보내는 호스트) i/o가 중단 되지 않습니다.
   
   설정한 경우 단일 장치 등록 서비스 tooyour hello 롤오버 프로세스가 완료 되었으므로 이제 고 hello 다음 단계를 건너뛸 수 있습니다. 를 여러 장치 등록된 tooyour 서비스가 있는 경우에 3 toostep을 진행 합니다.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>3 단계: hello 다른 StorSimple 장치에서 서비스 데이터 암호화 키 업데이트
장치 등록된 tooyour StorSimple Manager 서비스를 여러 개 있는 경우 다음이 단계를 StorSimple 장치의 hello Windows PowerShell 인터페이스에서 수행 되어야 합니다. 2 단계에서에서 적어 둔 hello 키: StorSimple tooinitiate hello 서비스 데이터 암호화 키 변경에 대 한 Windows PowerShell을 사용 하 여 hello StorSimple Manager 서비스에 등록 된 StorSimple 장치에 남은 모든 hello 사용된 tooupdate 이어야 합니다.

Hello 단계 tooupdate hello 서비스 데이터 암호화 장치에서 다음을 수행 합니다.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>tooupdate hello 서비스 데이터 암호화 키
1. StorSimple tooconnect toohello 콘솔에 대 한 Windows PowerShell을 사용 합니다. 에 대 한 모든 권한을 toolog 옵션 1 선택 합니다.
2. Hello 명령 프롬프트에서 다음을 입력 합니다.
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Hello 서비스 데이터 암호화 키에서 가져온 제공 [2 단계: StorSimple tooinitiate hello 서비스 데이터 암호화 키 변경에 대 한 Windows PowerShell을 사용 하 여](#to-initiate-the-service-data-encryption-key-change)합니다.

