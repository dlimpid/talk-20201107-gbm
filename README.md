# Gradient boosting tree를 이용한 데이터 분석

2020년 11월 7일, 2020 NIMS 산업수학 아카데미

## 계산 환경 설정

0. 주의사항

   - ℹ️ 인터넷 환경이나 컴퓨터에 따라 달라질 수 있으나 처음부터 끝까지 진행하는
     데 대략 10분에서 30분 정도가 걸립니다.
   - ℹ️ 스스로 계산 환경 설정이 가능하신 분은, 아래 과정을 똑같이 따르지 않아도
     `environment.yml`을 참조하여 본인이 사용 가능한 환경을 설정하셔도 됩니다.
   - ⚠️ Windows의 사용자 이름에 한글이 들어가는 경우, 아래 과정대로 기본
     옵션으로 설치시 설치 경로에 한글이 포함되어 제대로 동작하지 않는 경우가
     있습니다. 사용자 이름만 바꿔서는 이미 만들어진 사용자 디렉터리 이름은
     바뀌지 않으므로, 아래 과정 중 Anaconda나 Miniconda를 다른 곳(예:
     `C:\Aanaconda3`, `C:\opt\Miniconda3` 등)에 설치해 보세요.

1. 본인의 OS에 맞는 [Miniconda]\(추천)나 [Anaconda]를 설치합니다. 둘 중 하나
   이상이 이미 설치되어 있는 경우 다시 설치할 필요 없이, 기존에 설치된
   Miniconda나 Anaconda를 그대로 사용하시면 됩니다.

2. 터미널을 실행합니다.

   - ℹ️ 터미널 실행 방법

     - Windows: 시작 → Anaconda3 (64-bit) → Anaconda Prompt

       ("Anaconda Prompt (anaconda3)"나 "Anaconda Prompt (miniconda3)" 등일 수도
       있음)

     - macOS: Launchpad → 터미널

   - ℹ️ 터미널 명령줄은 OS나 환경에 따라 `(base) C:\Users\myusername>`,
     `bash3.2$`, `MacBook:~$`, `>` 등 다양한 형식으로 보일 수 있습니다. 아래에
     나오는 내용을 입력할 때에는 `$` 표시 다음 부분만 입력하면 됩니다.

3. Miniconda(Anaconda)가 실행되는 현재 디렉터리를 확인합니다.

   - Windows

     기본값으로 `C:\Users\<myusername>` 이고, 파일 탐색기에서는
     `C:\사용자\<myusername>`로 찾아가야 할 수도 있습니다. 확실하지 않은 경우
     터미널을 실행하면 볼 수 있습니다.

     ```sh
     (base) C:\Users\myusername>
     ```

   - macOS

     기본값으로 `/Users/<myusername>`이고, 확실하지 않은 경우 터미널에서 `pwd`
     명령어로 확인할 수 있습니다.

     ```sh
     (base) $ pwd
     /Users/myusername
     ```

4. (macOS 한정) OpenMP를 설치합니다.

   - [Homebrew](https://brew.sh/)를 설치합니다.

   - 다음을 입력하여 OpenMP를 설치합니다.

     ```sh
     brew install libomp
     ```

5. 터미널에서 `environment.yml` 파일이 있는 위치로 이동하여 다음을 입력하여 계산
   환경을 만듭니다.

   ```sh
   (base) $ conda env create -f environment.yml
   ```

   마지막에 다음과 비슷한 메시지가 나왔으면 제대로 설치된 것입니다.

   ```plain
   ...
   done
   #
   # To activate this environment, use
   #
   #     $ conda activate gbm
   #
   # To deactivate an active environment, use
   #
   #     $ conda deactivate
   ```

   ℹ️ 여기까지 한 번 진행하면 이후에는 이 위는 다시 할 필요가 없습니다.

6. 계산 환경을 활성화합니다.

   ```sh
   (base) $ conda activate gbm
   ```

7. `gbm` 환경이 활성화된 것을 확인하고, JupyterLab을 실행합니다.

   ```sh
   (gbm) $ jupyter lab
   ```

   JupyterLab을 마치려면 (파일을 모두 저장했는지 확인하고) File → Shut down을
   누르거나, 터미널에서 Ctrl-C를 입력합니다.

   ⚠️ JupyterLab에서는 보안상의 이유로 위의 명령어를 실행하는 위치의 하위
   디렉터리에만 접근할 수 있습니다. 예를 들어 `C:\Users\myusername`에서
   실행했다면 `C:\Users\myusername\myproject` 등의 디렉터리에는 접근 가능하지만,
   `D:\data` 등 다른 디렉터리에는 접근할 수 없습니다.

   💡 (선택사항) 터미널에 익숙하신 경우 JupyterLab 실행 위치를 그대로 따르지
   않아도 `cd` 등으로 원하는 위치로 이동하거나, `jupyter lab
   --notebook-dir="D:\my\favorite\path"` 처럼 경로를 지정하셔서 실행하셔도
   괜찮습니다.

8. 터미널을 닫았다가 다시 실행하려면 계산 환경 활성화부터만 진행하면 됩니다.

## 기타

- 계산 환경을 삭제하려면 (현재 환경을 활성화했으면 먼저 환경에서 빠져나간 후)
  `conda remove -n gbm --all`을 입력합니다.

  ```sh
  (gbm) $ conda deactivate
  (base) $ conda remove -n gbm --all
  ```

[Anaconda]: https://www.anaconda.com/distribution/
[Miniconda]: https://docs.conda.io/en/latest/miniconda.html
