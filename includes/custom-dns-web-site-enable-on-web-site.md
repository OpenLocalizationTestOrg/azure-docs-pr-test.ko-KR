도메인 이름에 대 한 hello 레코드를 전파 웹 앱과 연결 해야 합니다. 다음 웹 브라우저를 사용 하 여 단계 tooenable hello 도메인 이름을 hello를 사용 합니다.

> [!NOTE]
> TXT 레코드 hello DNS 시스템을 통해 이전 단계 toopropagate hello에서에서 만든 약간의 시간이 걸릴 수 있습니다. Hello TXT 레코드에 전파 될 때까지 tooyour 웹 응용 프로그램의 hello 도메인 이름을 추가할 수 없습니다. A 레코드를 사용 하는 hello 이전 단계에서 만든 hello TXT 레코드에 전파 될 때까지 hello 레코드 도메인 이름 tooyour 웹 응용 프로그램을 추가할 수 없습니다.
> 
> 와 같은 서비스를 사용할 수 <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> TXT 레코드 hello tooverify를 사용할 수 있습니다.
> 
> 

1. 브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **웹 앱** 탭, 웹 앱의 hello 이름을 클릭 한 다음 선택 **사용자 지정 도메인이**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Hello에 **사용자 지정 도메인** 블레이드에서 클릭 **호스트 이름 추가**합니다.
4. 사용 하 여 hello **Hostname** 텍스트 상자 tooenter hello 도메인 이름 tooassociate이 웹 앱과.
   
    ![](./media/custom-dns-web-site/add-custom-domain.png)
5. **유효성 검사**를 클릭합니다.
6. **유효성 검사** 를 클릭하면 Azure에서 도메인 검증 워크플로가 시작됩니다. 도메인 소유권으로 호스트 이름 가용성과 보고서의 성공 또는 된 규범적인 부모의 toofix 오류 hello 하는 방법에 자세한 오류 체크 인 됩니다.    

이 시점에서 브라우저에서 수 tooenter hello 사용자 지정 도메인 이름 이어야 하 고는 성공적으로 장에서 tooyour 웹 응용 프로그램을 참조 해야 합니다.

