## create formula
To create or edit formulae locally, you’ll need to first tap homebrew/core if you haven’t previously.
```sh
HOMEBREW_NO_INSTALL_FROM_API=1 brew tap homebrew/core
```
grab the URL 
```sh
brew create https://github.com/ericwq/aprilsh/archive/refs/tags/0.6.40.tar.gz
```
update formula definition
```sh
cd ~/dev/aprilsh/homebrew
cp aprilsh.rb /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core/Formula/a/aprilsh.rb
```
build and install formula
```sh
HOMEBREW_NO_INSTALL_FROM_API=1 brew install --build-from-source --verbose --debug aprilsh
```
uninstall aprilsh
```sh
brew uninstall aprilsh
```
audit the formula
```sh
brew audit --strict --online aprilsh
brew audit --new --formula aprilsh
```
The second audit reports, That's why we need to create a new tap instead of commit to homebrew default tap:
```
qiwang@Qi15Pro homebrew % brew audit --new --formula aprilsh
aprilsh
  * GitHub repository not notable enough (<30 forks, <30 watchers and <75 stars)
Error: 1 problem in 1 formula detected.
qiwang@Qi15Pro homebrew %
```
## create tap
run the following command to create new tap.
```sh
qiwang@Qi15Pro homebrew-utils % brew tap-new --verbose --debug ericwq/aprilsh
git -c init.defaultBranch=main init
Initialized empty Git repository in /usr/local/Homebrew/Library/Taps/ericwq/homebrew-aprilsh/.git/
git add --all
git commit -m Create ericwq/aprilsh tap
[main (root-commit) 317a392] Create ericwq/aprilsh tap
 3 files changed, 90 insertions(+)
 create mode 100644 .github/workflows/publish.yml
 create mode 100644 .github/workflows/tests.yml
 create mode 100644 README.md
git branch -m main
==> Created ericwq/aprilsh
/usr/local/Homebrew/Library/Taps/ericwq/homebrew-aprilsh

When a pull request making changes to a formula (or formulae) becomes green
(all checks passed), then you can publish the built bottles.
To do so, label your PR as `pr-pull` and the workflow will be triggered.

```
create a new git repository and clone it to local host.
```sh
ide@openrc-nvide:~/proj $ git clone https://github.com/ericwq/homebrew-utils
Cloning into 'homebrew-utils'...
remote: Enumerating objects: 17, done.
remote: Counting objects: 100% (17/17), done.
remote: Compressing objects: 100% (12/12), done.
remote: Total 17 (delta 3), reused 12 (delta 2), pack-reused 0
Receiving objects: 100% (17/17), 5.24 KiB | 5.24 MiB/s, done.
Resolving deltas: 100% (3/3), done.
ide@openrc-nvide:~/proj
```
copy the content from `ericwq/homebrew-aprilsh` to `ericwq/homebrew-utils`, Note the repository's name start with `homebrew-` so the short `brew tap` command can be used.  
```sh
cd /usr/local/Homebrew/Library/Taps/ericwq/homebrew-aprilsh/
cp -r .github/ ~/proj/homebrew-utils/
cp -r Formula/ ~/proj/homebrew-utils/
```
put the aprilsh.rb into Formula.
```sh
cp aprilsh.rb ~/proj/Formula/
```
## install aprilsh for macos
check the existing taps.
```sh
qiwang@Qi15Pro ericwq % brew tap
ericwq/utils
homebrew/cask-fonts
homebrew/core
wez/wezterm
```
`brew install ericwq/utils/<formula>` Or `brew tap ericwq/utils` and then `brew install <formula>`.

```sh
brew tap ericwq/utils
brew install aprilsh
```
