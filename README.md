# LaTeX 

> <img src="https://i.loli.net/2021/02/14/uOl4JX8sBNw9a3V.png" alt="VS Code + LaTeX" style="zoom:25%;" />

## Install

- archLinux

```zsh
yay -S texlive-full
```

- 添加环境变量

<img src="https://i.loli.net/2021/02/13/T4IuDldRy5wAK6a.png" alt="image-20210213230531038" style="zoom:55%;" /> 

```zsh
# 方法
export TexMan="/opt/texlive/2021/texmf-dist/doc/man"
export TexInfo="/opt/texlive/2021/texmf-dist/doc/info"
export TexLive="/opt/texlive/2021/bin/x86_64-linux"

export MANPATH="$MANPATH:$TexMan"
export INFOPATH="$INFOPATH:$TexInfo"
export PATH="$PATH:$TexLive"
```



## 教程

- LaTex入门教程：https://liam.page/2014/09/08/latex-introduction/
- LaTex工作室：https://www.latexstudio.net/







## 模板

- lab

- 