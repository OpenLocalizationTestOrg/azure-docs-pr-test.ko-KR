<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> SharePoint RBS 구성에 대 한 변경 내용을 toohello StorSimple 어댑터를 만들 때 toohello Domain Admins 그룹에 속하는 사용자 계정으로 로그온 해야 합니다. 또한 hello 구성 페이지 hello 중앙 관리 같은 호스트에서 실행 되는 브라우저에서 액세스 해야 합니다.
> 
> 

#### <a name="tooconfigure-rbs"></a>RBS tooconfigure
1. Hello SharePoint 중앙 관리 페이지를 열고 너무 찾아보기**시스템 설정**합니다. 
2. Hello에 **Azure StorSimple** 섹션에서 클릭 **StorSimple 어댑터 구성**합니다.
   
    ![Hello StorSimple 어댑터 구성](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. Hello에 **StorSimple 어댑터 구성** 페이지:
   
   1. 해당 hello 있는지 확인 **경로 편집 사용** 확인란을 선택 합니다.
   2. Hello 텍스트 상자에 hello BLOB 저장소의 hello 범용 명명 규칙 (UNC) 경로 입력 합니다.
      
      > [!NOTE]
      > hello BLOB 저장소 볼륨 hello StorSimple 장치에 구성 된 iSCSI 볼륨에서 호스팅해야 합니다.

   3. Hello 클릭 **사용** 각 원격 저장소에 대 한 tooconfigure 되도록 hello 콘텐츠 데이터베이스 아래 단추입니다.
      
      > [!NOTE]
      > hello BLOB 저장소에 공유 하 고 연결할 모든 웹 프런트 엔드 (WFE) 서버에 의해 여야 합니다. 및 hello SharePoint 서버 팜에 대해 구성 된 hello 사용자 계정 액세스 toohello 공유에 있어야 합니다.
      
      ![Hello RBS 공급자를 사용 하도록 설정](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      RBS를 사용 하지 않도록 설정 하거나 설정할 때 hello 메시지의 뒤에 나타납니다.
      
      ![StorSimple 어댑터 사용 또는 사용 안함 구성](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Hello 클릭 **업데이트** 단추 tooapply hello 구성 합니다. Hello를 클릭할 때 **업데이트** 단추를 hello RBS 구성 상태가 모든 WFE 서버에서 업데이트 되 고 hello 전체 팜에서 RBS 사용 하도록 설정 됩니다. hello 메시지의 뒤에 나타납니다.
      
      ![어댑터 구성 메시지](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > 매우 많은 (200 보다 큼) 데이터베이스와 SharePoint 팜에 대해 RBS를 구성 하는 경우 hello SharePoint 중앙 관리 웹 페이지 시간이 초과 될 수 있습니다. 이 경우 hello 페이지를 새로 고칩니다. Hello 구성 프로세스에는 영향을 주지 않습니다.

4. Hello 구성을 확인 하십시오.
   
   1. Toohello SharePoint 중앙 관리 웹 사이트에 로그인 하 고 toohello 찾아보기 **StorSimple 어댑터 구성** 페이지.
   2. Hello 구성 세부 정보 toomake hello 설정을 입력 한 일치 하는지 확인 합니다. 
5. RBS가 올바르게 작동하는지 확인합니다.
   
   1. 문서 tooSharePoint 업로드 합니다. 
   2. 사용자가 구성한 toohello UNC 경로를 찾습니다. Hello RBS 디렉터리 구조를 만든 다음 업로드 hello 개체 포함 하 고 있는지 확인 합니다.
6. (선택 사항) Hello Microsoft RBS를 사용할 수 있습니다 `Migrate()` SharePoint toomigrate 기존 BLOB 콘텐츠 toohello StorSimple 장치에 포함 된 PowerShell cmdlet. 자세한 내용은 참조 [로 또는 SharePoint 2013에서 RBS에서 콘텐츠를 마이그레이션하고] [ 6] 또는 [로 또는 RBS (SharePoint Foundation 2010)에서 콘텐츠를 마이그레이션하고] [7].
7. (선택 사항) 테스트 설치 시 hello Blob 다음과 같이 hello 콘텐츠 데이터베이스 외부로 이동 된 확인할 수 있습니다. 
   
   1. SQL Management Studio를 시작합니다.
   2. 다음과 같이 hello ListBlobsInDB_2010.sql 또는 ListBlobsInDB_2013.sql 쿼리를 실행 합니다.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      RBS가 올바르게 구성 업로드 되어 RBS로 성공적으로 표면화 된 모든 개체에 대 한 hello SizeOfContentInDB 열에 NULL 값이 표시 됩니다.
8. (선택 사항) RBS를 구성 하 고 모든 BLOB 콘텐츠 toohello StorSimple 장치로 이동 hello 콘텐츠 데이터베이스 toohello 장치 이동할 수 있습니다. Toomove hello 콘텐츠 데이터베이스를 선택 하면 기본 볼륨으로 hello 장치에서 hello 콘텐츠 데이터베이스 저장소를 구성 하는 것이 좋습니다. 그런 다음 사용 하 여 SQL Server 모범 사례 toomigrate hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 설정 합니다. 
   
   > [!NOTE]
   > Hello StorSimple 8000 시리즈 (것은 지원 되지 않습니다 hello 5000 또는 7000 시리즈에 대 한)에 대 한 이동 hello 콘텐츠 데이터베이스 toohello 장치 에서만 지원 됩니다.
   
   Blob 및 콘텐츠 데이터베이스 hello hello StorSimple 장치의 별도 볼륨에 저장 하면 hello에 구성 하는 것이 좋습니다 같은 볼륨 컨테이너입니다. 이렇게 하면 같이 백업됩니다.
   
   > [!WARNING]
   > RBS를 설정 하지 않은 경우 hello 콘텐츠 데이터베이스 toohello StorSimple 장치를 이동 하지 않는 것이 좋습니다. 테스트되지 않은 구성입니다.
   
9. 다음 단계로 이동 toohello: [가비지 수집 구성](#configure-garbage-collection)합니다.

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
