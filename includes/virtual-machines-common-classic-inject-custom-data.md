


이 항목에서는 이러한 방법에 대해 설명합니다.

* 프로비전 중에 Azure VM(가상 컴퓨터)에 데이터를 삽입합니다.
* Windows 및 Linux에 대해 데이터 검색
* 일부 시스템 toodetect에서 사용할 수 있는 특수 도구를 사용 하 고 사용자 지정 데이터를 자동으로 처리 합니다.

> [!NOTE]
> 이 문서에서는 방법을 사용자 지정 데이터 설명 hello Azure 서비스 관리 API를 사용 하 여 만든 VM을 사용 하 여 삽입 될 수 있습니다. toouse hello Azure 리소스 관리 API를 확인 하려면 어떻게 toosee [hello 예제 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata)합니다.
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Azure 가상 컴퓨터에 사용자 지정 데이터 삽입
이 기능은 현재 hello에만 지원 됩니다 [Azure 명령줄 인터페이스](https://github.com/Azure/azure-xplat-cli)합니다. 만들 여기는 `custom-data.txt` 우리의 데이터가 포함 된 파일 다음 삽입 하는 toohello VM의에서 프로 비전 중입니다. Hello에 대 한 hello 옵션 중 하나를 사용할 수 있지만 `azure vm create` 명령, hello 다음 한 가지 기본적인 방법을 보여 줍니다.

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>사용자 지정 데이터를 사용 하 여 hello 가상 컴퓨터에서
* Azure VM은 Windows 기반 VM 경우 hello 사용자 지정 데이터 파일은 너무 저장`%SYSTEMDRIVE%\AzureData\CustomData.bin`합니다. Hello 로컬 컴퓨터 toohello에서 base64 인코딩 tootransfer를 없었지만 새 VM은 자동으로 디코딩된 및 열거나 수 즉시 사용 합니다.
  
  > [!NOTE]
  > Hello 파일이 있으면 덮어씁니다. hello 디렉터리에 hello 보안 설정이 너무**시스템: 모든 권한** 및 **관리자: 모든 권한**합니다.
  > 
  > 
* Azure VM이 Linux 기반 VM hello 사용자 지정 데이터 파일에 배치 됩니다 hello 다음 중 하나에 배포판에 따라 배치 합니다. hello 데이터가 toodecode hello 데이터를 먼저 할 수 있도록 base64 인코딩된 될 수 있습니다.
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Azure에서 Cloud-Init
Ubuntu 또는 CoreOS 이미지에서 Azure VM이 있는 경우 CustomData toosend 클라우드 구성을 toocloud 초기화를 사용할 수 있습니다. 또는 사용자 지정 데이터 파일이 스크립트인 경우, cloud-init이 스크립트를 실행하기만 하면 됩니다.

### <a name="ubuntu-cloud-images"></a>Ubuntu 클라우드 이미지
대부분의 Azure Linux 이미지에서 편집 하는 "/ etc/waagent.conf" tooconfigure hello 일시적인 리소스 디스크와 스왑 파일입니다. 자세한 내용은 [Azure Linux 에이전트 사용자 가이드](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 를 참조하세요.

그러나 hello Ubuntu 클라우드 이미지를 사용 해야 클라우드 init tooconfigure hello 리소스 디스크 (즉, hello "임시" 디스크) 및 교환 파티션 합니다. 참조 페이지에 나오는 자세한 세부 정보에 대 한 hello Ubuntu wiki에 hello: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions)합니다.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>다음 단계: cloud-init 사용
자세한 내용은 참조 hello [Ubuntu 용 클라우드 init 설명서](https://help.ubuntu.com/community/CloudInit)합니다.

<!--Link references-->
[역할 서비스 관리 REST API 참조 추가](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Azure 명령줄 인터페이스](https://github.com/Azure/azure-xplat-cli)

