  

	1. mod_cache 의 필요성
		컴퓨터의 내용 또는 프록시된 내용을 캐시할 수 있도록 한다.
		
	2. 저장 관리 모듈
		mod_cache 사용시 저장 관리 모듈이 필요하다. 아파치에는 2가지 존재
		
			mod_cache_disk
				디스크 기반의 저장 관리자 
				
				header와 body는 별도로 디스크에 저장된다
					캐싱된 url을 md5 해시를 통해 파생된 디렉토리 구조에 저장
				
				부분 컨텐츠의 캐싱은 지원하지 않는다
			
			
			mod_cache_socache
				공유가능한 객체 기반의 저장 관리자
				
				header와 body는 캐시된 응답 url에 따라 단일 키와 함께 저장된다
				
				부분 컨텐츠의 캐싱은 지원하지 않는다
				
			
	3. 기본 예제
		httpd.conf
		
          LoadModule cache_module modules/mod_cache.so
	    <IfModule mod_cache.c>
		LoadModule cache_disk_module modules/mod_cache_disk.so
		<IfModule mod_cache_disk.c>
		    CacheRoot "c:/cacheroot"
		    CacheEnable disk  "/"
		    CacheDirLevels 5
		    CacheDirLength 3
		</IfModule>
		  # When acting as a proxy, don't cache the list of security updates
		CacheDisable "http://security.update.server/update-list/"
	    </IfModule>
			
		


	4. 주요 지시어
		CacheRoot
			캐시 파일이 저장된 최상위 디렉토리
			
		CacheDirLevels
			캐시 하위 디렉토리 레벨
			
		CacheDirLength
			하위 디렉터리 이름의 문자 수
		
		CacheDisable
			캐시하지 않을 Url을 지정할 수 있다
			
		CacheEnable
			특정 저장 관리자에 지정된 url을 캐시할 수 있다.
	
			
