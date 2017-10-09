hello DNS 도메인 이름 ()는 hello 요소를 사용 하는 toolocate 인터넷 합니다. 예를 들어 브라우저의 주소를 입력 하거나 웹 페이지에서 링크를 클릭 합니다. DNS tootranslate hello 도메인 IP 주소를 사용 합니다. hello IP 주소는 주소, 마치 있지만 매우 휴먼 활용이 편한 아닙니다. 예를 들어 이름인 훨씬 더 쉽게 tooremember DNS와 같은 **contoso.com** 는 것 보다 tooremember 192.168.1.88 또는 2001:0:4137:1f67:24a2:3888:9cce:fea3 같은 IP 주소입니다.

hello DNS 시스템에 따라 *레코드*합니다. 레코드는 *contoso.com*과 같은 구체적인 **이름**을 IP 주소 또는 DNS 이름과 연결합니다. DNS에서 이름을 찾습니다 웹 브라우저 같은 응용 프로그램을 그 hello 레코드를 찾을 사용 하는 경우 모든 것을 나타내는 tooas hello 주소입니다. Hello 값 포인트 toois IP 주소, hello 브라우저는 해당 값을 사용 합니다. Tooanother DNS 이름, 가리키면 hello 응용 프로그램에 한 toodo 해상도 다시 있습니다. 최종적으로 모든 이름 확인은 IP 주소 확인으로 완료됩니다.

Azure 웹 사이트를 만들 때 DNS 이름은 toohello 사이트를 자동으로 할당 됩니다. 이 이름은의 hello 형식을 취합니다  **&lt;yoursitename&gt;. azurewebsites.net**합니다. Azure 트래픽 관리자 끝점으로 웹 사이트를 추가 하면 다음 웹 사이트는 hello를 통해 액세스할 수 있는  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** 도메인입니다.

> [!NOTE]
> 웹 사이트의 트래픽 관리자 끝점으로 구성 되 면 hello 사용할 **. trafficmanager.net** DNS 레코드를 만들 때 처리 합니다.
> 
> 트래픽 관리자에는 CNAME 레코드만 사용할 수 있습니다.
> 
> 

또한 여러 종류의 레코드, 각기 고유한 기능 및 제한, 사항이 없지만 구성 된 웹 사이트 tooas 트래픽 관리자 끝점에 대 한만 할까요 하나에 대 한; *CNAME* 레코드입니다.

### <a name="cname-or-alias-record"></a>CNAME 또는 별칭 레코드
매핑하는 CNAME 레코드는 *특정* 같은 DNS 이름 **mail.contoso.com** 또는 **www.contoso.com**, tooanother (정식) 도메인 이름입니다. Hello 정식 도메인 이름이 트래픽 관리자를 사용 하 여 Azure 웹 사이트의 경우 hello는 hello  **&lt;myapp >. trafficmanager.net** 트래픽 관리자 프로필의 도메인 이름입니다. Hello CNAME 만듭니다 hello에 대 한 별칭을 만든 후  **&lt;myapp >. trafficmanager.net** 도메인 이름입니다. hello CNAME 항목 toohello IP 주소를 확인 합니다 프로그램  **&lt;myapp >. trafficmanager.net** hello 웹 사이트의 hello IP 주소가 변경 되 면 없는 tootake 조치 하므로 자동으로 도메인 이름입니다.

트래픽 관리자에 도착 하는 트래픽이 되 면 다음 hello 부하 분산 용으로 구성할 방법을 사용 하 여 hello 트래픽 tooyour 웹사이트를 라우팅합니다. 이 완전히 투명 하 게 toovisitors tooyour 웹사이트입니다. 브라우저에서 사용자 지정 도메인 이름을 hello만 표시 됩니다.

> [!NOTE]
> 일부 도메인 등록 기관에서는 toomap 하위 도메인 같은 CNAME 레코드를 사용할 경우 **www.contoso.com**, 및 하지와 같은 이름, 루트 **contoso.com**합니다. CNAME 레코드에 대 한 자세한 내용은 사용자 등록 기관에서 제공 하는 hello 설명서를 참조 하십시오. <a href="http://en.wikipedia.org/wiki/CNAME_record">CNAME 레코드에 대 한 Wikipedia 항목 hello</a>, 또는 hello <a href="http://tools.ietf.org/html/rfc1035">IETF 도메인 이름-구현 및 사양</a> 문서입니다.
> 
> 

