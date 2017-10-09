#### <a name="toocreate-a-cloud-appliance"></a>클라우드 어플라이언스에 toocreate

1. Hello Azure 포털에서에서 toohello 이동 **StorSimple 장치 관리자** 서비스입니다.
2. Toohello 이동 **장치** 블레이드입니다. Hello 서비스 요약 블레이드에서 hello 명령 모음에서 **만들기 클라우드 어플라이언스에**합니다.
    ![StorSimple 클라우드 어플라이언스 만들기](./media/storsimple-8000-create-cloud-appliance-u2/sca-create1.png)
3. Hello에 **만들기 클라우드 어플라이언스에** 블레이드에서 hello 다음 세부 정보를 지정 합니다.
   
    ![StorSimple 클라우드 어플라이언스 만들기](./media/storsimple-8000-create-cloud-appliance-u2/sca-create2m.png)
   
   1. **이름** – 클라우드 어플라이언스에 대한 고유 이름입니다.
   2. **모델** -hello 클라우드 어플라이언스에의 hello 모델을 선택 합니다. 8010 장치는 30TB의 표준 저장소를 제공하는 반면, 8020에는 64TB의 Premium Storage가 있습니다. 백업에서 8010 toodeploy 항목 수준 검색 시나리오를 지정 합니다. 8020 toodeploy 높은 성능, 대기 시간이 짧은 워크 로드를 선택 하거나 재해 복구를 위한 보조 장치로 사용 합니다.
   3. **버전** -hello 클라우드 어플라이언스에의 hello 버전을 선택 합니다. hello 버전 hello 가상 디스크 이미지를 사용 하는 toocreate hello 클라우드 어플라이언스에 toohello 버전에 해당 합니다. 지정 된 hello 버전 hello 클라우드 어플라이언스에 결정 실제 장치 장애 조치 또는에서 복제는 것이 중요 hello 클라우드 어플라이언스에의 적절 한 버전을 만들어야 합니다.
   4. **가상 네트워크** -이 클라우드 어플라이언스에 있는 toouse 되도록 하는 가상 네트워크를 지정 합니다. 프리미엄 저장소를 사용 하는 경우 프리미엄 저장소 계정의 hello 함께 지원 되는 가상 네트워크를 선택 해야 합니다. hello 지원 되지 않는 가상 네트워크는 hello 드롭다운 목록에서 없게 됩니다. 지원되지 않는 가상 네트워크를 선택한 경우 경고 메시지가 표시됩니다.
   5. **서브넷** -hello 가상 네트워크를 선택에 따라, hello 드롭다운 목록 hello 연결 된 서브넷을 표시 합니다. 서브넷 tooyour 클라우드 장비를 할당 합니다.
   6. **저장소 계정** – 프로 비전 시 hello 클라우드 어플라이언스의 저장소 계정 toohold hello 이미지를 선택 합니다. 이 저장소 계정은 hello에 있어야 합니다. 클라우드 어플라이언스에 hello 및 가상 네트워크와 동일한 영역입니다. 하지 수 사용 해야 데이터 저장소에 대 한 실제 hello 또는 hello 클라우드 어플라이언스에 합니다. 기본적으로 새 저장소 계정은 이 용도로 만들어집니다. 그러나이 용도에 적합 한 저장소 계정을 이미 알고 있는 경우 hello 목록에서 선택할 수 있습니다. 프리미엄 클라우드 장비를 만드는 경우 hello 드롭다운 목록에만 프리미엄 저장소 계정이 표시 됩니다.
      
      > [!NOTE]
      > hello 클라우드 어플라이언스에 hello Azure 저장소 계정과 함께 작동할 수 있습니다.
    
   7. Microsoft 데이터 센터에서 클라우드 어플라이언스에 hello에 저장 된 hello 데이터를 호스팅하는 이해 하는 hello 확인란 tooindicate를 선택 합니다.
       * 물리적 장치만 사용하는 경우, 암호화 키는 사용자 장치와 함께 유지되므로 Microsoft는 해독할 수 없습니다.

       * 클라우드 장비를 사용 하는 경우 hello 암호화 키와 hello 암호 해독 키가 Microsoft Azure에 저장 됩니다. 자세한 내용은 [클라우드 어플라이언스를 사용하기 위한 보안 고려 사항](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security)을 참조하세요.
   8. 클릭 **만들기** tooprovision hello 클라우드 어플라이언스에 합니다. hello 장치 프로 비전 하는 약 30 분 toobe를 걸릴 수 있습니다. Hello 클라우드 어플라이언스에 성공적으로 만들어지면 알림이 표시 됩니다. TooDevices 블레이드로 이동 하 고 장치의 목록을 hello toodisplay hello 클라우드 어플라이언스에 새로 고칩니다. 키를 누릅니다. hello 어플라이언스의 hello 상태는 **를 tooset 준비**합니다.
      
      ![StorSimple 클라우드 어플라이언스에 준비 tooset를](./media/storsimple-8000-create-cloud-appliance-u2/sca-create3.png)

