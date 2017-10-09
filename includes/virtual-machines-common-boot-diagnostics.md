이제 Azure에서 두 가지 디버깅 기능에 대한 지원이 제공됩니다. Azure Virtual Machines Resource Manager 배포 모델에 대한 콘솔 출력 및 스크린샷 지원. 

설정할 때 사용자 고유의 이미지 tooAzure 이거나도 부팅 중 hello 플랫폼 이미지, 가상 컴퓨터를 부팅할 수 없는 상태로 가져옵니다 하는 이유는 여러 가지 이유가 있을 수 있습니다. Tooeasily 있습니다를 진단 하 고 가상 컴퓨터 부팅 실패에서 복구 이러한 기능 사용 합니다.

Linux 가상 컴퓨터에 대 한 hello 출력 hello 포털에서에서 콘솔 로그를 쉽게 볼 수 있습니다.

![Azure portal](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
그러나 Windows와 Linux 가상 컴퓨터에 대 한 Azure가 해줍니다 toosee를 hello 하이퍼바이저에서 hello VM의 스크린샷:

![오류](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

이 두 가지 기능이 모든 지역의 Azure Virtual Machines에서 지원됩니다. 참고, 스크린샷 및 출력 저장소 계정에 분 tooappear too10 차지할 수 있습니다.

## <a name="common-boot-errors"></a>일반적인 부팅 오류

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [운영 체제를 찾지 못함](https://support.microsoft.com/help/4010142)
- [부팅 오류 또는 INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>새 가상 컴퓨터에서 진단 사용
1. Hello 미리 보기 포털에서에서 새 가상 컴퓨터를 만들 때 선택 hello **Azure 리소스 관리자** hello 배포 모델 드롭다운에서:
 
    ![리소스 관리자](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. 이러한 진단 파일 hello 모니터링 옵션 tooselect hello 저장소 계정 tooplace 하려는 위치를 구성 합니다.
 
    ![VM 만들기](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Azure 리소스 관리자 템플릿을 배포 하는 경우 tooyour 가상 컴퓨터 리소스를 이동 하 고 hello 진단 프로필 섹션을 추가 하세요. Toouse hello "2015-06-15" API 버전 헤더를 기억 합니다.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. hello 진단 프로필 tooselect hello 저장소 계정을 저장할 tooput 이러한 로그 있습니다.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy 부트 진단을 사용, 체크 아웃 여기의 리포지토리에서 샘플 가상 컴퓨터.

## <a name="update-an-existing-virtual-machine"></a>기존 가상 컴퓨터 업데이트 ##

hello 포털을 통해 tooenable 부트 진단을 hello 포털을 통해 기존 가상 컴퓨터를 업데이트할 수도 있습니다. Hello 부트 진단이 저장 및 옵션을 선택 합니다. Hello VM tootake 효과 다시 시작 합니다.

![기본 VM 업데이트](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

