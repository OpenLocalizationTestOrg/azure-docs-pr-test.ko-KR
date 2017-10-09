Azure 저장소의 모든 Blob은 컨테이너에 있어야 합니다. hello 컨테이너의 일부를 구성 hello blob 이름입니다. 예를 들어 `mycontainer` hello 이러한 샘플 blob Uri에에서 hello 컨테이너 이름입니다.

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

컨테이너 이름은 표준에 맞는 toohello 명명 규칙에 따라 유효한 DNS 이름 이어야 합니다.

1. 컨테이너 이름은 문자 또는 숫자로 시작 해야 하며 문자, 숫자 및 hello 대시 (-) 문자만 포함할 수 있습니다.
2. 컨테이너 이름에서 모든 대시(-) 문자는 문자 또는 숫자 바로 앞뒤에 와야 하며 연속 대시를 사용할 수 없습니다.
3. 컨테이너 이름의 모든 문자는 소문자여야 합니다.
4. 컨테이너 이름의 길이는 3자 이상, 63자 이하여야 합니다.

> [!IMPORTANT]
> 해당 hello 확인 된 컨테이너의 이름을 항상 소문자 여야 합니다. 컨테이너 이름에는 대문자를 포함 하거나 hello 컨테이너 명명 규칙을 위반 하는 그렇지 않은 경우 400 오류 (잘못 된 요청)를 나타날 수 있습니다. 
> 
> 

