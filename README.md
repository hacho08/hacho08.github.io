

# Jekyll 블로그 시작하기!

Github Page를 활용해 별도의 호스팅 없이 git repository를 이용해 Jekyll 블로그를 시작한 과정을 담아보았습니다.


## 준비하기

[Jekyll Docs](https://jekyllrb.com/docs/installation/) 를 참고하여 `Ruby`, `RubyGems`, `Jekyll`, 그리고 `Bundler`를 설치 해 주었습니다.


## 시작하기

`jekyll new . --force`라는 명령어를 입력하여 제가 작업하고 있던 디렉토리에 Jekyll을 설치했습니다.

`bundle exec jekyll serve` 로 Jekyll serve 실행 후 웹에서 localhost:4000에 접속해서 제가 만든 기본 테마로 된 Jekyll 사이트가 만들어진 것을 확인했습니다.


## 적용한 기능
1. 테마 변경
2. favicon 및 메인 이미지 적용
3. post 작성
4. Google Analytics 적용
5. 댓글 기능 적용 


## 테마 변경하기

마음에 드는 테마를 고르고 골라 [jekyll-theme-chirpy](https://github.com/cotes2020/jekyll-theme-chirpy) 라는 테마로 하기로 결정하고 로컬로 `git clone` 을 했습니다.
의존성을 감안하여 _posts를 제외하고 테마를 덮어씌우라고 배웠지만 저는 _posts에 내용을 따로 저장해두었기 때문에 모든 폴더를 덮어씌웠습니다.
직후 `bundle exec jekyll serve` 를 했더니 'Could not find gem 'html-proofer (~> 3.18)' in locally installed gems.
Run 'bundle install' to install missing gems.' 이런 에러가 발생해서 `bundle` 이라는 명령어로 dependencies를 설치해 주었습니다.

테마가 잘 적용된 것을 확인하고 _config.yml 부터 하나씩 내용을 변경했습니다.
생각보다 순조로운 테마 변경하기였습니다.


## favicon 및 메인 이미지 변경하기

### favicon
[Real Favicon Generator](https://realfavicongenerator.net/)에 들어가서 원하는 이미지를 넣고 favicon에 맞는 사이즈들로 zip파일을 다운받았습니다.
압축을 풀고 
- `browserconfig.xml`
- `site.webmanifest`

위 두개의 파일을 삭제 한 후 나머지 png, ico 파일들을 `assets/img/favicons/` 경로로 이동시켜주었습니다. 

### 메인 이미지
_config.yml에서 옵션들 중 img_cdn과 avatar이라는 옵션을 변경해 주었습니다. 
img_cdn 은 'https://hacho08.github.io' 로 avatar는 `/assets/img/meIcon.png` 이미지 파일 경로를 넣어주었습니다. 
로컬에서 볼 때는 이미지가 아직 리모트에 올라가지 않아서 보이지 않았지만 한번 푸시 해주고 난 후로는 잘 보였습니다.


## GitPages에 올리기

Git에 푸시를 했는데 'GitHub Pages failed to build your site.' 라는 에러가 뜨고 블로그에 반영이 되지 않았습니다 ㅠㅠ 
한참을 해매다가 해당 테마의 readme를 다시 천천히 읽으며 따라 해 보았습니다.
보안상의 이유로 Github Pages가 safe 모드로 빌드를 하기 때문에 플러그인 사용을 하는 것을 막아서 그렇다고 하는데요 이를 해결하기 위해  GitHub Actions 을 사용해 사이트를 빌드해주면 된다고 합니다. 이렇게 할 경우 새로운 브랜치를 만들어서 Github Pages의 source로 사용한다고 해요.

1. '_config.yml'의 'url'은 'https://hacho08.github.io' 이렇게 바꿔주고 'baseurl'은 그냥 ''로 놔둡니다. (저는 /<repository name>으로 해놨다가 한참 뒤에 잘못 된걸 알고 바꿔줬어요 ㅠㅠ 프로젝트가 별개로 있을때만 /<프로젝트명>을 해주는 것 같아요)
2. `.github/workflows/pages-deploy.yml` ,  `tools/deploy.sh` 해당 위치에 두 파일이 잘 있는지 확인했습니다. 저의 경우 .github라는 폴더는 없었기 때문에 폴더들과 파일을 만들어 주었습니다. 
3. Gemfile.lock도 올려주었기 때문에 linux를 사용하지 않으면 
```console
$ bundle lock --add-platform x86_64-linux
```
이것도 해줘야했습니다.

이렇게 해주고 난 후 푸시를 했더니 새로운 gh-pages라는 브랜치가 생겼습니다.
마지막으로 Github에 들어가서 Setting 탭에 들어간 후 Pages를 왼쪽 네브바에서 선택해서 들어가면 Source라는 부분이 보이는데요 여기서 branch를 master가 아닌 `gh-pages`로 변경해주고 저장을 해주었습니다.

이렇게만 하면 될 줄 알았더니..
분명 로컬에서는 페이지가 멀쩡히 나왔었는데 블로그 UI가 다 깨져있는게 아니겠어요...
이유를 찾고 찾던 중에 baseurl 을 확인해보라는 글을 보게 되었고 위에서 언급했던 baseurl을 그냥 빈칸으로 놔두고 다시 푸시를 했더니 해결 되었습니다!


## Lesson Learned

**Github의 readme를 꼼꼼히 읽자!!!**



