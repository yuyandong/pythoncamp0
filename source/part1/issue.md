
##有多少折腾就有多少岔子
你不一定碰到这些岔路，我反正没少折腾，它们陪了多少年啊，都是菜鸟时光啊，啊青春小鸟不回来，那就记录吧。。。

### SSH key 啊你在哪里啊
-  使用本地终端 输入命令： sudo apt-get install git ，安装git
- 再者你已经创建了github帐号了，也知道哪里填SSHkey，只是还不知道key从哪里来，哪里来呢，本地终端告诉你：在我这里。
- 使用本地终端的SSH 命令 ：ssh -T git@github.com 尝试呼叫（链接） github 的ssh服务器，被拒绝（太苦了它告诉你）：Permission denied (publickey).
- 使用本地终端SSH 命令 ：ssh-keygen -C "yourname@yourcompany.com" -f ~/.ssh/github ，它能生成sshkey，被保存在~/.ssh/github.pub 里。
    - 还有两步要补上！
    - 输入终端命令：eval "$(ssh-agent -s)" 确保终端能使用生成的key;
    - 并使用终端命令： ssh-add ~/.ssh/github.pub 加载进本地文件
- 剩下的是笨方法：去本地打开主文件夹，打开隐藏文件夹~/.ssh，打开生成的 文件 ：~/.ssh/github.pub 中可以找打它。
- 按官方指导在网页github添加刚才复制出的sshkey 保存后，回到本地终端使用：ssh -T git@github.com 登录，按提示输入 yes 即可成功

- 参考：https://help.github.com/articles/generating-ssh-keys/
 
 
###别名：origin 啊你又是什么啊
2015-3-18
- 别名的问题，通过别名来指代库链接
	+ git remote add origin git@github.com:ARVN/omooc.py
	+ 其中origin 是git@fichu.com:ARVN/omooc.py 这个库链接的别名/。
- 别名可以任意制定，一个别名对应一个库
	+ git remote add gitbook https;//git.gitbook.com/arvn/omooc.py.git
	+ 其中gitbook 是URL https://git.gitbook.com/arvn/omooc.py.git 的别名 
	+ 而 git remote add origin git@github.com:ARVN/omooc.py 
	+ 其中origin 是git@fichu.com:ARVN/omooc.py 这个库链接的别名/。
- 别名在push/pull 时候减少输入的URL 的次数。
- 明白别名代表URL库的意义后，也减少误解的发生——免得在每次push的时候都遇到 repo不存在的错误显示

### 啊gitbook我的目录发布不了
2015-3-25
- 已经通过git 发布过gitbook；但因为操作的本地库，只有READMEN.md 和 SUMMARY.md 两个文件。
- 然后我在gitbook editor页面中添加了文件xxx.md 并完善进SUMMARY.md中
- 发现gitbook editor 页面无法发布gitbook——在我已经添加进SUMMAR.md中的文件都无法显示。
- 因为[xxx](xxx.md)路径都收录在目录 SUMMARY.md 中，我推测正常情况是应该出现在 图书[book- pythoncamp0](https://www.gitbook.com/book/arvn/pythoncamp0/details) “Table Of Contents”中，但是没有xxx.md的文件名显示
- 个人book- pythoncamp0页面上只显示了[introduction](README.md）。
-原来也是编译SUMMARY.md 的问题——在# summary 多了一个空格 。
-正确是#summary之下，无空格直接起一行

```sample：
  summary
[如有空格将引起错误](fault.md）

```
