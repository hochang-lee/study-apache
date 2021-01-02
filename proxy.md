    1. proxy란?
    	서버와 클라이언트 사이의 중계 역할
    		클라이언트 - 프록시 - 서버
    		게이트웨이 역할

    	장점
    		서버로 요청됐던 내용을 캐싱해놓고 동일한 요청시 바로 응답할 수 있다.

    		클라이언트와 서버를 각각 숨길 수 있는 보안의 장점



    2. forward proxy의 필요성
 <div>
<img width='400' height='400' src="https://user-images.githubusercontent.com/63176389/103449693-590f4600-4cef-11eb-8ce1-3d5adac3ef05.png">
</div>

    		일반적으로 프록시라함은 포워드 프록시를 가리킨다

    		클라이언트는 실 서버를 타겟으로하는 요청을 프록시 서버로 보낸다. 이를 받은 프록시가 실 서버와 통신하여 결과값을 받아 클라이언트로 내려보낸다

    		클라이언트의 요청을 서버로 직접 요청하는 것이 아니라 프록시 서버를 거쳐서 요청 후 응답을 받는 형식
    			클라이언트를 감추는 역할을 한다.
    				서버가 응답받는 IP는 프록시 서버의 IP


    3. reverse proxy의 필요성



    	클라이언트는 리버스 프록시로 요청을 보낸다. 그러면 다른 서버에 있는 문서를 가져와서 클라이언트에게 전달할 수 있도록 해준다

    	서버를 감추는 역할을 한다
    		클라이언트는 리버스 프록시의 IP만을 확인할 수 있고 실제 서버의 IP를 알 수 없다

    	리버스 프록시를 통해 처리를 분산시킬 수 있다.

    	보안, 로드 밸런싱, 중앙 집중식의 인증의 경우 필요성이 대두된다.






    4. 기본 예제


    	Forward Proxy
    		ProxyRequests On
    		ProxyVia On

    		<Proxy *>
    		Order deny,allow
    		Deny from all
    		Allow from internal.example.com
    		</Proxy>


    	Reverse Proxy
    		ProxyRequests Off

    		<Proxy *>
    		Order deny,allow
    		Allow from all
    		</Proxy>

    		ProxyPass /foo http://foo.example.com/bar
    		ProxyPassReverse /foo http://foo.example.com/bar




    5. 주요 지시어
    	ProxyRequests
    		forward proxy 요청을 가능하게 한다

    	ProxyVia
    		via 응답 헤더에 담긴 정보를 제공한다
    			프록시 요청과 응답은 via header에 담긴다

    	ProxyPass
    		원격 서버를 로컬 서버의 url-space에 매핑시킨다.

    	ProxyPassReverse
    		리버스 프록시 서버로부터 보내진 HTTP 응답 헤더의 URL을 조정한다.


    6. 프록시 내용을 캐쉬할 경우 mod_cache 를 살펴볼 것
