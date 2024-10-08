# GitLab Tutorial

GitLab企业版使用指南、Git项目开发、推送、维护规则。<br>

极狐🦊GitLab链接:<br>

```txt
https://jihulab.com/
```

极狐🦊GitLab官方文档:<br>

```txt
https://www.wolai.com/gwbHb4oY8juQEBGNv7GCCz
```

- [GitLab Tutorial](#gitlab-tutorial)
  - [为团队成员创建账号并分配权限:](#为团队成员创建账号并分配权限)
    - [设置权限:](#设置权限)
    - [2FA双因素认证(可选):](#2fa双因素认证可选)
    - [IP访问限制(可选):](#ip访问限制可选)
  - [项目隔离:](#项目隔离)
  - [导入外部项目操作方式:](#导入外部项目操作方式)
  - [定义受保护分支:](#定义受保护分支)
    - [GitLab中设置方式:](#gitlab中设置方式)
    - [受保护分支设置详解:](#受保护分支设置详解)
    - [合并请求的审批人设置:](#合并请求的审批人设置)
    - ["合并请求批准" 和 "合并请求的审批人设置":](#合并请求批准-和-合并请求的审批人设置)
    - [谁可以修改受保护的分支(受保护的分支的保护力度):](#谁可以修改受保护的分支受保护的分支的保护力度)
    - [删除受保护的分支:](#删除受保护的分支)
  - [分支命名规范:](#分支命名规范)
    - [分支命名示例:](#分支命名示例)
    - [注意点:](#注意点)
  - [修改 Git 项目中主分支的名称:](#修改-git-项目中主分支的名称)
    - [最后3条命令的解释：](#最后3条命令的解释)
  - [定义推送规则:](#定义推送规则)
  - [更改项目名称/路径:](#更改项目名称路径)
  - [分支开发工作流:](#分支开发工作流)
  - [代码质量审批:](#代码质量审批)
    - [代码注释:](#代码注释)
    - [单元测试:](#单元测试)


## 为团队成员创建账号并分配权限:

### 设置权限:

![](./docs/用户角色授权.jpg)

极狐GitLab SaaS 无需用户安装，注册即可开启云端使用。极狐作为服务的提供方，负责SaaS服务的高可用架构、灾备恢复等维护；用户为服务等消费者，**最高权限为群组所有者(Group Owner)**。<br>


### 2FA双因素认证(可选):

密码+扫码，防止密码泄漏后被恶意登录。<br>

![](./docs/何谓2FA.jpg)


### IP访问限制(可选):

限制只有公司内网IP地址或指定IP白名单，防止员工在其他地点访问GitLab。<br>

![](./docs/IP白名单.jpg)


## 项目隔离:

小程序(网页)部分、AI算法不同部门代码分离。不同项目组的人看不到其他项目组的代码。<br>


## 导入外部项目操作方式:

![](./docs/导入外部项目操作方式.png)

注意，只有权限大于等于维护者才有导入外部项目的许可。开发者没有这个权限。<br>

![](./docs/导入外部项目的权限.png)


## 定义受保护分支:

定义受保护分支，防止代码越权提交。<br>

![](./docs/受保护分支.jpg)

### GitLab中设置方式:

选择项目 --> 设置 --> 仓库，效果图如下:<br>

![](./docs/受保护分支设置界面.png)

### 受保护分支设置详解:

![](./docs/受保护分支设置详解.png)

1. **受保护分支 (Protected Branches)**：此设置用于保护某些分支，防止未授权的更改。保护分支可以限制哪些用户或角色可以推送、合并、更改或删除该分支。

2. **分支 (Branch)**：
   - **main**：这是当前正在被保护的分支。在GitLab中，默认的主要分支通常是 `main`。

3. **允许合并 (Allowed to merge)**：
   - **Maintainers**：只有具有Maintainer角色的用户可以将合并请求（Merge Requests）合并到此分支。这意味着普通开发者（Developers）提交的合并请求需要由Maintainers来审核和合并。

4. **允许推送和合并 (Allowed to push and merge)**：
   - **Maintainers**：只有具有Maintainer角色的用户可以直接推送代码或合并更改到此分支。此设置进一步确保只有经过授权的用户才能直接修改此分支。

5. **允许强制推送 (Allow force push)**：
   - **关闭 (Off)**：不允许任何用户强制推送到该分支。强制推送通常会绕过常规的推送限制，可能导致代码历史被改写，因此通常是不推荐和被禁止的。

6. **代码所有者批准 (Require Code Owner approval)**：
   - **关闭 (Off)**：不要求代码所有者批准。这一选项用于要求特定文件的所有者（根据 `CODEOWNERS` 文件）在合并前批准更改。

7. **取消保护 (Unprotect)**：
   - 这个按钮允许具有适当权限的用户取消对该分支的保护。取消保护后，该分支将不再受上述限制。

### 合并请求的审批人设置:

![](./docs/合并请求的审批人设置.png)

在“允许合并”选项中选择了某些用户，那么 **这些用户可以被指定为合并请求的审批人** ，其他开发者在提交合并请求时可以将请求指派给这些用户进行审核和合并。<br>

### "合并请求批准" 和 "合并请求的审批人设置":

如果合并审批的流程简单，可以只进行 "合并请求的审批人设置"。<br>

如果合并审批的流程复杂，例如需要多层、多人审批，需要创建 "合并请求批准"。<br>

"合并请求批准"的设置方式如下:<br>

![](./docs/"合并请求批准"的设置方式.png)

审批总流程可点击 **"设置 --> 仓库 --> 分支规则 --> 查看详情"** 查看，最终效果图如下:<br>

![](./docs/审批总流程查看.png)

### 谁可以修改受保护的分支(受保护的分支的保护力度):

![](./docs/谁可以修改受保护的分支.png)

### 删除受保护的分支:

![](./docs/删除受保护的分支.png)


## 分支命名规范:

规范的分支命名可以在多人合作时避免对他人造成干扰，同时方便追溯功能开发。以下为分支命名规范:<br>

```txt
格式: <类型>/<来源>/<成员名>/<日期>/<描述>
```

> [!TIP]
> 成员名可只使用缩写，例如 peilongchen --> plc。

1. **主分支**:
   - `main` 或 `master`: 主要分支，通常是项目的生产版本分支。

2. **开发分支**:
   - `develop`: 开发主分支，通常是集成所有开发工作的分支。

3. **功能分支** (Feature branches):
   - `feature/<功能描述>`: 用于开发新功能。示例：`feature/main/peilongchen/20240628/user-authentication`

4. **修复分支** (Bugfix branches):
   - `bugfix/<修复描述>`: 用于修复项目中的bug。示例：`bugfix/main/peilongchen/20240613/fix-login-issue`

5. **发布分支** (Release branches):
   - `release/<版本号>`: 用于准备发布的分支。示例：`release/peilongchen/20240611/1.0.0`

6. **热修复分支** (Hotfix branches):
   - `hotfix/<修复描述>`: 用于修复生产环境中的紧急问题。示例：`hotfix/develop/peilongchen/20240601/fix-critical-bug`

### 分支命名示例:

以下是一个示例结构，展示了如何根据不同的需求创建和命名分支：<br>

```log
main
develop
feature/main/peilongchen/20240628/user-authentication
feature/main/peilongchen/20240625/add-payment-gateway
bugfix/main/peilongchen/20240613/fix-login-issue
bugfix/main/peilongchen/20240611/fix-signup-validation
release/peilongchen/20240611/1.0.0
release/peilongchen/20240621/1.1.0
hotfix/develop/peilongchen/20240601/fix-critical-bug
```

### 注意点:

1. **保持一致性**: 确保团队中的所有成员遵循相同的命名规范，以便于分支的管理和查找。
2. **描述清晰**: 分支名应当清晰地描述分支的内容或目的，避免使用过于简短或模糊的名字。
3. **使用连字符**: 使用连字符（`-`）来分隔单词，使分支名更加易读。


## 修改 Git 项目中主分支的名称:

修改 Git 项目中主分支的名称可以按照以下步骤进行。假设当前主分支名称为 `master`，你想将其改为 `main`：<br>

1. **切换到要重命名的分支**:

打开终端，分支先切换到要重命名的分支。<br>

```bash
git checkout master
```

2. **重命名本地分支**：

打开终端或命令行工具，进入你的 Git 项目目录，并执行以下命令来重命名本地的 `master` 分支为 `main`：<br>

```bash
git branch -m master main
```

3. **删除远程的 `master` 分支**：

首先，推送新命名的 `main` 分支到远程仓库：<br>

> 因为执行的是改名，所以可以直接push。

```bash
git push origin main
```

然后，删除远程的 `master` 分支：<br>

> 🚨主分支默认是受保护的，如果想删除主分支，需要先将主分支切换为其他分支。

```bash
git push origin --delete master
```

4. **将新命名的 `main` 分支设为远程默认分支**：

在远程仓库（GitLab）的设置中，将默认分支改为 `main`。具体步骤如下：<br>

- 登录到远程仓库（GitLab）。
- 进入对应的项目。
- 点击设置-->仓库-->分支默认值。
- 在分支默认值选项中，将默认分支改为 `main`。
- 点击设置-->仓库-->受保护分支。
- 在受保护分支选项中，删除`master`分支的保护，添加`main`分支的保护。

5. **同步本地仓库与远程仓库**：

在本地执行以下命令，更新你的本地仓库以反映删除的远程 `master` 分支：<br>

```bash
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```

通过这些步骤，你就成功将 Git 项目的主分支从 `master` 改名为 `main` 了。<br>

### 最后3条命令的解释：

1. **`git fetch origin`**：

这条命令从远程仓库（这里是 `origin`）拉取所有分支的更新信息，但不会修改你的本地代码库。它只是更新本地的远程追踪分支的状态。<br>

```bash
git fetch origin
```

具体来说，它会从远程仓库获取分支信息、提交记录等，并在本地的 `.git` 目录中更新这些信息。<br>

2. **`git branch -u origin/main main`**：

这条命令用于设置本地分支 `main` 跟踪远程的 `main` 分支。<br>

```bash
git branch -u origin/main main
```

`-u` 是 `--set-upstream-to` 的缩写，它将本地的 `main` 分支与远程的 `main` 分支关联起来，以便你可以使用简化的 `git pull` 和 `git push` 命令，而不需要每次都指定远程分支。<br>

3. **`git remote set-head origin -a`**：

这条命令用于自动更新远程仓库（这里是 `origin`）的默认分支指向。<br>

```bash
git remote set-head origin -a
```

`set-head` 用于设置或更新远程仓库的默认分支。`-a` 参数表示自动检测远程仓库的默认分支，并在本地进行相应的更新。这样可以确保你本地仓库中的默认分支指向与远程仓库的一致。<br>

总结一下，这些命令的主要作用是：<br>

1. 更新本地仓库中的远程分支信息。
2. 将本地的 `main` 分支与远程的 `main` 分支关联起来。
3. 确保本地仓库中的默认分支指向与远程仓库一致。

这些步骤确保了你的本地仓库正确同步和配置远程仓库的分支结构，以便你能够顺利地进行后续的代码管理操作。<br>


## 定义推送规则:

![](./docs/定义推送规则.jpg)

`git commit` 的消息需简介、明了，禁止仅使用 "提交"、"修改" 等无意义消息。<br>


## 更改项目名称/路径:

在更改项目名称/路径方面，GitLab与GitHub略有不同。GitHub中如果更改了项目的名称，拉取的路径会同步更改，但GitLab需要多一步 **更改路径** 操作。示例如下:

假设你将项目名称由 `gradio_multi_turn` -更改为-> `guangyao_demo`，GitLab仓库图:

![](./docs/更改项目名称_1.png)

可以看到项目名称更改了，但项目的路径没有更改。

**更改路径方式**: 项目设置 --> 更改路径

![](./docs/更改项目名称_2.png)

效果:

![](./docs/更改项目名称_3.png)


## 分支开发工作流:

![](./docs/分支开发工作流.jpg)

合并分支时:<br>

1. 审批人需要先确定提交分支与主分支是否有冲突，如果有冲突，需要让提交人解决。

2. 代码审批，杜绝提交垃圾文件，冗余代码，无用代码，垃圾代码。防止主程序逻辑混乱，无关程序影响主程序耗时。


## 代码质量审批:

![](./docs/什么是代码质量.jpg)

尤其是项目解释型文档(`README.md`)、代码注释，如果不合格，审批不予以通过。<br>

### 代码注释:

代码注释风格可参考 [**google风格注释**](https://google.github.io/styleguide/pyguide.html) ，python代码的示例如下:<br>

```python
async def qa_rag_service(question):
    """qa问答对检索。
    Args:
        question(str): 用户输入。
    Returns:
        milvus_rtn(dict): 用户输入在milvus中匹配的top结果。
    """

    # 自己的代码

    return milvus_rtn
```

🚨 python 代码缩进统一使用4个空格。<br>

### 单元测试:

添加重要功能时，必须经过单元测试保证函数或功能完整实现。<br>

可以参考下列单元测试示例，也可以自定义测试方法，关键是保证添加的功能正常实现，不影响主程序运行。<br>

假设你有一个简单的函数 `add`，用于将两个数相加：<br>

```python
"""
Description: 实现add函数。
Notes: 
"""
# mymodule.py

def add(a, b):
    return a + b
```

可以在根目录下`tests`目录为这个函数编写一个单元测试：<br>

```python
"""
Description: 定义单元测试，测试add函数效果。
Notes: 
"""
# test_mymodule.py

import sys
import os

# 获取当前脚本的绝对路径
current_script_path = os.path.abspath(__file__)
# 获取当前脚本的父目录的父目录
parent_directory_of_the_parent_directory = os.path.dirname(os.path.dirname(current_script_path))
# 将这个目录添加到 sys.path
sys.path.append(parent_directory_of_the_parent_directory)

import unittest
from mymodule import add

class TestAddFunction(unittest.TestCase):
    def test_add(self):
        self.assertEqual(add(1, 2), 3)
        self.assertEqual(add(-1, 1), 0)
        self.assertEqual(add(0, 0), 0)

if __name__ == "__main__":
    unittest.main()
```

在这个例子中，`TestAddFunction` 是一个测试类，它继承自 `unittest.TestCase` 。`test_add` 方法是一个测试方法，用于验证 `add` 函数的输出是否符合预期。`self.assertEqual` 方法用于检查两个值是否相等。如果不相等，则测试失败。<br>

运行这个测试文件时，会自动执行所有测试方法，并报告测试结果：<br>

```bash
python test_mymodule.py
```

如果你的单元测试运行成功，没有发现任何问题。终端将输出类似以下内容：<br>

```markdown
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

1. `.`：表示一个测试用例成功通过。每个成功通过的测试用例在输出中都会显示一个点。
2. `Ran 1 test in 0.000s`：表示运行了一个测试用例，并且测试运行时间非常短（0.000秒）。
3. `OK`：表示所有测试用例都通过了，没有任何失败或错误。

这意味着你的`add`函数在测试用例中表现正确，返回了预期的结果。<br>


