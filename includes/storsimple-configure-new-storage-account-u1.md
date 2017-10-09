<!--author=alkohli last changed: 9/17/15-->

#### <a name="tooadd-a-storage-account-in-storsimple-8000-series-update-10"></a>tooadd StorSimple 8000 시리즈 업데이트 1.0의 저장소 계정
1. Hello StorSimple 관리자 서비스 방문 페이지에서 서비스를 선택 하 고 두 번 클릭 합니다. 그러면 toohello **빠른 시작** 페이지. 선택 hello **구성** 페이지.
2. **저장소 계정 추가/편집**을 클릭합니다.
3. Hello에 **저장소 계정 추가/편집** 대화 상자를 클릭 **새로 추가**합니다.
4. Hello에 **공급자** 필드를 선택 하는 hello 적절 한 클라우드 서비스 공급자입니다. 지원 되는 hello 공급자는 Azure, Amazon S3, RR, HP 및 OpenStack Amazon S3입니다. Hello 자격 증명 및 연결 된 클라우드 서비스 공급자의 저장소 계정 hello hello 위치를 지정 합니다. 자격 증명을 제공 하는 hello 필드를 사용자가 지정한 hello 클라우드 서비스 공급자에 따라 달라질 수. 있습니다 
   
   * Azure 클라우드 서비스 공급자를 선택한 경우에 제공 hello **이름** 및 기본 hello **선택 키** Microsoft Azure 저장소 계정에 대 한 합니다. Azure 계정에 대 한 hello 위치 자동으로 채워집니다.
     
        ![Azure Storage 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddAzureStorageaccount-include.png)
   * Amazon S3 또는 Amazon S3 with RRS을 선택한 경우 친숙한 **저장소 계정 이름**, **액세스 키** 및 **비밀 키**를 제공합니다. Amazon S3 및 Amazon S3 RR으로 다음 위치 hello 지원 됩니다.
     
     * 미국 표준
     * 미국 서부(오리건)
     * 미국 서부(캘리포니아 북부)
     * EU(아일랜드)
     * 아시아 태평양(싱가포르)
     * 아시아 태평양(시드니)
     * 아시아 태평양(도쿄)
     * 남미(상파울루)
       
       ![Amazon 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddAmazonStorageaccount-include.png)
   * 클라우드 서비스 공급자로 HP를 선택한 경우, 친숙한 **저장소 계정 이름**, **테넌트 ID**, **사용자 이름** 및 **암호**를 제공합니다. HP, 다음 위치 hello 지원 됩니다.
     
     * 미국 동부
     * 미국 서부
       
       ![HP 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddHPStorageaccount-include.png)
   * **Openstack**을 클라우드 서비스 공급자로 선택한 경우, **호스트 이름**, **액세스 키** 및 **비밀 키**를 제공합니다.
     
     > [!NOTE]
     > Azure에서 제외 하 고 hello 클라우드 서비스 공급자, 모든에 대 한 이름을 허용 됩니다. 서로 다른 친숙 한 이름을 사용 하 고 자격 증명의 집합 동일 hello로 둘 이상의 저장소 계정을 만들 수 있습니다.
     > 
     > 
     
        ![Openstack 저장소 계정 추가](./media/storsimple-configure-new-storage-account-u1/AddOpenstackStorageaccount-include.png)
5. 선택 **SSL 모드 사용** toocreate 장치와 hello 클라우드 사이의 네트워크 통신을 위한 보안 채널입니다. 지우기 hello **SSL 모드 사용** 확인란 사설 클라우드 내에서 작동 하는 경우에 합니다.
   
   > [!NOTE]
   > HP를 공급자로 사용하는 경우 SSL을 항상 사용할 수 있습니다.
   > 
   > 
6. Hello 확인 아이콘을 클릭 합니다. ![확인 아이콘](./media/storsimple-configure-new-storage-account/HCS_CheckIcon-include.png)에서도 확인할 수 있습니다. Hello 저장소 계정이 정상적으로 만들어지면 알림이 표시 됩니다.
7. 새로 만든 저장소 계정 hello hello에 표시 될 **구성** 페이지 **저장소 계정은**합니다. 클릭 **저장** toosave hello 새 저장소 계정입니다. 확인하라는 메시지가 표시되면 **확인** 을 클릭합니다.

