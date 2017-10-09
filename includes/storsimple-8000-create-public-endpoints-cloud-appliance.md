#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>hello 클라우드 어플라이언스에 toocreate 공용 끝점

1. Azure 포털 toohello에 로그인 합니다.
2. 너무 이동**가상 컴퓨터**을 다음 선택 하 고 hello 가상 컴퓨터 클라우드 어플라이언스에으로 사용 되 고를 클릭 합니다.
    
3. 가상 컴퓨터 내부 및 외부로 toocreate를 네트워크 보안 그룹 (NSG) 규칙 toocontrol hello 트래픽 흐름을 해야합니다. Hello 단계 toocreate NSG 규칙 다음을 수행 합니다.
    1. **네트워크 보안 그룹**을 선택합니다.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. 표시 되는 hello 기본 네트워크 보안 그룹을 클릭 합니다.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. **인바운드 보안 규칙**을 선택합니다.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. 클릭 **+ 추가** toocreate 인바운드 보안 규칙입니다.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        Hello 추가 인바운드 보안 규칙 블레이드에서:

        1. Hello에 대 한 **이름**, hello 끝점에 대 한 형식 hello 다음 이름을: WinRMHttps 합니다.
        
        2. Hello에 대 한 **우선 순위**선택 합니다 (즉, hello 기본 규칙에 대 한 hello 우선 순위) 숫자 1000 보다 낮습니다. Hello 값이 높을수록 더 낮은 hello 우선 합니다.

        3. 집합 hello **소스** 너무**모든**합니다.

        4. Hello에 대 한 **서비스**선택, **WinRM**합니다. hello **프로토콜** 는 자동으로 너무 설정**TCP** 및 hello **포트 범위가** 너무 설정 되어**5986**합니다.

        5. 클릭 **확인** toocreate hello 규칙입니다.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. 마지막 단계는 tooassociate 서브넷 또는 특정 네트워크 인터페이스를 네트워크 보안 그룹입니다. 네트워크 보안 그룹은 서브넷과 hello 단계 tooassociate 다음을 수행 합니다.
    1. 너무 이동**서브넷**합니다.
    2. **+ 연결**을 클릭합니다.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. 가상 네트워크를 선택 하 고 hello 적절 한 서브넷을 선택 합니다.
    4. 클릭 **확인** toocreate hello 규칙입니다.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Hello 규칙을 만든 후 해당 세부 정보 toodetermine hello 공용 VIP (가상 IP) 주소를 볼 수 있습니다. 이 주소를 기록합니다.


