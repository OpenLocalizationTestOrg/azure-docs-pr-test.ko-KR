# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>증분 스냅숏을 사용하여 Azure 관리되지 않는 VM 디스크 백업
## <a name="overview"></a>개요
Azure 저장소 blob의 스냅숏도 tootake hello 기능을 제공합니다. 스냅숏 시간 해당 시점에 hello blob 상태를 캡처합니다. 이 문서에서는 스냅숏을 사용하여 가상 컴퓨터 디스크의 백업을 유지 관리할 수 있는 시나리오에 대해 설명합니다. Toouse 하지 않으려는 경우이 방법을 사용할 수 있습니다 Azure 백업 및 복구 서비스 및 가상 컴퓨터 디스크에 대 한 사용자 지정 백업 전략 희망 toocreate 합니다.

Azure 가상 컴퓨터 디스크는 Azure 저장소에 페이지 Blob으로 저장됩니다. 이 문서에서 가상 컴퓨터 디스크에 대 한 백업 전략을 기술 하는 것을 이후 페이지 blob의 hello 컨텍스트에서 toosnapshots를 이라고 합니다. 스냅숏에 대해 자세히 toolearn 너무 참조[Blob의 스냅숏을 만드는](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)합니다.

## <a name="what-is-a-snapshot"></a>스냅숏은 무엇입니까?
Blob 스냅숏은 특정 시점에 캡처된 Blob의 읽기 전용 버전입니다. 스냅숏이 생성된 후에는 읽거나 복사하거나 삭제할 수 있지만 수정할 수는 없습니다. 스냅숏은 시점에 표시 된 대로 blob 방법을 tooback를 제공 합니다. 버전 2015-04-05 REST까지 hello 기능 toocopy 전체 스냅숏 해야 했습니다. Hello REST 버전 2015-07-08 이상에서 있습니다 수 증분 스냅숏 복사 합니다.

## <a name="full-snapshot-copy"></a>전체 스냅숏 복사
스냅숏 수 tooanother 저장소 계정을 hello 기본 blob의 blob tookeep 백업으로 복사 합니다. Hello blob tooan 복원 유사한 기본 blob에 대해 스냅숏을 복사할 수도 있습니다 이전 버전입니다. 한 저장소 계정 tooanother에서 스냅숏으로 복사 되 면 hello hello 기본 페이지 blob으로 동일한 공간을 차지 합니다. 따라서 한 저장소 계정 tooanother에서 전체 스냅숏 복사 느립니다. 고 hello 대상 저장소 계정에서 많은 공간을 사용 합니다.

> [!NOTE]
> 기본 blob tooanother 대상 hello를 복사 하는 경우 hello blob의 스냅숏은 hello 함께 복사 되지 않습니다. 마찬가지로, 한 복사본과 기본 blob을 덮어쓰는 경우 hello 기본 blob와 연결 된 스냅숏을 영향을 받지 않습니다 및 hello 기본 blob 이름을 그대로 유지 합니다.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>스냅숏을 사용하여 디스크 백업
가상 컴퓨터 디스크에 대 한 백업 전략 hello 디스크 또는 페이지 blob의 스냅숏을 정기적으로 있고 tooanother 저장소 계정 등의 도구를 사용 하 여 복사할 [Blob 복사](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) 작업 또는 [AzCopy](../articles/storage/common/storage-use-azcopy.md)합니다. 다른 이름으로 스냅숏 tooa 대상 페이지 blob을 복사할 수 있습니다. hello 결과 대상 페이지 blob에 쓰기 가능한 페이지 blob 이며 스냅숏이 아닙니다. 이 문서의 뒷부분에 나오는 단계 tootake 백업 스냅숏을 사용 하 여 가상 컴퓨터 디스크의 설명입니다.

### <a name="restore-disks-using-snapshots"></a>스냅숏을 사용하여 디스크 복원
시간 toorestore 디스크 tooa hello 백업 스냅숏 중 하나에서 이전에 캡처된 버전 안정적 이면 hello 기본 페이지 blob를 통해 스냅숏을 복사할 수 있습니다. Hello 스냅숏이 승격된 toohello 기본 페이지 blob를 되 면 hello 스냅숏은 그대로 유지 하지만 수 모두 읽고 쓸 수 있는 복사본으로 원본을 덮어씁니다. 이 문서의 뒷부분에 나오는 단계 toorestore 스냅숏에서 해당 디스크의 이전 버전을 설명 합니다.

### <a name="implementing-full-snapshot-copy"></a>전체 스냅숏 복사 구현
Hello 다음을 수행 하 여 전체 스냅숏 복사본을 구현할 수 있습니다.

* Hello를 사용 하 여 hello 기본 blob의 스냅숏을 먼저 [스냅숏 Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob) 작업 합니다.
* 그런 다음 복사 hello tooa 대상 저장소 계정을 사용 하 여 스냅숏 [Blob 복사](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob)합니다.
* 기본 blob의이 프로세스 toomaintain 백업 복사본을 반복 합니다.

## <a name="incremental-snapshot-copy"></a>증분 스냅숏 복사
hello의 새로운 기능 hello [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) API는 페이지 blob의 스냅숏 hello 훨씬 더 나은 방법은 tooback를 제공 합니다. hello API 변경 내용 목록은 hello 사이의 반환 hello 기본 blob와 hello 스냅숏을 hello 백업 계정에 사용 되는 저장 공간의 hello 크기 감소 합니다. hello API 프리미엄 저장소: 표준 저장소에 페이지 blob을 지원합니다. 이 API를 사용하여 Azure VM에 대한 빠르고 효율적인 백업 솔루션을 빌드할 수 있습니다. 이 API는 사용할 수 있는 hello REST 버전 2015-07-08 이상 됩니다.

증분 스냅숏 복사본에서 저장소 계정 tooanother hello 경우의 차이점, toocopy 수 있습니다.

* 기본 Blob과 해당 스냅숏 또는
* Hello 기본 blob의 스냅숏도 모두 두 개의

제공 된 hello 다음 조건이 충족 되 면

* 1 월 1-2016 년 이후에 hello blob은 만들었습니다.
* hello blob로 덮어쓰이 하지 [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) 또는 [Blob 복사](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob) 두 스냅숏 사이입니다.

**참고**: 이 기능은 프리미엄 및 표준 Azure 페이지 Blob에 대해 사용할 수 있습니다.

스냅숏을 사용 하 여 사용자 지정 백업 전략을 사용 하는 경우 hello 스냅숏 복사 한 저장소 계정 tooanother에서 느려질 수 있습니다 및 저장소 공간을 사용할 수 있습니다. Hello 전체 스냅숏 tooa 백업 저장소 계정, 복사 하는 대신 hello 차이 연속 된 스냅숏 tooa 백업 페이지 blob 작성할 수 있습니다. 이러한 방식으로 hello 시간 toocopy 및 hello 공간 toostore 백업은 크게 감소 됩니다.

### <a name="implementing-incremental-snapshot-copy"></a>증분 스냅숏 복사 구현
Hello 다음을 수행 하 여 증분 스냅숏 복사본을 구현할 수 있습니다.

* 사용 하 여 hello 기본 blob의 스냅숏을 [스냅숏 Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob)합니다.
* 복사 hello toohello 대상 백업 저장소 계정을 사용 하 여 스냅숏 [Blob 복사](https://docs.microsoft.com/rest/api/storageservices/Copy-Blob)합니다. 이 hello 백업 페이지 blob입니다. Hello 백업 페이지 blob의 스냅숏을 만들고 hello 백업 계정에 저장 합니다.
* 스냅숏 Blob를 사용 하 여 hello 기본 blob의 다른 스냅숏을 생성 합니다.
* Hello 사용 하 여 hello 기본 blob의 hello 첫 번째 및 두 번째 스냅숏의 차이점이 가져오기 [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges)합니다. Hello 새 매개 변수를 사용 하 여 **prevsnapshot**, toospecify hello와 tooget hello 차이 원하는 hello 스냅숏의 날짜/시간 값입니다. 이 매개 변수가 있는 경우 나머지 응답 hello 대상 스냅숏과 일반 페이지를 포함 하 여 이전 스냅숏 간의 변경 된 hello 페이지만 포함 됩니다.
* 사용 하 여 [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) tooapply 이러한 변경 내용 toohello 백업 페이지 blob입니다.
* 마지막으로 hello 백업 페이지 blob의 스냅숏을 만들고 hello 백업 저장소 계정에 저장 합니다.

Hello 다음 섹션에서 설명할 자세히 증분 스냅숏 복사본을 사용 하 여 디스크의 백업을 유지 관리할 수 있습니다.

## <a name="scenario"></a>시나리오
이 섹션에서는 스냅숏을 사용하여 가상 컴퓨터 디스크에 대한 사용자 지정 백업 전략을 포함하는 시나리오에 대해 설명합니다.

프리미엄 저장소 P30 디스크가 연결된 DS 시리즈 Azure VM을 고려합니다. 라는 hello P30 디스크 *mypremiumdisk* 호출 프리미엄 저장소 계정에 저장 된 *mypremiumaccount*합니다. 표준 저장소 계정 이라는 *mybackupstdaccount* 의 hello 백업을 저장 하는 데 사용 되는 *mypremiumdisk*합니다. 스냅숏을 tookeep 같은의 *mypremiumdisk* 12 시간 간격입니다.

저장소 계정 및 디스크를 만드는 방법에 대해 toolearn 너무 참조[에 대 한 Azure 저장소 계정](../articles/storage/storage-create-storage-account.md)합니다.

Azure Vm을 백업 하는 방법에 대 한 toolearn 너무 참조[계획 Azure VM 백업을](../articles/backup/backup-azure-vms-introduction.md)합니다.

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>증분 스냅숏을 사용 하 여 디스크의 단계 toomaintain 백업
hello 다음과 같은 단계로 진행 방법의 tootake 스냅숏을 *mypremiumdisk* 에서 hello 백업을 유지 관리 및 *mybackupstdaccount*합니다. hello 백업이 표준 페이지 blob 이라는 *mybackupstdpageblob*합니다. hello 백업 페이지 blob 항상 반영의 마지막 스냅숏이 hello 상태 동일 hello *mypremiumdisk*합니다.

1. 프리미엄 저장소 디스크에 대 한 hello 백업 페이지 blob의 스냅숏을 수행 하 여 만들 *mypremiumdisk* 호출 *mypremiumdisk_ss1*합니다.
2. 이 스냅숏 toomybackupstdaccount 라는 페이지 blob으로 복사 *mybackupstdpageblob*합니다.
3. [스냅숏 Blob](https://docs.microsoft.com/rest/api/storageservices/Snapshot-Blob)을 사용하여 *mybackupstdpageblob_ss1*이라는 *mybackupstdpageblob*의 스냅숏을 만들고 *mybackupstdaccount*에 저장합니다.
4. Hello 백업 시간 동안 생성의 다른 스냅숏을 *mypremiumdisk*, 예: *mypremiumdisk_ss2*에 저장 *mypremiumaccount*합니다.
5. Hello 두 스냅숏 사이의 hello 증분 변경 내용을 *mypremiumdisk_ss2* 및 *mypremiumdisk_ss1*를 사용 하 여 [GetPageRanges](https://docs.microsoft.com/rest/api/storageservices/Get-Page-Ranges) 에  *mypremiumdisk_ss2* hello로 **prevsnapshot** 매개 변수 설정의 타임 스탬프 toohello *mypremiumdisk_ss1*합니다. 이러한 증분 변경을 toohello 백업 페이지 blob 쓰기 *mybackupstdpageblob* 에 *mybackupstdaccount*합니다. Hello 증분 변경에서 삭제 된 범위 인 hello 백업 페이지 blob에서 해제 해야 합니다. 사용 하 여 [PutPage](https://docs.microsoft.com/rest/api/storageservices/Put-Page) toowrite 증분 변경 내용 toohello 백업 페이지 blob입니다.
6. Hello 백업 페이지 blob의 스냅숏을 *mybackupstdpageblob*라는 *mybackupstdpageblob_ss2*합니다. Hello 이전 스냅숏을 삭제 *mypremiumdisk_ss1* 프리미엄 저장소 계정에서 합니다.
7. 백업 창마다 4~6단계를 반복합니다. 이러한 방식으로 표준 저장소 계정에서 *mypremiumdisk* 의 백업을 유지할 수 있습니다.

![증분 스냅숏을 사용하여 디스크 백업](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>단계 toorestore 스냅숏에서 디스크
다음 단계 hello, toorestore 프리미엄 디스크를 hello 하는 방법에 대해 설명 *mypremiumdisk* hello 백업 저장소 계정에서 스냅숏 이전 tooan *mybackupstdaccount*합니다.

1. 시간을 toorestore hello 프리미엄 디스크를 hello 시점을 식별 합니다. 스냅숏 있는지 경우를 가정해 *mybackupstdpageblob_ss2*, hello 백업 저장소 계정에 저장 되어 *mybackupstdaccount*합니다.
2. Mybackupstdaccount, 승격 hello 스냅숏 *mybackupstdpageblob_ss2* hello 새 백업 기본 페이지 blob으로 *mybackupstdpageblobrestored*합니다.
3. *mybackupstdpageblobrestored_ss1*이라는 이 복원된 백업 페이지 Blob의 스냅숏을 만듭니다.
4. 복원 하는 hello 페이지 blob 복사 *mybackupstdpageblobrestored* 에서 *mybackupstdaccount* 너무*mypremiumaccount* hello 새로운 프리미엄 디스크와  *mypremiumdiskrestored*합니다.
5. 향후 증분 백업을 만들기 위해 *mypremiumdiskrestored_ss1*이라는 *mypremiumdiskrestored*의 스냅숏을 만듭니다.
6. Hello DS 시리즈 VM 복원 toohello 디스크 가리킨 *mypremiumdiskrestored* 및 이전 hello 분리 *mypremiumdisk* hello VM에서에서 합니다.
7. 복원 하는 hello 디스크에 대 한 이전 섹션에서 설명한 hello 백업 프로세스를 시작 *mypremiumdiskrestored*, hello를 사용 하 여 *mybackupstdpageblobrestored* hello 백업 페이지 blob으로 합니다.

![스냅숏에서 디스크 복원](../articles/virtual-machines/windows/media/incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>다음 단계
사용 하 여 hello 다음 blob의 스냅숏 만들기 및 VM 백업 인프라를 계획 하는 방법에 대 한 자세한 toolearn을 연결 합니다.

* [Blob의 스냅숏 만들기](https://docs.microsoft.com/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)
* [VM 백업 인프라 계획](../articles/backup/backup-azure-vms-introduction.md)

