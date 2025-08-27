# Cách Setup Terminal Đẹp (BASH + Oh My Bash)

## Bước 1: 

```bash
chsh -s $(which zsh)        # Đặt bash làm shell mặc định
```
## Bước 2: Cài Oh My Bash

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/ohmybash/oh-my-bash/master/tools/install.sh)"
```

## Bước 3: Cài theme terminal đẹp
Tạo file theme mới:

```bash
nano ~/.oh-my-bash/custom/themes/devcontainers/devcontainers.theme.sh
```

Paste:
```bash
# devcontainers.bash-theme for Oh My Bash

function __omb_theme_git_prompt() {
  if [ "$(git config --get devcontainers-theme.hide-status 2>/dev/null)" != 1 ] && \
     [ "$(git config --get codespaces-theme.hide-status 2>/dev/null)" != 1 ]; then

    local branch
    branch=$(git symbolic-ref --short HEAD 2>/dev/null || git rev-parse --short HEAD 2>/dev/null)
    if [[ -n "$branch" ]]; then
      local dirty=""
      if [ "$(git config --get devcontainers-theme.show-dirty 2>/dev/null)" = 1 ] && \
         git ls-files --error-unmatch -m --directory --no-empty-directory -o --exclude-standard ":/*" >/dev/null 2>&1; then
        dirty=" \e[1;33m✗"
      fi
      # Remove \[\] from inside echo
      echo -e "\e[1;36m(\e[1;31m${branch}${dirty}\e[1;36m)\e[0m "
    fi
  fi
}

# Prompt username
if [[ -n "${GITHUB_USER}" ]]; then
  __omb_prompt_user="@${GITHUB_USER}"
else
  __omb_prompt_user="\u"
fi

# Prompt symbol
__omb_prompt_symbol="\[\e[0m\]➜"

# Main prompt (PS1)
PS1="\[\e[32m\]${__omb_prompt_user} ${__omb_prompt_symbol} "
PS1+="\[\e[1;34m\]\w\[\e[0m\] "
PS1+='$( __omb_theme_git_prompt )'
PS1+="\[\e[37m\]\$ \[\e[0m\]"

# Optional: set terminal title if using xterm
case "$TERM" in
  xterm*|rxvt*)
    PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}: ${PWD}\007"'
    ;;
esac
```
## Bước 4: Sử dụng theme vừa tạo
```bash
nano ~/.bashrc
```

Tìm dòng và sửa:
```bash
OSH_THEME="devcontainers"
```

Đặt bash làm terminal mặc định trong VS Code
1. Mở VS Code.
2. Nhấn Ctrl + , để mở Settings.
3. Tìm: terminal.integrated.defaultProfile.linux
4. Chọn: bash
* Tips: là vào trong workspaces trên github rồi vào xem tệp custom theme sau đó copy và tạo ra cái của mình hehee

Refer: 
- https://thuanbui.me/len-doi-terminal-voi-zsh-va-oh-my-zsh/#ii-cai-dat-oh-my-zsh
- https://github.com/ohmyzsh/ohmybash
