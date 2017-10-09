## <a name="what-is-blob-storage"></a>Blob 저장소 정의
Azure Blob 저장소는 많은 양의 텍스트 또는 이진 데이터를 액세스할 수 있는에서 아무 곳 이나 HTTP 또는 HTTPS를 통해 hello world에 같은 구조화 되지 않은 개체 데이터를 저장 하기 위한 서비스입니다. Blob 저장소 tooexpose 데이터 사용 하 여 공개적으로 toohello 권역 또는 toostore 응용 프로그램 데이터 개인적으로 합니다.

Blob 저장소의 일반적인 사용은 다음과 같습니다.

* 서비스 제공 이미지 또는 직접 tooa 브라우저에 설명
* 분산 액세스를 위해 파일 저장
* 동영상 및 오디오 스트리밍
* 백업 및 복원, 재해 복구 및 보관을 위한 데이터 저장
* 온-프레미스 또는 Azure 호스티드 서비스에서 분석하기 위해 데이터 저장

## <a name="blob-service-concepts"></a>BLOB 서비스 개념
hello를 Blob 서비스는 hello를 다음과 같은 구성 요소가 포함 되어 있습니다.

![Blob 아키텍처](./media/storage-blob-concepts-include/blob1.png)

* **저장소 계정:** 저장소 계정을 통해 모든 액세스 tooAzure 저장소 작업은 수행 됩니다. 이 저장소 계정은 **범용 저장소 계정**이거나, 개체/Blob 저장용으로 특화된 **Blob 저장소 계정**이 될 수 있습니다. 자세한 내용은 [Azure Storage 계정 정보](../articles/storage/common/storage-create-storage-account.md)를 참조하세요.
* **컨테이너:** 컨테이너는 Blob 집합 그룹화를 제공합니다. 모든 Blob은 컨테이너에 있어야 합니다. 한 계정에 포함될 수 있는 컨테이너 수에는 제한이 없습니다. 한 컨테이너에 저장될 수 있는 Blob 수에도 제한이 없습니다. Note 해당 hello 컨테이너 이름은 소문자 여야 합니다.
* **Blob:** 모든 형식과 크기의 파일입니다. Azure 저장소에는 블록 Blob, 페이지 Blob 및 추가 Blob의 세 가지 Blob 유형이 있습니다.
  
    *블록 Blob* 은 문서 및 미디어 파일과 같은 텍스트 또는 이진 파일을 저장하기에 적합합니다. *추가 blob* 는 비슷한 tooblock blob는 블록으로 구성 하지만에 맞게 최적화 된 추가 작업을 로깅 시나리오에 유용한 되기 때문입니다. 단일 블록 blob too50, 각, too100 MB의 000 블록을 포함할 수 있습니다 (100 MB X 50000) 4.75 TB 보다 조금 더 큰의 전체 크기에 대 한 합니다. 단일 blob too50, 각, too4 MB의 000 블록을 포함할 수 있습니다 (4 MB X 50000) 195 GB 보다 조금 더 큰의 전체 크기에 대 한 합니다.
  
    *페이지 blob* 크기가 too1 TB를 수 있으며 자주 읽기/쓰기 작업에 대 한 더 효율적입니다. Azure 가상 컴퓨터는 OS 및 데이터 디스크로 페이지 Blob을 사용합니다.
  
    컨테이너 및 Blob를 명명하는 세부 정보는 [컨테이너, Blob 및 메타데이터 명명 및 참조](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata)를 참조하세요.

