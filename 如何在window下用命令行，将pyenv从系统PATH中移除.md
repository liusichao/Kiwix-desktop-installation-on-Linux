# 如何在window下用命令行，将%USERPROFILE%\.pyenv\pyenv-win\bin和%USERPROFILE%\.pyenv\pyenv-win\shims从系统PATH中移除

## 在Windows系统中，可以通过命令行修改系统环境变量`PATH`来移除指定路径。以下是详细步骤：

---

### **方法一：使用`setx`临时修改（需重启或新终端生效）**
1. **查看当前PATH**  
   运行以下命令查看当前用户或系统的PATH值：
   ```cmd
   echo %PATH%
   ```
   或（系统级PATH）：
   ```cmd
   reg query "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v Path
   ```

2. **移除目标路径**  
   使用`setx`结合字符串替换（需谨慎操作，避免误删其他路径）：
   ```cmd
   :: 备份当前PATH（重要！）
   setx PATH_BACKUP "%PATH%"

   :: 移除用户级PATH中的目标路径（示例）
   for /f "tokens=1* delims=;" %%a in ("%PATH%") do (
       if "%%a" neq "%USERPROFILE%\.pyenv\pyenv-win\bin" (
           if "%%a" neq "%USERPROFILE%\.pyenv\pyenv-win\shims" (
               set "NEW_PATH=%%a"
               :loop
               if "%%b" neq "" (
                   set "NEXT=%%b"
                   for /f "tokens=1* delims=;" %%c in ("!NEXT!") do (
                       if "%%c" neq "%USERPROFILE%\.pyenv\pyenv-win\bin" (
                           if "%%c" neq "%USERPROFILE%\.pyenv\pyenv-win\shims" (
                               set "NEW_PATH=!NEW_PATH!;%%c"
                               set "NEXT=%%d"
                               goto loop
                           ) else (
                               set "NEXT=%%d"
                               goto loop
                           )
                       ) else (
                           set "NEXT=%%d"
                           goto loop
                       )
                   )
               )
           )
       )
   )
   :: 实际设置PATH（需启用延迟变量扩展）
   setlocal enabledelayedexpansion
   setx PATH "!NEW_PATH!"
   ```
   **问题**：上述批处理脚本复杂且易出错，推荐使用方法二。

---

### **方法二：通过PowerShell精确修改（推荐）**
1. **以管理员身份打开PowerShell**  
   右键点击“开始”菜单 → 选择“Windows PowerShell (管理员)”。

2. **获取当前PATH并移除目标路径**  
   运行以下脚本：
   ```powershell
   # 获取用户级PATH
   $userPath = [Environment]::GetEnvironmentVariable("PATH", "User")
   $paths = $userPath -split ";" | Where-Object {
       $_ -ne "$env:USERPROFILE\.pyenv\pyenv-win\bin" -and
       $_ -ne "$env:USERPROFILE\.pyenv\pyenv-win\shims"
   }
   $newPath = $paths -join ";"

   # 设置新的PATH
   [Environment]::SetEnvironmentVariable("PATH", $newPath, "User")
   ```

3. **验证修改**  
   重新打开命令行，运行：
   ```cmd
   echo %PATH%
   ```
   确认目标路径已消失。

---

### **方法三：手动通过图形界面修改**
1. **打开环境变量编辑器**  
   - 按 `Win + R`，输入 `sysdm.cpl` → 回车。
   - 切换到“高级”选项卡 → 点击“环境变量”。

2. **编辑用户变量中的PATH**  
   - 在“用户变量”列表中找到`PATH` → 点击“编辑”。
   - 手动删除以下两项：
     ```
     %USERPROFILE%\.pyenv\pyenv-win\bin
     %USERPROFILE%\.pyenv\pyenv-win\shims
     ```
   - 点击“确定”保存。

---

### **注意事项**
1. **备份PATH**  
   修改前建议备份当前PATH，避免误操作导致系统异常。
2. **作用范围**  
   - 用户级PATH：仅影响当前用户。
   - 系统级PATH：需管理员权限，影响所有用户（通过`[Environment]::SetEnvironmentVariable("PATH", $newPath, "Machine")`修改）。
3. **即时生效**  
   修改后需重启命令行或运行：
   ```cmd
   setx PATH "%PATH%"  # 强制刷新（不推荐，可能重复路径）
   ```
   更推荐直接重启终端。

---

### **总结**
- **推荐方法**：使用PowerShell脚本（方法二），安全且可精确控制。
- **备选方案**：手动图形界面操作（方法三），适合不熟悉脚本的用户。
- **避免方法**：直接使用`setx`拼接字符串（方法一），容易因路径含特殊字符导致失败。
