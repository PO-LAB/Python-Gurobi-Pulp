# Installation for ubuntu
在此使用ubuntu 17.04和ubuntu 17.10做為示範環境，假如你有python3.6，應該都會成功

不過因為ubuntu 17.10才會預裝gurobi7.5.1需要的python3.6.3，所以還是建議使用17.10來建置環境
另外因為ubuntu可以裝起來，所以debian或其他相關Linux發行版應該也可以。


## Prerequistie
- Python 3.6 or Python 2.7 (or upper version)
- bash

## 1. download & install the software

- 先去[官網](http://www.gurobi.com/downloads/gurobi-optimizer)下載，在這邊我選的是Gurobi 7.5.1

- 首先你會需要解壓縮

```sh
$ tar zxvf gurobi7.5.1_linux64.tar.gz
```

- 將解壓縮後的檔案，搬遷到`/opt/`底下

```sh
$ cp -r gurobi751 /opt/
```

## 2. 設定全域變數
 
- 將以下複製到`.bashrc`上

```sh
export GUROBI_HOME="/opt/gurobi751/linux64"
export PATH="${PATH}:${GUROBI_HOME}/bin"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"
```

- 其中GUROBI_HOME對應到你剛剛將解壓縮後的檔案放置於哪裡

- ![](/Installation/picture/003.png)

## 3. Request Academic License
 
- 去[官網](https://user.gurobi.com/download/licenses/free-academic)要求Licenses，應該會得到一串prompt `grbgetkey **********`
- 直接在你的終端機上下指令
- ![](/Installation/picture/001.png)

- 那麼就會在你的指定路徑上生成特定檔案
- ![](/Installation/picture/002.png)

## 4. 再次設定全域變數

- 將以下複製到`.bashrc`上

```sh
export GRB_LICENSE_FILE="/home/kuoteng/gurobi.lic"
```

- GRB_LICENSE_FILE則是對應到LICENSES FILE的位置

## 5. 設定python interface

- 移動到你剛剛解壓縮後檔案放置位置

```sh
$ cd /opt/gurobi751/linux64
```

- 輸入以下指令（你可以打開virtualenv來執行）
```sh
$ sudo python3 setup.py install
```



## 5. Try yourself

- 自己嘗試看看吧
- ![](/Installation/picture/004.png)

## Author

Kuo Teng, Ding



