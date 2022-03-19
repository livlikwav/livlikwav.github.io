
# Jekyll guide

> ruby, jekyll 은 매번 헷갈린다. repo에 파일로 그냥 저장해두자.
> 이제와서 hugo로 바꾸기엔 마음에 드는 테마도 없고, 넘 귀찮은 것...

## Use-cases

- 로컬 테스트 서버 실행
  - `bundle exec jekyll serve`

## Knowledges

> 가만~히 냅둔 블로그 오랜만에 와서 다시 수정하려고 하면, 이상한 의존성 문제가 발생한다;;
> 그냥 하라는대로만 하자...

- [Mac에서 Gem::FilePermissionError 에러 발생시 해결 방법](https://jojoldu.tistory.com/288)
- [Bundler::GemNotFound 해결 방법](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=cyydo96&logNo=221588642260)
- [왜 jekyll serve 가 안될까?](https://frhyme.github.io/others/jekyll_serve_not_work/)
- [jekyll 실행 시킬 때 `require': cannot load such file -- webrick (LoadError) 오류가 난다면 bundle add webrick](https://junho85.pe.kr/1850)

- 기초
  - gem: Ruby의 패키지 매니저
  - gemfile: bundler에서 사용하는 의존성 파일
  - bundler: 일일히 gem설치를 할수 없기에 한번에 해결해주는 프로그램
    - bundle install, bundle update 명령어를 통해 일괄적으로 처리가 가능
    - bundle은 gemfile에 정의된 gem들의 의존성을 파악해 사용할 수 있게 해줌
