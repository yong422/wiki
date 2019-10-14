# python

## install

- python version 3.7 이상 설치시 `ModuleNotFoundError: No module named '_ctypes'` 오류

  ```bash
  File "/tmp/tmpov0v7ywd/pip-18.1-py2.py3-none-any.whl/pip/_internal/cli/main_parser.py", line 12, in <module>
  File "/tmp/tmpov0v7ywd/pip-18.1-py2.py3-none-any.whl/pip/_internal/commands/__init__.py", line 6, in <module>
  File "/tmp/tmpov0v7ywd/pip-18.1-py2.py3-none-any.whl/pip/_internal/commands/completion.py", line 6, in <module>
  File "/tmp/tmpov0v7ywd/pip-18.1-py2.py3-none-any.whl/pip/_internal/cli/base_command.py", line 18, in <module>
  File "/tmp/tmpov0v7ywd/pip-18.1-py2.py3-none-any.whl/pip/_internal/download.py", line 38, in <module>
  File "/tmp/tmpov0v7ywd/pip-18.1-py2.py3-none-any.whl/pip/_internal/utils/glibc.py", line 3, in <module>
  File "/tmp/python-build.20190820090624.7749/Python-3.7.2/Lib/ctypes/__init__.py", line 7, in <module>
    from _ctypes import Union, Structure, Array
  ModuleNotFoundError: No module named '_ctypes'
  ```

  - c compiler 로 빌드된 라이브러리에 python 인터프리터가 접근하기 위핸 인터페이스 라이브러리가 설치되지 않아서 발생하는 문제.
  - libffi-devevl 설치하여 문제 해결

## pyenv & python 설치

- pyenv 를 사용할 로컬계정에 pyenv 설치.

```bash
$ git clone https://github.com/yyuu/pyenv.git ~/.pyenv
$ git clone https://github.com/yyuu/pyenv-virtualenv.git \
          ~/.pyenv/plugins/pyenv-virtualenv
```

- pyenv 를 위한 환경변수 추가 (.bashrc , .bash_profile , .zshrc)

```bash
# Add 'pyenv' to PATH.
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"

# Enable shims and autocompletion for pyenv.
eval "$(pyenv init -)"
# Load pyenv-virtualenv automatically by adding
# # the following to ~/.zshrc:
#
eval "$(pyenv virtualenv-init -)"
```

- install python with shared libpython(necessary for PyInstaller to work)

```bash
env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 2.7.13 # 설치하려는 버전.
```

- 설치한 python 으로 환경 설정 및 pipenv 설치

```bash
pyenv global 2.7.13
pip install pipenv
```


## pipenv

- python 전용 가상환경 설정 패키지로 pip 을 이용
- Pipfile 이 존재하는 프로젝트에서 실행시.

  ```bash
  # Pipfile 에 등록된 패키지를 가상환경으로 설치.
  $ python install
  # python 가상 환경으로 shell 변경
  $ python shell
  ```

## pyenv

- pyenv install 진행시 openssl 별도 경로 추가

  - openssl 의 설치경로가 /usr/local/openssl1.0.2 일 경우.

  ```bash
  # python shared library 빌드 추가. python 2.7.13 을 설치할때.
  $ CFLAGS="-I/usr/local/openssl1.0.2/include" LDFLAGS="-L/usr/local/openssl1.0.2/lib" PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 2.7.13
  ```

- pyenv run 실행시 dependency 라이브러리 미설치에 대한 해결방안

  - [참조](https://github.com/pypa/pipenv/issues/2093)