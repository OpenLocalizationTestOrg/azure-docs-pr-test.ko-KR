<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>SharePoint 2010 tooSharePoint 2013 업그레이드 한 다음 SharePoint에 대 한 hello StorSomple 어댑터 설치
> [!IMPORTANT]
> 모든 이전에 RBS 통해 tooexternal 저장소 제공 됩니다 hello 업그레이드가 완료 될 때까지 옮겨진 파일 및 hello RBS 기능 다시 활성화 됩니다. toolimit 사용자에 영향을 줄, 업그레이드 또는 계획 된 유지 관리 기간 동안 다시 설치를 수행 합니다.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>SharePoint 2010 tooupgrade tooSharePoint 2013 및 hello 어댑터 설치
1. Hello BLOB 저장소 경로 hello에 대 한 참고 hello SharePoint 2010 팜에서 RBS를 사용할 수 있는 Blob 및 콘텐츠 데이터베이스 hello 표면화 합니다. 
2. 설치 하 고 hello 새 SharePoint 2013 팜을 구성 합니다. 
3. Hello SharePoint 2010 팜 toohello 새 SharePoint 2013 팜에서 데이터베이스, 응용 프로그램 및 사이트 모음을 이동 합니다. 자세한 내용은 이동 너무[hello 업그레이드 프로세스 tooSharePoint 2013 개요](https://technet.microsoft.com/library/cc262483.aspx)합니다.
4. Hello 새 팜에 SharePoint 용 StorSimple 어댑터 hello를 설치 합니다. 너무 이동[SharePoint 용 StorSimple 어댑터 설치 hello](#install-the-storsimple-adapter-for-sharepoint) 프로시저에 대 한 합니다.
5. 1 단계에서 적어 둔 hello 정보를 사용 하 여 동일한 콘텐츠 데이터베이스의 설정 하 고 동일한 BLOB hello SharePoint 2010 설치에 사용 된 경로 저장 하는 hello를 제공 하는 hello에 대 한 RBS를 설정 합니다. 너무 이동[RBS 구성](#configure-rbs) 프로시저에 대 한 합니다. 이 단계를 완료 한 후에 이전에 표면화 된 파일 hello 새 팜에서 액세스할 수 있어야 합니다. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>SharePoint 용 StorSimple 어댑터 업그레이드 hello
> [!IMPORTANT]
> 다음 이유로 hello에 대 한 계획 된 유지 관리 기간 동안이 업그레이드 toooccur를 예약 해야:
> 
> * 이전에 표면화 된 콘텐츠 hello 어댑터를 다시 설치 될 때까지 하지 제공 됩니다.
> * SharePoint 용 StorSimple 어댑터 hello의 hello 이전 버전을 제거 하 고 hello 새 버전을 설치 하기 전에 hello 콘텐츠 데이터베이스에 저장 됩니다 후 toohello 사이트를 업로드 하는 콘텐츠입니다. Hello 새 어댑터를 설치한 후 해당 콘텐츠 toohello StorSimple 장치 toomove 해야 합니다. Microsoft hello를 사용할 수 있습니다` RBS Migrate()` SharePoint toomigrate hello 콘텐츠에 포함 하는 PowerShell cmdlet입니다. 자세한 내용은 [RBS에서 콘텐츠 마이그레이션](https://technet.microsoft.com/library/ff628255.aspx)을 참조하세요. 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>tooupgrade hello SharePoint 용 StorSimple 어댑터
1. SharePoint 용 StorSimple 어댑터의 hello 이전 버전을 제거 합니다.
   
   > [!NOTE]
   > RBS hello 콘텐츠 데이터베이스에 자동으로 해제 됩니다. 그러나 기존 Blob hello StorSimple 장치에 유지 됩니다. RBS를 사용 하지 않도록 설정 하 고 hello Blob 백 toohello 마이그레이션된 콘텐츠 데이터베이스 적용 되지 않은 때문에 해당 Blob에 대 한 모든 요청이 실패 합니다. 
   > 
   > 
2. 설치는 SharePoint 용 StorSimple 어댑터 새 hello 합니다. hello 새로운 어댑터 이전에 사용 하도록 설정 하거나 rbs 사용 하지 않도록 설정 하는 hello 콘텐츠 데이터베이스를 자동으로 인식 됩니다와 hello 이전 설정을 사용 합니다.

