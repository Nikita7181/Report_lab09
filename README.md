#           **Отчет Lab09**
##                *Report*
- `Ход работы`

- Были выплнены следующие команды

![Туториал](https://github.com/Nikita7181/lab09)

```
export GITHUB_TOKEN=мой токен
export GITHUB_USERNAME=Nikita7181
export PACKAGE_MANAGER=pacman
export GPG_PACKAGE_NAME=gpg
$PACKAGE_MANAGER install xclip
alias gsed=sed
alias pbcopy='xclip -selection clipboard'
alias pbpaste='xclip -selection clipboard -o'
cd ${GITHUB_USERNAME}/workspace
pushd .
source scripts/activate
go get github.com/aktau/github-release
git clone https://github.com/${GITHUB_USERNAME}/lab08 projects/lab09
cd projects/lab09
git remote remove origin
git remote add origin https://github.com/${GITHUB_USERNAME}/lab09
gsed -i 's/lab08/lab09/g' README.md
$PACKAGE_MANAGER install ${GPG_PACKAGE_NAME}
gpg --list-secret-keys --keyid-format LONG
gpg --full-generate-key
gpg --list-secret-keys --keyid-format LONG
gpg -K ${GITHUB_USERNAME}
GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
gpg --armor --export ${GPG_KEY_ID} | pbcopy
pbpaste
open https://github.com/settings/keys
git config user.signingkey ${GPG_SEC_KEY_ID}
git config gpg.program gpg
test -r ~/.bash_profile && echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile
echo 'export GPG_TTY=$(tty)' >> ~/.profile
cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
cmake --build _build --target package
travis login --auto
travis enable
git tag -s v0.1.0.0
git tag -v v0.1.0.0
git show v0.1.0.0
git push origin master --tags
github-release --version
github-release info -u ${GITHUB_USERNAME} -r lab09
github-release release \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "libprint" \
    --description "my first release"
export PACKAGE_OS=`uname -s` PACKAGE_ARCH=`uname -m` 
export PACKAGE_FILENAME=print-${PACKAGE_OS}-${PACKAGE_ARCH}.tar.gz
github-release upload \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "${PACKAGE_FILENAME}" \
    --file _build/*.tar.gz
github-release info -u ${GITHUB_USERNAME} -r lab09
wget https://github.com/${GITHUB_USERNAME}/lab09/releases/download/v0.1.0.0/${PACKAGE_FILENAME}
tar -ztf ${PACKAGE_FILENAME}
```

- Результат выполнения команд
  
![](https://raw.githubusercontent.com/Nikita7181/Report_lab09/master/Screenshots/1.png)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/2.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/3.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/4.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/5.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/6.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/7.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/8.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/9.png?raw=true)

![](https://github.com/Nikita7181/Report_lab09/blob/master/Screenshots/10.png?raw=true)

- После чего все было выгружено на Git hub

```
cd /home/nikita/Nikita7181/workspace/projects/Report_lab09
git add .
git commit -m "Complete tasks"
git push origin master
```
