
## <a name="about-vhds"></a>VHD에 대하여

hello Azure에서 사용 되는 Vhd는 Azure의 표준 또는 프리미엄 저장소 계정에 페이지 blob으로 저장 된.vhd 파일입니다. 페이지 Blob에 대한 자세한 내용은 [블록 Blob 및 페이지 Blob 이해하기](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/)를 참조하세요. 프리미엄 저장소에 대한 자세한 내용은 [고성능 프리미엄 저장소와 Azure VM](../articles/storage/common/storage-premium-storage.md)을 참조하세요.

Azure는 디스크 VHD 형식의 고정 hello를 지원 합니다. hello 고정 형식 배치 디스크 오프셋 X가 blob 오프셋 X에 저장 되므로 hello 파일 내에 선형적으로 논리적 디스크 아웃 hello 합니다. Hello blob의 hello 끝에는 작은 바닥글이 hello VHD의 hello 속성을 설명합니다. 종종 hello 고정된 형식 대부분의 디스크에 큰 사용 하지 않는 범위 때문에 공간을 차지 합니다. 그러나 Azure에서는.vhd 파일 저장을 스파스 형식으로의 고정 두 hello hello 혜택을 받 및 hello에서 동적 디스크 동일 하므로 시간입니다. 자세한 내용은 [가상 하드 디스크 시작](https://technet.microsoft.com/library/dd979539.aspx)을 참조하세요.

소스 toocreate 디스크로 toouse 원하는 또는 읽기 전용 이미지는 Azure에서 모든.vhd 파일입니다. 디스크 또는 이미지를 만들 때 Azure에서는.vhd 파일을 hello의 복사본에 게 만듭니다. 이러한 복사본은 읽기 전용 또는 읽기 / 쓰기, VHD hello를 사용 하는 방법에 따라 수 있습니다.

이미지에서 가상 컴퓨터를 만들 때 Azure hello 원본.vhd 파일의 복사본 인 hello 가상 컴퓨터에 대 한 디스크를 만듭니다. 실수로 삭제 tooprotect, Azure 임대 이미지, 운영 체제 디스크 또는 데이터 디스크 toocreate가 사용 하는 모든 원본.vhd 파일에 배치 합니다.

원본.vhd 파일을 삭제 하려면 먼저 hello 디스크 또는 이미지를 삭제 하 여 tooremove hello 임대가 필요 합니다. toodelete 운영 체제 디스크로 가상 컴퓨터에서 사용 중인.vhd 파일을 삭제할 수 있습니다 hello 가상 컴퓨터, hello 운영 체제 디스크 및 원본.vhd 파일 hello 한 번에 모두 hello 가상 컴퓨터를 삭제 하 고 모든 관련된 디스크를 삭제 합니다. 그러나 데이터 디스크의 원본인 .vhd 파일을 삭제하려면 설정된 순서대로 몇 가지 단계를 수행해야 합니다. 먼저 hello 디스크 hello 가상 컴퓨터에서 다음 delete hello 디스크를 분리 한 다음 hello.vhd 파일을 삭제.

> [!WARNING]
> 저장소에서 원본 .vhd 파일을 삭제하거나, 사용자의 저장소 계정을 삭제한 경우, Microsoft는 해당 데이터를 복구할 수 없습니다.
> 

## <a name="types-of-disks"></a>디스크 유형 

Azure 디스크는 99.999% 가용성을 위해 설계되었습니다. Azure 디스크는 업계 최고의 0% 연간 실패율(Annualized Failure Rate)로 엔터프라이즈급 내구성을 일관되게 제공합니다.

디스크(Standard Storage 및 Premium Storage)를 만들 때 선택할 수 있는 저장소에는 두 가지 성능 계층이 있습니다. 또한 디스크에도 두 가지 유형(비관리 및 관리)이 있으며, 두 성능 계층 중 한 계층에 있을 수 있습니다.


### <a name="standard-storage"></a>Standard Storage 

Standard Storage는 HDD에 의해 지원되며 성능은 그대로이면서 비용 효율적인 저장소를 제공합니다. Standard Storage는 하나의 데이터센터에 로컬로 복제되거나 기본 및 보조 데이터센터와 함께 지역 중복 저장소가 될 수 있습니다. 저장소 복제에 대한 자세한 내용은 [Azure Storage 복제](../articles/storage/common/storage-redundancy.md)를 참조하세요. 

VM 디스크로 Standard Storage를 사용하는 방법에 대한 자세한 내용은 [Standard Storage 및 디스크](../articles/storage/common/storage-standard-storage.md)를 참조하세요.

### <a name="premium-storage"></a>Premium Storage 

Premium Storage는 SSD에 의해 지원되며 I/O 사용량이 많은 작업을 실행하는 VM을 위해 고성능의 낮은 대기 시간의 디스크를 지원합니다. Premium Storage는 DS, DSv2, GS, Ls 또는 FS 시리즈 Azure VM과 함께 사용할 수 있습니다. 자세한 내용은 [Premium Storage](../articles/storage/common/storage-premium-storage.md)를 참조하세요.

### <a name="unmanaged-disks"></a>관리되지 않는 디스크

관리 되지 않는 디스크는 Vm에서 사용 된 디스크의 hello 기존의 종류입니다. 이러한, 사용자 고유의 저장소 계정을 만들고 hello 디스크를 만드는 경우 해당 저장소 계정 지정 합니다. 너무 많은 디스크를 배치 하지 않는 있는지 toomake 있는 hello를 초과할 수 때문에 동일한 저장소 계정을 hello [확장성 목표](../articles/storage/common/storage-scalability-targets.md) Vm 제한 되 고 그 결과 hello의 hello 저장소 계정 (예: 20, 000 IOPS). 관리 되지 않는 디스크를 하나 이상의 저장소 계정 tooget hello 성능을 극대화 Vm의 toomaximize hello 사용법 아웃 toofigure를 해야 합니다.

### <a name="managed-disks"></a>관리 디스크 

Hello 저장소 계정 만들기/관리 hello 백그라운드로, 및의 hello 저장소 계정 확장성 제한 hello에 대 한 tooworry 있는지를 확인 하는 디스크 핸들을 관리 합니다. Hello 디스크 크기와 hello 성능 계층 (표준/프리미엄) 단순히 지정 하 고 Azure 위해 만들고 관리 hello 디스크 있습니다. 디스크를 더하거나 hello VM 확장 및 축소가 서 되더라도 tooworry hello 저장소 사용량에 대 한 필요는 없습니다. 

또한 Azure 지역 마다 하나의 저장소 계정에 사용자 지정 이미지를 관리 하 고 hello에 Vm의 toocreate 수백 사용 수 동일한 구독 합니다. 관리 되는 디스크에 대 한 자세한 내용은 hello를 참조 하십시오 [디스크 관리 개요](../articles/virtual-machines/windows/managed-disks-overview.md)합니다.

Azure 관리 되는 디스크를 사용 하 여 새 Vm에 대 한 및 변환 하는 hello tootake 활용 하면 이전 관리 되지 않는 디스크 toomanaged 디스크 많은 기능을 관리 하는 디스크에서 사용할 수 있는 것이 좋습니다.

### <a name="disk-comparison"></a>디스크 비교

다음 표에서 hello 비관리 코드와 어떤 toouse를 결정 하는 디스크 toohelp 관리 둘 다에 대 한 프리미엄 vs 표준의 비교를 제공 합니다.

|    | Azure Premium Disk | Azure Standard Disk |
|--- | ------------------ | ------------------- |
| 디스크 유형 | 반도체 드라이브(SSD) | 하드 디스크 드라이브 (HDD)  |
| 개요  | IO 사용량이 많은 작업을 실행하거나 중요 업무용 프로덕션 환경을 호스팅하는 VM을 위해 SSD 기반의 고성능, 낮은 대기 시간 디스크 지원 | 개발/테스트 VM 시나리오를 위한 HDD 기반의 경제적인 디스크 지원 |
| 시나리오  | 프로덕션 및 성능이 중요한 워크로드 | 개발/테스트, 중요하지 않음, <br>액세스를 자주 하지 않음 |
| 디스크 크기 | P4: 32GB(Managed Disks에만 해당)<br>P6: 64GB(Managed Disks에만 해당)<br>P10: 128GB<br>P20: 512GB<br>P30: 1024GB<br>P40: 2048GB<br>P50: 4095GB | 관리되지 않는 디스크: 1GB-4TB(4095GB) <br><br>관리 디스크:<br> S4: 32GB <br>S6: 64GB <br>S10: 128GB <br>S20: 512GB <br>S30: 1024GB <br>S40: 2048GB<br>S50: 4095GB| 
| 디스크당 최대 처리량 | 250MB/초 | 60MB/s | 
| 디스크당 최대 IOPS | 7500IOPS | 500IOPS | 

