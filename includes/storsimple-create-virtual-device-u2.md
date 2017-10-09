#### <a name="toocreate-a-virtual-device"></a>toocreate 가상 장치
1. Hello Azure 포털에서에서 toohello 이동 **StorSimple Manager** 서비스입니다.
2. Toohello 이동 **장치** 페이지. 클릭 **가상 장치 만들기** hello hello 맨 아래에 **장치** 페이지.
3. Hello에 **가상 장치 만들기 대화 상자**, hello 다음 세부 정보를 지정 합니다.
   
    ![StorSimple 가상 장치 만들기](./media/storsimple-create-virtual-device-u2/CreatePremiumsva1.png)
   
   1. **이름** – 가상 장치에 대한 고유 이름입니다.
   2. **모델** -hello 가상 장치의 hello 모델을 선택 합니다. 이 필드는 업데이트 2 이상을 실행하는 경우에만 표시됩니다. 8010 장치 모델은 30TB의 표준 저장소를 제공하는 반면, 8020에는 64TB의 프리미엄 저장소가 있습니다. 백업에서
   3. 백업에서 toodeploy 항목 수준 검색 시나리오입니다. 8020 toodeploy 고성능 선택, 대기 시간이 짧은 작업 또는 재해 복구를 위한 보조 장치로 사용 합니다.
   4. **버전** -hello 가상 장치의 hello 버전을 선택 합니다. 8020 장치 모델을 선택 하면 다음 hello 버전 필드 표시 되지 않습니다 toohello 사용자입니다. 이 옵션은 없거나 1 (또는 이상)이이 서비스에 등록 된 장치에서 업데이트를 실행 중인 모든 실제 hello 하는 경우. 사전 업데이트 1의 혼합 되어 업데이트 1 실제 장치에 등록 된 hello 동일한 경우에이 필드는 표시 서비스입니다. Hello 가상 장치의 버전 hello 지정한 할 수 있습니다는 실제 장치를 결정 합니다 장애 조치 또는 복제에는 적절 한 버전의 hello 가상 장치를 만들어야 합니다. 선택:
      
      * 업데이트 0.3 이상을 실행하는 물리적 장치에서 장애 조치(Failover)하거나 DR하려는 경우 버전 업데이트 0.3을 선택합니다. 
      * 업데이트 1 이상을 실행하는 물리적 장치에서 장애 조치(Failover)하거나 복제하려는 경우 버전 업데이트 1을 선택합니다. 
   5. **가상 네트워크** –이 가상 장치에 toouse 되도록 하는 가상 네트워크를 지정 합니다. 프리미엄 저장소 (업데이트 2 이상)를 사용 하는 경우 프리미엄 저장소 계정의 hello 함께 지원 되는 가상 네트워크를 선택 해야 합니다. hello 드롭다운 목록에서 지원 되지 않는 hello 가상 네트워크는 회색입니다. 지원되지 않는 가상 네트워크를 선택한 경우 경고 메시지가 표시됩니다. 
   6. **가상 장치 생성을 위한 저장소 계정** – 프로 비전 시 hello 가상 장치의 저장소 계정 toohold hello 이미지를 선택 합니다. 이 저장소 계정은 hello에 있어야 합니다. 가상 장치 hello 및 가상 네트워크와 동일한 영역입니다. 하지 수 사용 해야 데이터 저장소에 대 한 hello 물리적 또는 가상 장치 hello 합니다. 기본적으로 새 저장소 계정은 이 용도로 만들어집니다. 그러나이 용도에 적합 한 저장소 계정을 이미 알고 있는 경우 hello 목록에서 선택할 수 있습니다. 프리미엄 가상 장치를 만드는 경우 hello 드롭다운 목록에는 프리미엄 저장소 계정이 표시 됩니다. 
      
      > [!NOTE]
      > 가상 장치 hello hello Azure 저장소 계정으로 작동할 수 있습니다. 클라우드 서비스와 같은 다른 공급자 Amazon, HP, 및 OpenStack (지원 되는 hello 물리적 장치에 대 한) hello StorSimple 가상 장치에 대 한 지원 되지 않습니다.
      > 
      > 
   7. Hello 가상 장치에 저장 된 hello 데이터는 Microsoft 데이터 센터에서 호스팅된다는 이해 하는 hello 확인 표시가 tooindicate를 클릭 합니다. 물리적 장치만 사용하는 경우, 암호화 키는 사용자 장치와 함께 유지되므로 Microsoft는 해독할 수 없습니다. 
      
       가상 장치를 사용 하 여 hello 암호화 키와 hello 암호 해독 키가 Microsoft Azure에 저장 됩니다. 자세한 내용은 [가상 장치를 사용하기 위한 보안 고려 사항](../articles/storsimple/storsimple-security.md#storsimple-virtual-device-security)을 참조하세요.
   8. Hello 검사 아이콘 toocreate hello 가상 장치를 클릭 합니다. hello 장치 프로 비전 하는 약 30 분 toobe를 걸릴 수 있습니다.
      
      ![StorSimple 가상 장치 만들기 단계](./media/storsimple-create-virtual-device-u2/StorSimple_VirtualDeviceCreating1M.png)

