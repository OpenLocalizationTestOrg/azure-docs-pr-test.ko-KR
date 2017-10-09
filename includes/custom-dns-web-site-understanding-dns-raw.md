hello DNS 도메인 이름 ()는 hello에 사용 되는 toolocate 리소스 인터넷 합니다. 예를 들어 웹 페이지에서 링크를 클릭 하거나 브라우저에서 웹 앱 주소를 입력 하면 DNS tootranslate hello 도메인 IP 주소를 사용 합니다. hello IP 주소는 주소, 마치 있지만 매우 휴먼 활용이 편한 아닙니다. 예를 들어 이름인 훨씬 더 쉽게 tooremember DNS와 같은 **contoso.com** 는 것 보다 tooremember 192.168.1.88 또는 2001:0:4137:1f67:24a2:3888:9cce:fea3 같은 IP 주소입니다.

hello DNS 시스템에 따라 *레코드*합니다. 레코드는 *contoso.com*과 같은 구체적인 **이름**을 IP 주소 또는 DNS 이름과 연결합니다. DNS에서 이름을 찾습니다 웹 브라우저 같은 응용 프로그램을 그 hello 레코드를 찾을 사용 하는 경우 모든 것을 나타내는 tooas hello 주소입니다. Hello 값 포인트 toois IP 주소, hello 브라우저는 해당 값을 사용 합니다. Tooanother DNS 이름, 가리키면 hello 응용 프로그램에 한 toodo 해상도 다시 있습니다. 최종적으로 모든 이름 확인은 IP 주소 확인으로 완료됩니다.

앱 서비스에서 웹 앱을 만들 DNS 이름이 toohello 웹 응용 프로그램 자동으로 할당 됩니다. 이 이름은의 hello 형식을 취합니다  **&lt;yourwebappname&gt;. azurewebsites.net**합니다. 이기도 가상 IP 주소를 사용 하기 위해 사용할 수 있는 레코드 DNS를 만들 때 만들 수 있도록 하거나 레코드 해당 지점 toohello **. azurewebsites.net**, 또는 toohello IP 주소를 가리키도록 설정할 수 있습니다.

> [!NOTE]
> 삭제 및 웹 응용 프로그램을 다시 만들 hello 앱 서비스 계획 모드도 변경 하거나 웹 응용 프로그램의 hello IP 주소가 변경 됩니다**무료** 너무 설정 된 후**기본**, **Shared**, 또는 **표준**합니다.
> 
> 

레코드의 유형은 여러 가지이며 각 유형에는 고유한 함수 및 제한이 있지만 웹앱의 경우 *A* 및 *CNAME* 레코드, 두 가지만 주의하면 됩니다.

### <a name="address-record-a-record"></a>주소 레코드(A 레코드)
A 레코드와 같은 도메인을 매핑합니다 **contoso.com** 또는 **www.contoso.com**, *또는 와일드 카드 도메인* 같은  **\*. contoso.com**, tooan IP 주소입니다. 앱 서비스에서 웹 앱의 경우 hello hello 서비스 또는 웹 앱에 대 한 구매 하는 특정 IP 주소를 가상 IP hello 중 하나입니다.

hello CNAME 레코드를 통해 A 레코드의 주요 이점은 다음과 같습니다.

* 와 같은 루트 도메인을 매핑할 수 있습니다 **contoso.com** tooan IP 주소; 많은 허용 등록 A 레코드를 사용 하 여이
* **\*.contoso.com**과 같이 와일드카드를 사용하는 하나의 항목만 지정하고, 이 항목 하나로 **mail.contoso.com**, **blogs.contoso.com** 또는 **www.contso.com**과 같은 여러 하위 도메인에 대한 요청을 처리할 수 있습니다.

> [!NOTE]
> A 레코드 매핑되어 있으므로 tooa 고정 IP 주소, 웹 응용 프로그램의 변경 내용을 toohello IP 주소를 자동으로 해결 수 없습니다. 웹 앱에 대 한 사용자 지정 도메인 이름 설정을 구성할 때 IP 주소는 레코드와 함께 사용 하기 위해 제공 됩니다. 하지만이 값을 삭제 및 웹 응용 프로그램을 다시 만들 hello 앱 서비스 계획 모드 tooback도 변경 하거나 변경 될 수 있습니다**무료**합니다.
> 
> 

### <a name="alias-record-cname-record"></a>별칭 레코드(CNAME 레코드)
매핑하는 CNAME 레코드는 *특정* 같은 DNS 이름 **mail.contoso.com** 또는 **www.contoso.com**, tooanother (정식) 도메인 이름입니다. 앱 서비스 웹 앱의 경우 hello hello 정규 도메인 이름은 hello  **&lt;yourwebappname >. azurewebsites.net** 웹 앱의 도메인 이름입니다. Hello CNAME 만듭니다 hello에 대 한 별칭을 만든 후  **&lt;yourwebappname >. azurewebsites.net** 도메인 이름입니다. hello CNAME 항목 toohello IP 주소를 확인 합니다 프로그램  **&lt;yourwebappname >. azurewebsites.net** hello 웹 앱의 hello IP 주소가 변경 되 면 없는 tootake 조치 하므로 자동으로 도메인 이름입니다.

> [!NOTE]
> 일부 도메인 등록 기관에서는 toomap 하위 도메인 같은 CNAME 레코드를 사용할 경우 **www.contoso.com**, 및 하지와 같은 이름, 루트 **contoso.com**합니다. CNAME 레코드에 대 한 자세한 내용은 사용자 등록 기관에서 제공 하는 hello 설명서를 참조 하십시오. <a href="http://en.wikipedia.org/wiki/CNAME_record">CNAME 레코드에 대 한 Wikipedia 항목 hello</a>, 또는 hello <a href="http://tools.ietf.org/html/rfc1035">IETF 도메인 이름-구현 및 사양</a> 문서입니다.
> 
> 

### <a name="web-app-dns-specifics"></a>웹앱 DNS 설명
A 레코드를 사용 하 여 웹 앱과 toofirst hello TXT 레코드를 다음 중 하나를 만듭니다.

* **Hello 루트 도메인에 대 한** -A DNS TXT 레코드의  **@**  너무  **&lt;yourwebappname&gt;. azurewebsites.net**합니다.
* **특정 하위 도메인에 대 한** -의 DNS 이름을  **&lt;하위 도메인 >** 너무**&lt;yourwebappname&gt;. azurewebsites.net**합니다. 예를 들어 **블로그** hello 레코드에 대 한 경우 **blogs.contoso.com**합니다.
* **와일드 카드 하위-dodmains hello에 대 한** -A DNS TXT 레코드의 * * * 너무  **&lt;yourwebappname&gt;. azurewebsites.net**합니다.

이 TXT 레코드는 사용 되는 tooverify toouse 넣을 hello 도메인을 소유 합니다. 또한 웹 응용 프로그램의 toohello 가상 IP 주소를 가리키는 toocreating A 레코드입니다.

Hello IP 주소를 찾을 수 있습니다 및 **. azurewebsites.net** 다음 단계를 수행 하 여 웹 앱에 대 한 이름을 hello:

1. 브라우저를 열고 hello [Azure 포털](https://portal.azure.com)합니다.
2. Hello에 **웹 앱** 블레이드에서 hello 웹 응용 프로그램 이름을 클릭 한 다음 선택 **사용자 지정 도메인** hello hello 페이지 아래에서 합니다.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Hello에 **사용자 지정 도메인** 블레이드에서 나타납니다 hello 가상 IP 주소입니다. 이 정보는 DNS 레코드를 만들 때 사용되므로 저장합니다.
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > 사용자 지정 도메인 이름을 사용할 수 없습니다는 **무료** 너무 hello 앱 서비스 계획을 업그레이드 해야 하 고 웹 앱,**Shared**, **기본**, **표준**, 또는 **프리미엄** 계층입니다. 앱 서비스 hello에 대 한 자세한 내용은 계획의 가격 책정 계층을 어떻게 toochange hello 웹 응용 프로그램의 가격 책정 계층을 포함 하 여, 참조 [어떻게 tooscale 웹 앱](../articles/app-service-web/web-sites-scale.md)합니다.
   > 
   > 

