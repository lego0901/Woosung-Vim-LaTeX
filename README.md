# Woosung Song의 LaTeX을 위한 Vim 설정 파일

자세한 건 모두 manual.pdf 파일으로 작성해놓았습니다.

완전히 처음 텍을 접하시는 분들을 위해 .tex 파일도 함께 업로드합니다.

**리눅스 환경**을 추천드립니다.

윈도우에서는 **bash**로 많이들 쓰더군요. 리눅스 설치가 불가하다면 이를 추천드립니다.

.vimrc 파일 관련된 사항은 [여기](https://github.com/lego0901/My-Vim-Settings)를 봐주세요.

감사합니다!

- C, C++, Java, Python 코딩
- Coq 코딩 및 실행
- LaTeX 파일 작성

정도 입니다.

주로 **Ubuntu 16.04 LTS, gvim 환경**에서 사용합니다. 플러그인은 미니멀하게 쓰는 것을 좋아하나, 다소 무거운 것들을 사용하기도 합니다. (YCM 포함) 이상하게 gvim이 스크립트 호환성이 더 좋은 것 같더라고요. 그냥 생으로 vim을 쓰는 것보다 더 추천합니다.

제가 쓰는 vimrc 파일과 C 코딩 템플릿, 그리고 coq_IDE.vim 의 수정본([출처](https://github.com/tauli/CoqIDE/commit/2e5578c8078c7aa60aee491d037cc6eed1ab3a8c)) 파일을 두도록 하겠습니다.



## 리눅스 설치 후 손볼 것들

아마, 굳이 이 글을 통해 설치하시는 분들은.. 제 동기들, 혹은 리눅스를 처음 접하시는 초보 분들일 것이라고 예상하여 메뉴얼을 자세히 적도록 하겠습니다.

- 우선 Ubuntu 설치를 마친 후 다음과 같은 코드로 필요한 패키지들을 모두 설치하였습니다.

  - 미니멀하게 쓰실 분 (**추천**)

    ```l
    $ sudo apt purge vim-tiny openjdk*
    $ sudo add-apt-repository 'ppa:webupd8team/java'

    $ sudo apt-get update
    $ sudo apt-get install oracle-java8-installer
    $ sudo apt-get install vlc git vim vim-nox build-essential cmake python-dev python3-dev clang kolourpaint4 gparted vim-gnome vim-gnome-py2

    $ git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim

    $ sudo update-alternatives --set vim /usr/bin/vim.gnome-py2
    ```

  - Tex, Coq, Typora(마크다운 툴) 등 제가 쓰는 세팅을 쓰실 분

    ```
    $ sudo apt purge vim-tiny openjdk*
    $ sudo add-apt-repository 'ppa:webupd8team/java'
    $ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
    $ sudo add-apt-repository 'deb https://typora.io ./linux/'

    $ sudo apt-get update
    $ sudo apt-get install oracle-java8-installer
    $ sudo apt-get install typora vlc git vim vim-nox build-essential cmake python-dev python3-dev clang texlive-full kolourpaint4 gparted coq vim-gnome vim-gnome-py2

    $ git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim

    $ sudo update-alternatives --set vim /usr/bin/vim.gnome-py2
    ```

  > - Java 등을 다른 방법으로 설치하고자 하시는 분들은 그러셔도 됩니다. 하지만 경험적으로 느낀 바로는 이 설치법이 가장 편한 것 같습니다.
  > - vlc, kolourpaint4, gparted 등은 되게 좋더라고요. 그래서 넣었습니다. 빼셔도 됩니다.명
  > - 마지막 줄 바로 위에 있는 코드는 vundle 이라는 플러그인을 사용하기 위한 발판입니다. 꼭 해주세요.

- 또, 이 repository 에 있는 파일은 **Clone or download** 버튼을 누른 뒤, 링크를 복사하여(Ctrl-c), 콘솔 창에

  ```
  $ git clone https://github.com/lego0901/My-Vim-Settings.git
  ```

  이렇게 입력해주시면 저장하실 수 있습니다.



## 파일 설명

YouCompleteMe는 Valloric([출처](https://github.com/Valloric/YouCompleteMe))의 repository 로부터 설치하였습니다. 설치 과정은 [neverapple88 님의 블로그](http://neverapple88.tistory.com/26)를 참고하였습니다.

다음은 각 파일에 대한 설명입니다.

- swsvimrc_before_plugin_install: vim을 깔고 아무 작업도 안 한 사용자 분들을 위한 설정 파일입니다. 다운 받으신 후 파일 이름 수정한 다음 ~/.vimrc 파일에 덮어쓰시면 됩니다.

  - 덮어쓰신 뒤 리눅스 terminal 을 열고

    ```
    $ vim +PluginInstall +qall
    ```

    을 입력하시면 플러그인이 설치됩니다.

  - YouCompleteMe 는 굉장히 무겁습니다. 설치 시간이 제법 오래 걸립니다.

  - 플러그인 설치가 끝나면 YouCompleteMe 세팅을 해줘야 합니다. [neverapple88 님의 블로그](http://neverapple88.tistory.com/26) 에서 설명을 긁어왔습니다.

    - 다음과 같은 코드로 컴파일 해주세요.

      ```
      $ ~/.vim/bundle/YouCompleteMe/install.py --clang-completer --system-libclang
      ```

    - 그 다음 ycm_extra_conf.py 파일을 ~/.vim 폴더 내에 복사 붙어넣기를 하세요. 숨겨진 폴더일텐데, Ctrl+h 버튼을 누르면 보일겁니다. 그런 뒤 파일 이름을 ".ycm_extra_conf.py" 으로 바꿔주세요. 앞에 점 하나만 붙이면 됩니다.

    - YCM Server ... 이런 메세지가 뜬다면 아마 python3 스크립트로 vim 이 돌아가고 있을 가능성이 큽니다. 이 코드로 해결 됩니다. 아치 리눅스에선 이 방식대론 잘 안 되던데, 저도 왜 그런지는 모르겠습니다.

      ```
      $ sudo update-alternatives --set vim /usr/bin/vim.gnome-py2
      ```

- swsvimrc.txt: 위 과정에서 플러그인을 설치한 후 마찬가지로 덮어쓰세요.

- swsvimrc_with_tex_coq.txt: Tex, coq 과 같은 프로그램을 사용할 분들이 쓰시면 됩니다. (아니면 전혀 필요가 없어요.)

  > 미니멀한 용도로 쓰실 분이 아니라면 가볍게 넘겨주시면 됩니다.

  - 몇 가지 수정이 필요합니다. 특히 coq 이 문제인데, ~/.vim/bundle/CoqIDE/plugin/coq_IDE.vim 파일을 제 repository에 있는 파일로 대체해주시면 해결 됩니다. ([출처](https://github.com/tauli/CoqIDE/commit/2e5578c8078c7aa60aee491d037cc6eed1ab3a8c))

- templates.zip: c.vim 을 쓰면 C, C++ 코딩을 왜 vim에서 하는지 알게 되실겁니다. 근데 너무 너저분하다는 생각도 들어서.. 이것도 손을 약간 봐주었습니다.

  > - 처음 .c, .cpp 파일을 만들었을 때 한 11줄 정도? 엄청 긴 주석이 자동으로 추가됩니다. 그걸 제거하고, #include \<stdio.h> 만 뜨도록 하였습니다.
  > - 단축키 "\isc", "\ip" 를 눌리면 scanf, printf 함수를 쓸 수 있게 되어있는데, 공백 처리와 같은 문제를 제 방식대로 바꿨습니다.

  - 사용법은 다음과 같습니다. 압축을 푼 뒤 templates 폴더 안의 내용을 복사하여 "~/.vim/bundle/c.vim/c-support/templates" 에 전부 덮어쓰시면 됩니다.




## 플러그인에 대한 간단한 설명

vundle, vim-fugitive, The-NERD-tree 이외의 플러그인에 대한 설명을 적겠습니다.

- a.vim, c.vim: C, C++ 코딩을 위한 플러그인입니다.

  - 단축키가 정말 많습니다. "\ip", "\isc", "\sfo" 등을 입력해보세요.

  - 단축키를 더 알고 싶다면 gvim 화면에서 콜론(:)을 찍고

    ```
    :set guioptions+=m
    ```

    을 입력하여 메뉴창을 띄웁시다. C/C++ 탭이 있을텐데, 거기서 여러 문법들을 확인할 수 있습니다.

- YouCompleteMe: 각종 코딩들에서 문법 체크(C, CPP) 및 자동완성을 시켜주는 플러그인입니다.

- coq.vim: Coq 을 사용하기 위한 플러그인입니다.

- CoqIDE: coq IDE 를 vim 에서 사용하기 위한 플러그인입니다. ([출처](http://cohama.hateblo.jp/entry/2014/04/27/194210))

- Solarized: 제가 좋아하는 색상 스킨입니다. ㅎㅎ



## vimrc 코드에 대한 설명

코드에 주석을 많이 달아놨습니다. 그래서 기능적인 부분만 설명하도록 하겠습니다.

- Ctrl-c, Ctrl-v 키를 이용해 다른 프로그램에서 복사한 것들 gvim 으로 붙어넣기 하거나, 반대의 작업을 실행할 수 있습니다.
- F2 키를 이용하여 NERDTree를 토글할 수 있습니다.
- F11 키를 이용하여 알맞는 화면 크기로 조정할 수 있습니다.
- .c, .cpp 파일에서 F3 키를 눌려 컴파일한 후, F4 키를 눌려 실행할 수 있습니다. 실행은 gnome-terminal 에서 구현됩니다.
- .java 파일 상에서 F3 키로 컴파일, F4 키로 실행할 수 있습니다. "\sysout" 단축키를 통해 System.out.println(); 코드를 빠르게 불러올 수 있습니다.
  - **주의**. java, javac 명령어는 콘솔을 실행하는 디렉토리의 위치에 영향을 많이 받습니다. NERDTree에서 소스코드가 담긴 폴더로 이동하여 "cd" 명령어를 입력하시면 잘 작동할 것입니다.
- .python 파일에서는 F3 키로 컴파일과 실행을 동시에 하실 수 있습니다.
  - python3 사용자 분들은 "au FileType python nmap \<F3> :! python %" 대신 "au FileType python nmap \<F3> :! python3 %"로 바꿔 사용하시면 됩니다.

