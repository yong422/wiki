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


  ## pyenv

  - pyenv install 진행시 openssl 별도 경로 추가

    - openssl 의 설치경로가 /usr/local/openssl1.0.2 일 경우.

    ```bash
    # python shared library 빌드 추가. python 2.7.13 을 설치할때.
    $ CFLAGS="-I/usr/local/openssl1.0.2/include" LDFLAGS="-L/usr/local/openssl1.0.2/lib" PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 2.7.13
    ```

  - pyenv run 실행시 dependency 라이브러리 미설치에 대한 해결방안

    - [참조](https://github.com/pypa/pipenv/issues/2093)