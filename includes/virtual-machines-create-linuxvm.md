
1. 로그인에 나열 된 hello 단계를 사용 하 여 Azure 구독을 tooyour [hello Azure CLI 1.0에서에서 tooAzure 연결](../articles/xplat-cli-connect.md)합니다.

2. 다음과 같이 hello 클래식 배포 모드에 있는 있는지 확인 합니다.

    ```azurecli
    azure config mode asm
    ```

3. 확인 hello Linux 이미지 tooload hello 제공 되는 이미지에서 다음과 같이 되도록 합니다.

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    Windows 명령 프롬프트 창에서 grep 대신 **find** 를 사용합니다.
   
4. 사용 하 여 `azure vm create` toocreate hello 이전 목록에서 hello Linux 이미지를 사용 하 여 VM입니다. 이 단계에서는 클라우드 서비스 및 저장소 계정을 만듭니다. 이 VM tooan 기존 클라우드 서비스와 연결할 수도 수는 `-c` 옵션입니다. Hello로 toohello Linux 가상 컴퓨터에서 SSH 끝점 toolog 만들기 `-e` 옵션입니다. hello 다음 예제에서는 V `myVM` hello를 사용 하 여 `Ubuntu-14_04_4-LTS` hello에 이미지 `West US` 위치, 사용자 이름을 추가 하 고 `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    hello 비슷한 toohello 다음은 예제 출력:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Linux 가상 컴퓨터에 대 한 hello 제공 해야 `-e` 옵션 `vm create`합니다. Hello 가상 컴퓨터를 만든 후 가능한 tooenable SSH 않습니다. 에 대 한 자세한 내용은 SSH, 읽을 [어떻게 tooUse와 Azure에서 Linux에 SSH](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

5. Hello를 사용 하 여 hello VM의 hello 특성을 확인할 수 있습니다 `azure vm show` 명령입니다. hello 다음 예에서는 나열 hello 라는 VM에 대 한 정보 `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Hello로 VM을 시작 `azure vm start` 명령은 다음과 같습니다.

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>다음 단계
이러한 모든 Azure CLI 1.0 가상 컴퓨터 명령에 대 한 세부 정보를 참조 하세요 hello [hello 클래식 배포 API 사용 하 여 hello Azure CLI 1.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)합니다.

