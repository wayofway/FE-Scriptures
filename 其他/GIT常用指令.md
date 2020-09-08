# GIT常用指令

| 功能                                          | 指令                                                         |
| --------------------------------------------- | ------------------------------------------------------------ |
| 配置config                                    | git config user.name  "Administrator"                        |
|                                               | git config user.email "root@example.com"                     |
| clone项目                                     | git clone http://git.code.oa.com/group_path/project_path.git |
| 创建并切换分支                                | git checkout –b test(分支名）                                |
| 添加修改的文件到缓存区                        | git add 文件名                                               |
| 查看状态                                      | git status                                                   |
| 提交代码到本地仓库                            | git commit –m "描述信息"                                     |
| 查看历史                                      | git log                                                      |
| 拉取远程仓库最新代码                          | git pull origin test                                         |
| 推送代码到远程仓库                            | git push origin test                                         |
| 本地合并分支(合并前要切分支和拉最新代码)      | git checkout master                                          |
|                                               | git pull origin master                                       |
|                                               | git merge test                                               |
| 变基rebase合并（rebase后还要回到主分支merge） | git checkout test                                            |
|                                               | git rebase master                                            |
| 打tag，查看tag                                | git tag v1.0                                                 |
|                                               | git tag                                                      |
|                                               | git push origin v1.0                                         |
| 关联远程仓库                                  | cd existing_folder                                           |
|                                               | git init                                                     |
|                                               | git remote add origin url                                    |
|                                               | git add .                                                    |
|                                               | git commit -m "init"                                         |
|                                               | git push -u origin master                                    |
| 查看当前远程仓库地址                          | git remote –v                                                |
| http与ssh互转                                 | git remote set-url origin http://xxxxxxx.git                 |
|                                               | git remote set-url origin git@git.xxxxx.git                  |



