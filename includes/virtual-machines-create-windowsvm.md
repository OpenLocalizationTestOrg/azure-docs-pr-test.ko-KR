1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.

2. 왼쪽 위에서 hello 년부터 클릭 **새로 만들기 > 계산 > Windows Server 2016 Datacenter**합니다.

    ![Hello 포털에서 Azure VM 이미지 toohello 이동](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. Windows Server 2016 Datacenter hello hello 클래식 배포 모델을 선택 합니다. 만들기를 클릭합니다.

    ![Hello 포털에서 사용할 수 있는 hello Azure VM 이미지를 보여 주는 스크린샷](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a>1. 기본 사항 블레이드

hello 기본 사항 블레이드에서 hello 가상 컴퓨터에 대 한 관리 정보를 요청합니다.

1. 입력 한 **이름** hello 가상 컴퓨터에 대 한 합니다. Hello 예에서 _HeroVM_ hello hello 가상 컴퓨터 이름입니다. hello 이름은 1 ~ 15 자 해야 및 특수 문자를 포함할 수 없습니다.

2. 입력 한 **사용자 이름** 강력한 및 **암호** 사용된 toocreate hello VM에서 로컬 계정이 됩니다. hello 로컬 계정을 사용 tooand에 toosign hello VM을 관리 합니다. Hello 예에서 _azureuser_ hello 사용자 이름입니다.

 hello 암호 여야 8 123 자 이상 이어야 하 고는 세 가지 hello 4 개의 다음 복잡성 요구 사항을 충족: 하나의 \t-소문자, 대문자 한 문자, 숫자, 및 특수 문자를 하나 있습니다. 자세한 내용은 [사용자 이름 및 암호 요구 사항](../articles/virtual-machines/windows/faq.md)을 참조하세요.

3. hello **구독** 선택 사항입니다. 일반적인 설정 중 하나는 "종량제"입니다.

4. 기존 선택 **리소스 그룹** 또는 새 유형 hello 이름입니다. Hello 예에서 _HeroVMRG_ hello hello 리소스 그룹 이름입니다.

5. Azure 데이터 센터 선택 **위치** hello VM toorun 원하는 합니다. Hello 예에서 **미국 동부** hello 위치입니다.

6. 완료 되 면 클릭 **다음** toocontinue toohello 다음 블레이드입니다.

    ![Azure VM을 구성 하기 위한 기본 사항 블레이드에서 hello hello 설정을 보여 주는 스크린샷](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a>2. 크기 블레이드

hello 크기 블레이드 hello VM의 hello 구성 세부 정보를 식별 하 고 운영 체제, 프로세서, 디스크 저장소 유형 및 월간 사용 비용을 예상된 수를 포함 하는 다양 한 옵션을 나열 합니다.  

VM 크기를 선택 하 고 클릭 한 다음 **선택** toocontinue 합니다. 이 예제에서는 _DS1_\__V2 표준_ hello VM 크기입니다.

  ![Hello 선택할 수 있는 Azure VM 크기를 보여 주는 hello 크기 블레이드의 스크린샷](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a>3. 설정 블레이드

hello 설정 블레이드에서 저장소 및 네트워크 옵션을 요청합니다. Hello 기본 설정을 사용할 수 있습니다. Azure는 필요에 따라 적절한 항목을 만듭니다.

지원하는 가상 컴퓨터 크기를 선택한 경우 디스크 유형에서 프리미엄(SSD)을 선택하여 Azure Premium Storage를 사용해 볼 수 있습니다.

변경 작업이 완료되면 **확인**을 클릭합니다.

## <a name="4-summary-blade"></a>4. 요약 블레이드

hello 요약 블레이드 hello 이전 블레이드에 지정 된 hello 설정을 나열 합니다. 클릭 **확인** 준비 toomake hello 이미지 라인인 경우입니다.

 ![Hello 가상 컴퓨터의 지정 된 설정을 제공 하는 요약 블레이드 보고서](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

Hello 포털 hello 새 가상 컴퓨터에 표시 되는 hello 가상 컴퓨터를 만든 후 **모든 리소스**, hello 대시보드에서 hello 가상 컴퓨터의 타일을 표시 합니다. 해당 클라우드 서비스와 저장소 계정은 hello도 생성 되어 나열 합니다. Hello 가상 컴퓨터 및 클라우드 서비스를 모두 자동으로 시작 하 고 해당 상태로 나열 되어 **실행**합니다.

 ![Hello 가상 컴퓨터의 VM 에이전트 및 hello 끝점 구성](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
