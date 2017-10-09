도메인 이름에 대 한 hello 레코드를 전파 해야 사용자 지정 도메인 이름을 수 있는 사용자 브라우저 tooverify 수 toouse 수 사용된 tooaccess Azure 앱 서비스의 웹 응용 프로그램 수입니다.

> [!NOTE]
> Hello DNS 시스템을 통해 프로그램 CNAME toopropagate 약간의 시간이 걸릴 수 있습니다. 와 같은 서비스를 사용할 수 <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> CNAME hello tooverify를 사용할 수 있습니다.
> 
> 

트래픽 관리자 끝점으로 웹 앱을 이미 추가 하지 않은 경우 이렇게 해야 hello 사용자 지정 도메인 이름 경로 tooTraffic 관리자와 이름 확인이 작동 합니다. 트래픽 관리자는 다음 tooyour 웹 응용 프로그램을 라우팅합니다. Hello 정보에 사용 하 여 [추가 / 삭제 끝점](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd 트래픽 관리자 프로필에서 끝점으로 웹 앱입니다.

> [!NOTE]
> 끝점을 추가할 때 웹앱이 목록에 나열되지 않는 경우 웹앱이 **표준** 앱 서비스 계획 모드로 구성되었는지 확인합니다. 사용 해야 **표준** 순서 toowork 트래픽 관리자에서에서 웹 응용 프로그램에 대 한 모드입니다.
> 
> 

1. 브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **웹 앱** 탭을 선택 하면 웹 앱의 hello 이름을 클릭 **설정**를 선택한 후 **사용자 지정 도메인이**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Hello에 **사용자 지정 도메인** 블레이드에서 클릭 **호스트 이름 추가**합니다.
4. 사용 하 여 hello **Hostname** 텍스트 상자 tooenter hello 트래픽 관리자 도메인 이름 tooassociate이 웹 앱과.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. 클릭 **유효성 검사** toosave hello 도메인 이름 구성 합니다.
6. **유효성 검사** 를 클릭하면 Azure에서 도메인 검증 워크플로가 시작됩니다. 도메인 소유권으로 호스트 이름 가용성과 보고서의 성공 또는 된 규범적인 부모의 toofix 오류 hello 하는 방법에 자세한 오류 체크 인 됩니다.    
7. 유효성을 검사 **호스트 이름 추가** 단추가 활성화 됩니다 고 수 toohello 할당 호스트 이름이 됩니다. 브라우저에서 사용자 지정 도메인 이름을 tooyour 이제 이동 합니다. 이제 사용자 지정 도메인 이름을 사용하여 앱이 실행되고 있음을 확인할 수 있습니다. 
   
   Hello 사용자 지정 도메인 이름을 hello에 나열 됩니다 구성 완료 되 면 **도메인 이름** 웹 앱의 섹션입니다.

이 시점에서 브라우저에서 수 tooenter hello 트래픽 관리자 도메인 이름 이름 이어야 하 고는 성공적으로 장에서 tooyour 웹 응용 프로그램을 참조 해야 합니다.

