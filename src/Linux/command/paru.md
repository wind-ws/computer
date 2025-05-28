
```
export http_proxy=http://127.0.0.1:7890
export https_proxy=http://127.0.0.1:7890
yay 和 pacman 和 paru
    用yay代替pacman,两者差不多,也就是大部分 选项 一样,如果报错就用原命令
    yay 安装命令不需要加 sudo
    网址: https://www.cnblogs.com/arteches/articles/12468668.html
    常用:
        pacman -Syu         #对整个系统进行更新  (今日无事可做)
        pacman -Scc         #清理所有的缓存文件
        pacman -Ss          #在仓库中搜索含关键字的包
        yay -S              # 从 AUR 安装软件包 (==下载安装)
        pacman -Rs          #删除包，删除其所有没有被其他已安装软件包使用的依赖关系
        pacman -Qs          #搜索已安装的包
    pacman -Syu         #对整个系统进行更新
    pacman -Syy         #强制更新
    pacman -Ss          #在仓库中搜索含关键字的包
    pacman -Sw          #只下载包，不安装。
    pacman -Sc          #清理未安装的包文件,包文件位于 /var/cache/pacman/pkg/ 目录
    pacman -Scc         #清理所有的缓存文件
    pacman -Syudd       #使用 -dd跳过所有检测
    pacman -R           #只删除包，保存其全部已经安装的依赖关系
    pacman -Rs          #删除包，删除其所有没有被其他已安装软件包使用的依赖关系
    pacman -Rsc         #删除包，删除所有依赖这个软件包的程序
    pacman -Rd          #删除包，不检查依赖
    pacman -Qs          #搜索已安装的包
    pacman -Qi          #查询本地安装包的详细信息
    pacman -Ql          #列出该包的文件
    pacman -Qk          #检查软件包安装的文件是否都存在
    pacman -Ql          #要获取已安装软件包所包含文件的列表
    pacman -Fs          #按文件名查找软件库


```