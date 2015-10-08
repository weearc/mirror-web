## Android 镜像使用帮助
**注意: 本镜像是 AOSP 镜像，Android SDK因版权原因，我们不能提供镜像服务。**

参考 Google 教程 <https://source.android.com/source/downloading.html>，
将 `https://android.googlesource.com/` 全部使用 `https://aosp.tuna.tsinghua.edu.cn/` 代替即可。

- **2015-10-08 : 镜像地址更新为 https://aosp.tuna.tsinghua.edu.cn/ (结尾没有/android) **

### 过程摘录
(参考 https://lug.ustc.edu.cn/wiki/mirrors/help/aosp 编写)

下载 repo 工具:
```
mkdir ~/bin
PATH=~/bin:$PATH
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

建立工作目录:
```
mkdir WORKING_DIRECTORY
cd WORKING_DIRECTORY
```

初始化仓库:
```
repo init -u https://aosp.tuna.tsinghua.edu.cn/aosp/platform/manifest
## 如果提示无法连接到 gerrit.googlesource.com，可以编辑 ~/bin/repo，把 REPO_URL 一行替换成下面的：
## REPO_URL = 'https://gerrit-google.tuna.tsinghua.edu.cn/git-repo'
```

如果需要某个特定的 Android 版本([列表](https://source.android.com/source/build-numbers.html#source-code-tags-and-builds))：
```
repo init -u https://aosp.tuna.tsinghua.edu.cn/platform/manifest -b android-4.0.1_r1
```

同步源码树（以后只需执行这条命令来同步）：
```
repo sync
```


### 替换已有的 AOSP 源代码的 remote

如果你之前已经通过某种途径获得了 AOSP 的源码(或者你只是 init 这一步完成后)，
你希望以后通过 TUNA 同步 AOSP 部分的代码，只需要将
`.repo/manifest.xml` 把其中的 aosp 这个 remote 的 fetch 从
`https://android.googlesource.com` 改为 `https://aosp.tuna.tsinghua.edu.cn/`。
```diff
<manifest>

   <remote  name="aosp"
-           fetch="https://android.googlesource.com"
+           fetch="https://aosp.tuna.tsinghua.edu.cn"
            review="android-review.googlesource.com" />

   <remote  name="github"
```

**这个方法也可以用来在同步 Cyanogenmod 代码的时候从 TUNA 同步部分代码**

### FAQ

1. 镜像的是什么？

   - 对 https://android.googlesource.com/ 的反向代理

2. 为何不能通过浏览器访问？

   - 暂时没有 gitweb, 而且反正是 git bare 仓库，没有可以直接看到的内容。

3. 出现 `curl: (22) The requested URL returned error: 404 Not Found
Server does not provide clone.bundle; ignoring.` 怎么办？

   - 无视即可。