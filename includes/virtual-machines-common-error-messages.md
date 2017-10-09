>[!NOTE]
> 이 페이지에 의견을 남기거나 #azerrormessage 태그를 사용하여 [Azure 피드백](https://feedback.azure.com/forums/216843-virtual-machines)을 통해 의견을 남겨주세요.

## <a name="error-response-format"></a>오류 응답 형식 
Azure Vm 오류 응답에 대 한 JSON 형식에 따라 hello를 사용 합니다.

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

오류 응답에는 상태 코드와 오류 개체가 항상 포함됩니다. 각 오류 개체에는 오류 코와 메시지가 항상 포함됩니다. Hello VM이 만들어지면 템플릿을 사용 하 여 면 hello error 개체는 내부 수준의 오류 코드 및 메시지를 포함 하는 세부 정보 섹션에 포함 합니다. 일반적으로 hello 대부분 내부 오류 메시지 수준은 hello 루트 실패 합니다.


## <a name="common-virtual-machine-management-errors"></a>일반적인 가상 컴퓨터 관리 오류

이 섹션에서는 hello 일반적인 오류 메시지가 Vm을 관리할 때 발생할 수 있습니다.

|  오류 코드  |  오류 메시지  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  ' {'이 (0) blob URI {1 \}를 사용 하 여 디스크를 만드는 동안 tooacquire 임대를 실패 했습니다. Blob이 이미 사용 중입니다.  |  
|  AllocationFailed  |  할당하지 못했습니다. Hello VM 크기 또는 Vm의 수를 줄여 보십시오, 나중에 다시 시도 하거나 tooa 배포 해 보세요 다른 가용성 집합 또는 Azure 위치입니다.  |  
|  AllocationFailed  |  tooan 내부 오류로 인해 hello VM 할당에 실패 했습니다. 나중에 다시 시도 하거나 tooa 다른 위치를 배포 해 보십시오.  |
|  ArtifactNotFound  |  위치 '{2 \}'에 hello 게시자 ' {'이 (0) 및 유형 '{1 \}' 인 VM 확장을 찾을 수 없습니다.  |
|  ArtifactNotFound  |  게시자 ' {'이 (0) '{1 \}'를 입력 하 고 형식 처리기 버전 '{2 \}' hello 확장 리포지토리에서 찾을 수 없습니다.  |
|  ArtifactVersionNotFound  |  버전 ' {'이 (가) 요청 하는 버전이 hello를 충족 하는 hello 아티팩트 리포지토리에서 찾을 수 없습니다.  |
|  ArtifactVersionNotFound  |  버전 ' {'이 (가) VM 확장에 대 한 게시자 '{1 \}' 및 '{2 \}' 형식으로 요청 하는 버전이 hello를 충족 하는 hello 아티팩트 리포지토리에서 찾을 수 없습니다.  |
|  AttachDiskWhileBeingDetached  |  데이터 디스크 ' {'이 (0) tooVM '{1 \}' hello 디스크 현재 분리 되어 있으므로 연결할 수 없습니다. Hello 디스크가 완전히 분리 될 때까지 기다렸다가 다시 시도 하십시오.  |
|  BadRequest  |  정렬된 가용성 집합은 이 지역에서 아직 지원되지 않습니다.  |
|  BadRequest  |  Toonon 관리 되는 가용성 집합 또는 blob 기반 디스크 toomanaged 가용성 집합을 사용 하 여 VM의 추가 지원 되지 않습니다는 관리 되는 디스크를 사용 하 여 VM 추가 합니다. 가용성 집합으로 만드십시오 '관리' 속성 집합 순서 tooadd에서 관리 하는 디스크 tooit 사용 하 여 VM.  |
|  BadRequest  |  Managed Disks는 이 지역에서 지원되지 않습니다.  |
|  BadRequest  |  처리기당 여러 VMExtensions이 OS 유형 '{0}'에 지원되지 않습니다. 처리기 '{2}'를 사용하는 VMExtension '{1}'을 이미 추가했거나 입력에서 지정했습니다.  |
|  BadRequest  |  Managed Disks를 사용하여 리소스 '{1}'에서 작업 '{0}'이 지원되지 않습니다.  |
|  CertificateImproperlyFormatted  |  hello {0}에서 검색할 암호의 JSON 표현에 데이터 필드가 올바른 형식의 PFX 파일 되지 않는 또는 제공 된 hello 암호 hello PFX 파일을 올바로 디코드 하지 않습니다.  |
|  CertificateImproperlyFormatted  |  {0}에서 검색 하는 hello 데이터를 JSON으로 역직렬화 할 수 없습니다.  |
|  충돌  |  디스크 크기 조정은 VM을 만들 때에 또는 hello VM 할당 취소 된 경우 허용 됩니다.  |
|  ConflictingUserInput  |  Hello 디스크 이미 소유 하 고 VM '{1 \}'에서 디스크 ' {'이 (0)을 연결할 수 없습니다.  |
|  ConflictingUserInput  |  원본 및 대상 리소스 그룹은 동일한 hello 됩니다.  |
|  ConflictingUserInput  |  디스크 {0}에 대한 원본 저장소 계정과 대상 저장소 계정이 서로 다릅니다.  |
|  ContainerAlreadyOnLease  |  {0} URI 사용 하 여 hello blob를 보유 하는 hello 저장소 컨테이너에 임대가 이미입니다.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  hello 리소스 이동 요청에는 하나 이상의 {0} s hello 요청에 의해 참조 되는 KeyVault 리소스가 포함 되어 있습니다. 현재 이 기능은 구독 간 이동에서 지원되지 않습니다. Hello KeyVault 리소스 Id에 대 한 hello 오류 세부 정보를 확인 하십시오.  |
|  DiagnosticsOperationInternalError  |  VM {0}의 진단 프로필을 처리하는 동안 내부 오류가 발생했습니다.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  Blob {0} 이미 tooVM '{1 \}'에 속한 다른 디스크가 사용 중입니다. Hello 디스크 참조 정보에 대 한 hello blob 메타 데이터를 검사할 수 있습니다.  |
|  DiskBlobNotFound  |  디스크 '{1 \}'에 대 한 URI {0} 수 없습니다 toofind VHD blob 수입니다.  |
|  DiskBlobNotFound  |  없습니다 toofind VHD blob URI {0}를 포함 하는 것입니다.  |
|  DiskEncryptionKeySecretMissingTags  |  {0} 비밀 hello {1 \} 태그를 갖고 있지 않습니다. Hello 암호 버전을 업데이트, hello 필요한 태그를 추가 하 고 다시 시도 하십시오.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  {1} 키를 사용하여 암호 {0} 값의 래핑을 해제하지 못했습니다.  |
|  DiskImageNotReady  |  디스크 이미지 {0}은 {1} 상태입니다. 이미지가 준비되면 다시 시도하세요.  |
|  DiskPreparationError  |  VM 디스크를 준비하는 동안 하나 이상의 오류가 발생했습니다. 자세한 내용은 디스크 인스턴스 보기를 참조하세요.  |
|  DiskProcessingError  |  Hello VM 실패 한 디스크의 다른 디스크에 따라 디스크 처리를 중지 합니다.  |
|  ImageBlobNotFound  |  디스크 '{1 \}'에 대 한 URI {0} 수 없습니다 toofind VHD blob 수입니다.  |
|  ImageBlobNotFound  |  없습니다 toofind VHD blob URI {0}를 포함 하는 것입니다.  |
|  IncorrectDiskBlobType  |  디스크 Blob은 유형 페이지 Blob일 수 있습니다. 디스크 '{1}'에 대한 Blob {0}은 유형 블록 Blob입니다.  |
|  IncorrectDiskBlobType  |  디스크 Blob은 유형 페이지 Blob일 수 있습니다. Blob {0}은 '{1}' 유형입니다.  |
|  IncorrectImageBlobType  |  디스크 Blob은 유형 페이지 Blob일 수 있습니다. 디스크 '{1}'에 대한 Blob {0}은 유형 블록 Blob입니다.  |
|  IncorrectImageBlobType  |  디스크 Blob은 유형 페이지 Blob일 수 있습니다. Blob {0}은 '{1}' 유형입니다.  |
|  InternalOperationError  |  저장소 계정 '{0}'을 확인할 수 없습니다. 만든 hello 저장소 리소스 공급자를 통해 hello 동일를 확인 하십시오 hello와 위치는 리소스를 계산 합니다.  |
|  InternalOperationError  |  {0} 목표 검색 태스크에 실패했습니다.  |
|  InternalOperationError  |  VM ' {'이 (0)의 네트워크 프로필 hello 유효성 검사에 오류가 발생 했습니다.  |
|  InvalidAccountType  |  hello AccountType 잘못 되었습니다.  |
|  InvalidParameter  |  hello {0} 매개 변수 수가 잘못 되었습니다.  |
|  InvalidParameter  |  지정 된 hello 관리자 암호가 허용 되지 않습니다.  |
|  InvalidParameter  |  "hello 제공 된 암호는 {0} 사이 여야 합니다-\ {1 \\} 자 이상 만족 해야 및 {2 \}는 hello 다음에서 암호 복잡성 요구 사항: <ol><li> 대문자를 포함합니다.</li><li>소문자를 포함합니다.</li><li>숫자를 포함합니다.</li><li>특수 문자를 포함합니다.</li></ol>  |
|  InvalidParameter  |  hello 지정 된 관리자 사용자 이름은 허용 되지 않습니다.  |
|  InvalidParameter  |  Hello VM이 생성 된 사용자 또는 플랫폼 이미지에서 기존 운영 체제 디스크를 연결할 수 없습니다.  |
|  InvalidParameter  |  컨테이너 이름 {0}이 올바르지 않습니다. 컨테이너 이름의 길이는 3-63자여야 하며 소문자 영숫자 및 하이픈만 포함할 수 있습니다. 하이픈은 다음에 영숫자가 와야 합니다.  |
|  InvalidParameter  |  URL {1}의 컨테이너 이름 {0}이 올바르지 않습니다. 컨테이너 이름의 길이는 3-63자여야 하며 소문자 영숫자 및 하이픈만 포함할 수 있습니다. 하이픈은 다음에 영숫자가 와야 합니다.  |
|  InvalidParameter  |  {0} URL의에서 hello blob 이름은 슬래시를 포함 합니다. 이 항목은 현재 디스크에 지원되지 않습니다.  |
|  InvalidParameter  |  hello URI {0} toobe 올바른 blob URI를 검사 하지 않습니다.  |
|  InvalidParameter  |  디스크 ' {(이) 라는 ' 이미 사용 하 여 동일한 LUN hello: {1 \}입니다.  |
|  InvalidParameter  |  '{0}'이라는 디스크는 이미 존재합니다.  |
|  InvalidParameter  |  지정 된 hello에 이미 정의 되어 디스크에 대 한 사용자 이미지 재정의 지정할 수 없습니다 참조 이미지입니다.  |
|  InvalidParameter  |  디스크 ' {(이) 라는 ' 이미 사용 하 여 hello 동일한 VHD URL {1 \}입니다.  |
|  InvalidParameter  |  hello 지정 된 오류 도메인 수 {0} 범위 있어야 hello 범위 {1} too\ {2 \}에서 합니다.  |
|  InvalidParameter  |  hello 라이선스 형식 {0} 올바르지 않습니다. 올바른 라이선스 유형: Windows_Client 또는 Windows_Server(대/소문자 구분)  |
|  InvalidParameter  |  Linux 호스트 이름이 {0} 자를 초과할 수 없습니다 또는 hello 문자 포함: {1 \}입니다.  |
|  InvalidParameter  |  Ssh 공개 키에 대 한 대상 경로가 현재 제한 tooits 기본 값 {0} due tooa 알려진 Linux 프로비저닝 에이전트에 문제가 있습니다.  |
|  InvalidParameter  |  LUN {0}에 디스크가 이미 있습니다.  |
|  InvalidParameter  |  Hello 요청 구독 0} hello 구독 {1 \} hello 관리 되는 디스크 id에 포함 된 일치 해야 합니다.  |
|  InvalidParameter  |  OSProfile의 사용자 지정 데이터는 Base64 인코딩이어야 하고 최대 길이가 {0}자여야 합니다.  |
|  InvalidParameter  |  URL {0}의 Blob 이름은 '{1}' 확장명으로 끝나야 합니다.  |
|  InvalidParameter  |  {0}'은 캡처된 유효한 VHD Blob 이름 접두사가 아닙니다. 유효한 접두사는 regex '{1}'과 일치합니다.  |
|  InvalidParameter  |  Hello VM 에이전트가 프로 비전 되지 않은 경우 인증서 tooyour VM을 추가할 수 없습니다.  |
|  InvalidParameter  |  LUN {0}에 디스크가 이미 있습니다.  |
|  InvalidParameter  |  VM 수 없습니다 toocreate hello hello 요청 크기 {0} 때문에 사용할 수 없는 경우 hello 가용성 집합은 현재 할당 된 hello 클러스터의 hello 사용 가능한 크기는: {1 \}입니다. https://aka.ms/azure-resizevm에서 전략의 크기를 조정하는 VM을 참고합니다.  |
|  InvalidParameter  |  hello VM 크기 {0} hello 현재 지역에서 사용할 수 없는 요청 했습니다. hello 현재 지역에서 사용할 수 있는 hello 크기는: {1 \}입니다. Hello 사용 가능한 VM 크기에 대 한 자세한 https://aka.ms/azure-regions에서 각 지역에 확인 합니다.  |
|  InvalidParameter  |  hello VM 크기 {0} hello 현재 지역에서 사용할 수 없는 요청 했습니다. Hello 사용 가능한 VM 크기에 대 한 자세한 https://aka.ms/azure-regions에서 각 지역에 확인 합니다.  |
|  InvalidParameter  |  Windows 관리자 사용자 이름 두 개 이상의 {0} 자를 long, 마침표 (.)는, 끝나야 또는 hello 문자를 포함할 수 없습니다: {1 \}입니다.  |
|  InvalidParameter  |  Windows 컴퓨터 이름 두 개 이상의 {0} 자를 long, 모두 숫자 또는 hello 문자를 포함할 수 없습니다: {1 \}입니다.  |
|  MissingMoveDependentResources  |  hello 리소스 이동 요청에 hello 종속 된 모든 리소스 누락된 리소스 ID에 대한 오류 세부 정보를 확인하세요.  |
|  MoveResourcesHaveInvalidState  |  hello 리소스 이동 요청에 잘못 된 저장소 계정에 연관 된 Vm 포함 되어 있습니다. 이러한 리소스 ID 및 참조된 저장소 계정 이름에 대한 세부 정보를 확인하세요.  |
|  MoveResourcesHavePendingOperations  |  hello 리소스 이동 요청에 작업이 보류 중인 리소스를 포함 합니다. 이러한 리소스 ID에 대한 세부 정보를 확인하세요. Hello 보류 중인 작업이 완료 되 면 작업을 다시 시도 합니다.  |
|  MoveResourcesNotFound  |  hello를 찾을 수 없는 리소스를 포함 하는 요청 하는 리소스를 이동 합니다. 이러한 리소스 ID에 대한 세부 정보를 확인하세요.  |
|  NetworkingInternalOperationError  |  알 수 없는 네트워크 할당 오류입니다.  |
|  NetworkingInternalOperationError  |  알 수 없는 네트워크 할당 오류입니다.  |
|  NetworkingInternalOperationError  |  Hello VM의 네트워크 프로필을 처리에서 내부 오류가 발생 했습니다.  |
|  NotFound  |  hello 가용성 집합 {0}를 찾을 수 없습니다.  |
|  NotFound  |  원본 가상 컴퓨터 ' {'이 (가) hello 요청에 지정 합니다.이 Azure 위치에 존재 하지 않습니다.  |
|  NotFound  |  ID {0}을(를) 갖는 테넌트를 찾을 수 없습니다.  |
|  NotFound  |  hello 이미지 {0}를 찾을 수 없습니다.  |
|  NotSupported  |  hello 라이선스 유형을 않으며 {0} hello 이미지 blob {1 \}가 온-프레미스에서입니다.  |
|  OperationNotAllowed  |  가용성 집합 {0}을 삭제할 수 없습니다. 가용성 집합을 삭제하려면 먼저 가용성 집합이 VM을 포함하지 않도록 하세요.  |
|  OperationNotAllowed  |  설정 변경 'Aligned' too'Classic에서 집합 SKU' 허용 되지 않습니다.  |
|  OperationNotAllowed  |  Hello VM 실행 중이지 않을 때 hello VM에서에서 확장을 수정할 수 없습니다.  |
|  OperationNotAllowed  |  hello 캡처 작업은 blob 기반 디스크와 가상 컴퓨터 에서만 지원 됩니다. Hello '이미지' 리소스 Api toocreate 관리 되는 가상 컴퓨터에서 이미지를 사용 하십시오.  |
|  OperationNotAllowed  |  hello 리소스 {0} 이미지 성공적으로 만들었습니다. 될 때까지 이미지 {1 \}에서 만들 수 없습니다.  |
|  OperationNotAllowed  |  VM의 할당이 취소 한 후 다시 시도 하세요 VM 할당 업데이트 tooencryptionSettings 허용 되지 않습니다.  |
|  OperationNotAllowed  |  Blob 기반 디스크와 관리 되는 디스크 tooa VM의 추가 지원 되지 않습니다.  |
|  OperationNotAllowed  |  연결 된 toobe tooa이이 크기의 VM은 {0} 허용 하는 hello 최대 데이터 디스크 수 있습니다.  |
|  OperationNotAllowed  |  관리 되는 디스크와 blob 기반 디스크 tooVM의 추가 지원 되지 않습니다.  |
|  OperationNotAllowed  |  작업 ' {'이 (가) 이미지 삭제 되도록 표시 되어 hello 이후 이미지 '{1 \}'에 허용 되지 않습니다. 수만 hello 삭제 작업을 다시 시도 하세요 (또는 진행 중인 한 toocomplete 대기).  |
|  OperationNotAllowed  |  작업 ' {'이 (가) VM을 일반화 hello 이후 VM '{1 \}'에서 허용 되지 않습니다.  |
|  OperationNotAllowed  |  복원 지점 컬렉션 '{1}'을 삭제하도록 표시하는 경우 작업 '{0}'이 허용되지 않습니다.  |
|  OperationNotAllowed  |  VM 확장 '{1}'이 삭제 예정으로 표시되었으므로 이 VM 확장에서는 작업 '{0}'이(가) 허용되지 않습니다. 수만 hello 삭제 작업을 다시 시도 하세요 (또는 진행 중인 한 toocomplete 대기).  |
|  OperationNotAllowed  |  Hello 이미지 '{2 '을 \를}를 사용 하 여 hello 가상 컴퓨터 '{1 '을 \를}를 프로 비전 되는 작업 ' {'이 (가) 허용 되지 않습니다.  |
|  OperationNotAllowed  |  Hello ScaleSet 가상 컴퓨터 '{1 \}'에서 현재 hello '{2 \}' 이미지를 사용 중 이므로 작업 ' {'이 (가) 허용 되지 않습니다.  |
|  OperationNotAllowed  |  VM 삭제 되도록 표시 되어 hello 이후 VM '{1 \}'에서 작업 ' {'이 (가) 허용 되지 않습니다. 수만 hello 삭제 작업을 다시 시도 하세요 (또는 진행 중인 한 toocomplete 대기).  |
|  OperationNotAllowed  |  Hello VM 할당이 취소 되는 할당이 해제 또는 표시 된 toobe 이므로 작업 ' {'이 (가) VM '{1 \}'에 허용 되지 않습니다.  |
|  OperationNotAllowed  |  Hello VM 실행 되 고 이후 VM '{1 \}'에서 작업 ' {'이 (가) 허용 되지 않습니다. 하십시오 전원 끄기 명시적으로 종료할 경우 hello VM에서 게스트 운영 체제에서 hello 합니다.  |
|  OperationNotAllowed  |  작업 ' {'이 (가) VM 할당이 해제 되지 않습니다 hello 이후 VM '{1 \}'에서 허용 되지 않습니다.  |
|  OperationNotAllowed  |  VM에 오류 상태인 '{2}' 확장이 있으므로 VM '{1}'에서는 작업 '{0}'이(가) 허용되지 않습니다.  |
|  OperationNotAllowed  |  다른 작업이 진행 중이므로 작업 '{0}'은(는) VM '{1}'에서 허용되지 않습니다.  |
|  OperationNotAllowed  |  hello 작업 ' {'이 (가) 가상 컴퓨터 '{1 \}' toobe hello 일반화 됨으로 필요합니다.  |
|  OperationNotAllowed  |  hello 작업을 실행 하는 hello VM toobe 필요 하거나 toorun 설정.  |
|  OperationNotAllowed  |  디스크 크기 {0} GB는 hello 보다 작은 {1}GB 이미지에 해당 디스크의 크기 조정, 허용 되지 않습니다.  |
|  OperationNotAllowed  |  VM 크기 집합 확장 처리기 ' {'이 (0)의 VM 크기 집합 만들기의 hello 타임에만 추가할 수 있습니다.  |
|  OperationNotAllowed  |  VM 크기 집합 확장 처리기 ' {'이 (0)의 VM 크기 집합 삭제의 hello 타임에만 삭제할 수 있습니다.  |
|  OperationNotAllowed  |  '{0}' VM이 이미 Managed Disks를 사용하고 있습니다.  |
|  OperationNotAllowed  |  VM ' {'이 (0) 속한 too'Classic' 가용성 집합 '{1 \}'. 업데이트 hello 가용성 toouse 'Aligned' SKU 설정 하 고 hello 변환을 다시 시도 하십시오.  |
|  OperationNotAllowed  |  이미지에서 만든 VM은 Blob 기반 디스크를 사용할 수 없습니다. 모든 디스크는 디스크 관리 toobe 있습니다.  |
|  OperationNotAllowed  |  캡처 hello VM 일반화 되지 않으면 때문에 작업을 완료할 수 없습니다.  |
|  OperationNotAllowed  |  VM ' {'이 (0)의 관리 작업에는 VM 디스크를 변환 된 toomanaged 디스크 때문에 허용 되지 않습니다.  |
|  OperationNotAllowed  |  진행 중인 작업에는 가상 컴퓨터 {0} too\ {1 \\}의 전원 상태를 변경입니다. 일정 시간이 지난 후 {2} 작업을 수행하세요.  |
|  OperationNotAllowed  |  없습니다 tooadd 또는 업데이트 hello VM입니다. hello 요청한 VM 크기 {0}를 hello 기존 할당 단위에서 확인할 수 있습니다. https://aka.ms/azure-resizevm에서 전략의 크기를 조정하는 VM을 참고합니다.  |
|  OperationNotAllowed  |  VM 수 없습니다 tooresize hello hello 요청 크기 {0} 때문에 사용할 수 없는 경우 hello 가용성 집합은 현재 할당 된 hello 클러스터의 hello 사용 가능한 크기는: {1 \}입니다. https://aka.ms/azure-resizevm에서 전략의 크기를 조정하는 VM을 참고합니다.  |
|  OperationNotAllowed  |  VM 수 없습니다 tooresize hello hello 요청 크기 {0} 때문에 사용할 수 없는 경우 여기서 hello VM는 현재 할당 된 hello 클러스터의 tooresize 프로그램 VM too\ {1 \\}를 할당 취소 하십시오 (hello Azure 포털에서에서 중지 작업은) hello 크기 조정 작업을 다시 시도 하십시오. https://aka.ms/azure-resizevm에서 전략의 크기를 조정하는 VM을 참고합니다.  |
|  OSProvisioningClientError  |  OS 프로비저닝이 없으므로 VM ' {'이 (0)에 대 한 hello 게스트 OS가 현재 프로비저닝되 고입니다.  |
|  OSProvisioningClientError  |  VM '{0}'에 대한 OS를 프로비전하지 못했습니다. 오류 세부 정보: {1 \} 확인 되었는지 hello 이미지가 제대로 준비 (범용 화) 합니다. <ul><li>Windows에 대한 지침: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  SSH 호스트 키를 생성하지 못했습니다. 오류 세부 정보: {0} tooresolve Linux 에이전트가 제대로 설정 되어 있으면이 문제 확인 합니다. <ul><li>Hello 지침을 확인할 수 있습니다: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  VM이 Linux 배포에 적합 하지 않습니다. hello에 대 한 사용자 이름을 지정 합니다. 오류 세부 정보: {0}  |
|  OSProvisioningInternalError  |  OS 프로비저닝이 실패 했습니다 VM ' {'이 (0)에 대 한 tooan 내부 오류입니다.  |
|  OSProvisioningTimedOut  |  VM ' {'이 (0)에 대 한 OS 프로비저닝이 hello 할당 시간에에서 완료 되지 않았습니다. hello VM 프로비저닝이 성공적으로 완료 계속 될 수 있습니다. 나중에 프로비전 상태를 확인합니다.  |
|  OSProvisioningTimedOut  |  VM ' {'이 (0)에 대 한 OS 프로비저닝이 hello 할당 시간에에서 완료 되지 않았습니다. hello VM 프로비저닝이 성공적으로 완료 계속 될 수 있습니다. 나중에 프로비전 상태를 확인합니다. 또한 hello 이미지가 제대로 준비 되었는지 확인 하십시오 (범용 화) 합니다.   <ul><li>Windows에 대한 지침: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Linux에 대한 지침: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  VM ' {'이 (0)에 대 한 OS 프로비저닝이 hello 할당 시간에에서 완료 되지 않았습니다. 그러나 hello VM 게스트 에이전트 실행 검색 되었습니다. Hello 게스트 운영 체제를 제대로 되지 않은 준비 toobe VM 이미지로 사용 되는 원인 중 하나 (CreateOption FromImage =) 합니다. tooresolve이 문제를 사용 하 여 hello VHD CreateOption 있는 그대로 두 연결 = 또는 이미지 형식으로 사용 하기 위해 적절히 준비:   <ul><li>Windows에 대한 지침: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Linux에 대한 지침: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  hello는 hello 선택한 위치에서 v M 크기를 현재 사용할 수 없는 필요 합니다.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  이 이번 tooongoing 플랫폼 업데이트 때문에 리소스를 업데이트할 수 없습니다. 나중에 다시 시도하세요.  |
|  StorageAccountLimitation  |  저장소 계정 ' {'이 (가) 필요한 toocreate 디스크는 페이지 blob을 지원 하지 않습니다.  |
|  StorageAccountLimitation  |  저장소 계정 '{0}'이(가) 할당량을 초과했습니다.  |
|  StorageAccountLocationMismatch  |  저장소 계정 '{0}'을 확인할 수 없습니다. 만든 hello 저장소 리소스 공급자를 통해 hello 동일를 확인 하십시오 hello와 위치는 리소스를 계산 합니다.  |
|  StorageAccountNotFound  |  저장소 계정 {0}을 찾을 수 없습니다. 저장소 계정 삭제 되지 않습니다 및 toohello 속한 확인 hello VM과 동일한 Azure 위치입니다.  |
|  StorageAccountNotRecognized  |  저장소 리소스 공급자가 관리하는 저장소 계정을 사용하세요. {0}은 지원되지 않습니다.  |
|  StorageAccountOperationInternalError  |  저장소 계정 {0}에 액세스하는 동안 내부 오류가 발생했습니다.  |
|  StorageAccountSubscriptionMismatch  |  저장소 계정 {0} toosubscription {1 \}에 속하지 않습니다.  |
|  StorageAccountTooBusy  |  저장소 계정 '{0}'은 현재 사용량이 너무 많습니다. 다른 계정을 사용하는 것이 좋습니다.  |
|  StorageAccountTypeNotSupported  |  {0} 디스크는 Blob Storage 계정인 {1}을 사용합니다. 범용 저장소 계정을 사용하여 다시 시도하세요.  |
|  StorageAccountTypeNotSupported  |  저장소 계정 {0}은 {1} 유형입니다. 부팅 진단은 저장소 계정 유형 {2}를 지원합니다.  |
|  SubscriptionNotAuthorizedForImage  |  hello 구독은 권한이 없습니다.  |
|  TargetDiskBlobAlreadyExists  |  Blob {0}은 이미 있습니다. 제공 하십시오 다른 blob URI toocreate는 새로운 빈 데이터 디스크 '{1 \}'.  |
|  TargetDiskBlobAlreadyExists  |  캡처 대상 이미지 blob {0} 이미 있으며 hello 플래그 toooverwrite VHD blob 설정 되어 있지 않으므로 작업을 계속할 수 없습니다. Hello blob 삭제 toooverwrite VHD blob hello 플래그를 설정 및 다시 시도 하십시오.  |
|  TargetDiskBlobAlreadyExists  |  대상 이미지 Blob {0}에 활성 임대가 있어서 캡처 작업을 계속할 수 없습니다.   |
|  TargetDiskBlobAlreadyExists  |  Blob {0}은 이미 있습니다. 다른 Blob URI를 디스크 '{1}'에 대한 대상으로 제공하세요.  |
|  TooManyVMRedeploymentRequests  |  VM ' {'이 (0)에 대 한 재배포 요청을 너무 많이 받았습니다 또는의 hello Vm이이 VM과 동일한 availabilityset hello 합니다. 나중에 다시 시도하십시오.  |
|  VHDSizeInvalid  |  hello 지정 디스크 '{1 '을 \를} blob {2 \}와 {0}의 디스크 크기 값이 올바르지 않습니다. 디스크 크기는 {3}에서 {4} 사이여야 합니다.  |
|  VMAgentStatusCommunicationError  |  VM '{0}'이 VM 에이전트 또는 확장의 상태를 보고하지 않았습니다. 아웃 바운드 연결 tooAzure 저장소를 설정할 수을 hello VM에는 실행 중인 VM 에이전트를 확인 하십시오.  |
|  VMArtifactRepositoryInternalError  |  Hello 아티팩트 저장소 tooretrieve VM 아티팩트 세부 정보와 함께 통신 하는 동안 오류가 발생 했습니다.  |
|  VMArtifactRepositoryInternalError  |  Hello 아티팩트 리포지토리에서 hello VM 아티팩트 데이터를 검색 하는 동안 내부 오류가 발생 했습니다.  |
|  VMExtensionHandlerNonTransientError  |  처리기 '{0}'에서 VM 확장 '{1}'에 대한 오류를 보고했습니다. 터미널 오류 코드는 '{2}'이고 오류 메시지는 다음과 같습니다. '{3}'  |
|  VMExtensionManagementInternalError  |  VM 확장 '{0}'을 처리하는 동안 내부 오류가 발생했습니다.  |
|  VMExtensionManagementInternalError  |  Hello VM 확장을 준비 하는 동안 여러 오류가 발생 했습니다. 자세한 내용은 VM 확장 인스턴스 보기를 참조하세요.  |
|  VMExtensionProvisioningError  |  확장 '{0}'을(를) 처리하는 동안 VM이 오류를 보고했습니다. 오류 메시지 "{1}"  |
|  VMExtensionProvisioningError  |  여러 개의 VM 확장 toobe hello VM에서 프로 비전 하지 못했습니다. 자세한 내용은 VM 확장 인스턴스 보기 hello를 참조 하십시오.  |
|  VMExtensionProvisioningTimeout  |  VM 확장 '{0}'의 프로비전이 시간을 초과했습니다. 확장 설치에 시간이 오래 걸릴 수 있습니다. 또는 확장 상태를 가져오지 못할 수 있습니다.  |
|  VMMarketplaceInvalidInput  |  비 마켓플레이스 이미지 로부터 가상 컴퓨터 만들기는 하지 필요 정보, 계획 hello 요청에 hello 계획 정보를 제거 하십시오. OS 디스크 이름은 {0}입니다.  |
|  VMMarketplaceInvalidInput  |  hello 구매 정보가 일치 하지 않습니다. Hello 마켓플레이스 이미지 로부터 toodeploy 수 없습니다. OS 디스크 이름은 {0}입니다.  |
|  VMMarketplaceInvalidInput  |  마켓플레이스 이미지 로부터 가상 컴퓨터를 만드는 hello 요청에 계획 정보가 필요 합니다. OS 디스크 이름은 {0}입니다.  |
|  VMNotFound  |  hello VM ' {'이 (0) 찾을 수 없습니다.  |
|  VMRedeploymentFailed  |  VM ' {'이 (0) 재배포 tooan 내부 오류로 인해 실패 했습니다. 나중에 다시 시도하십시오.  |
|  VMRedeploymentTimedOut  |  VM ' {'이 (0)를 재배포 하면 hello 할당 시간에에서 완료 되지 않았습니다. 얼마 뒤면 성공적으로 완료될 수 있습니다. 다른 hello 요청을 다시 시도할 수 있습니다.  |
|  VMStartTimedOut  |  VM ' {'이 (0) hello 할당 시간에에서 시작 되지 않았습니다. hello VM을 시작할 수 있습니다. 나중에 hello 전원 상태를 확인 하십시오.  |


## <a name="next-steps"></a>다음 단계
도움이 필요한 경우 문의할 수 있습니다에 Azure 전문가 hello [MSDN Azure 및 스택 오버플로 포럼 hello](https://azure.microsoft.com/support/forums/)합니다. 또는 Azure 기술 지원 인시던트를 제출할 수 있습니다. Toohello 이동 [Azure 지원 사이트](https://azure.microsoft.com/support/options/) 선택 **Get Support**합니다.
