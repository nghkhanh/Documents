# Cách Setup Terminal Đẹp (ZSH + Oh My Zsh)

## Bước 1: Cài `zsh`

```bash
sudo apt install zsh -y         # Dành cho Ubuntu / WSL
chsh -s $(which zsh)            # Đặt zsh làm shell mặc định
```
## Bước 2: Cài Oh My Zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## Bước 3: Cài Plugin

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

## Bước 4: Chỉnh sửa file cấu hình ~/.zshrc

```bash
nano ~/.zshrc
```
Tìm dòng plugins= và chỉnh sửa như sau:

```bash
plugins=(
  git
  docker
  docker-compose
  history
  rsync
  safe-paste
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```
## Bước 5: Cài theme terminal đẹp
Tạo file theme mới:

```bash
nano ~/.oh-my-zsh/custom/themes/devcontainers.zsh-theme
```

Paste:
```bash
# Oh My Zsh! theme - partly inspired by robbyrussell theme
__zsh_prompt() {
    local prompt_username
    if [ ! -z "${GITHUB_USER}" ]; then
        prompt_username="@${GITHUB_USER}"
    else
        prompt_username="%n"
    fi
    PROMPT="%{$fg[green]%}${prompt_username} %(?:%{$reset_color%}➜ :%{$fg_bold[red]%}➜ )"
    PROMPT+='%{$fg_bold[blue]%}%(5~|%-1~/…/%3~|%4~)%{$reset_color%} '
    PROMPT+='`\
        if [ "$(git config --get devcontainers-theme.hide-status 2>/dev/null)" != 1 ] && [ "$(git config --get codespaces-theme.hide-status 2>/dev/null)" != 1 ]; then \
            export BRANCH=$(git --no-optional-locks symbolic-ref --short HEAD 2>/dev/null || git --no-optional-locks rev-parse --short HEAD 2>/dev/null); \
            if [ "${BRANCH}" != "" ]; then \
                echo -n "%{$fg_bold[cyan]%}(%{$fg_bold[red]%}${BRANCH}" \
                && if [ "$(git config --get devcontainers-theme.show-dirty 2>/dev/null)" = 1 ] && \
                    git --no-optional-locks ls-files --error-unmatch -m --directory --no-empty-directory -o --exclude-standard ":/*" > /dev/null 2>&1; then \
                        echo -n " %{$fg_bold[yellow]%}✗"; \
                fi \
                && echo -n "%{$fg_bold[cyan]%})%{$reset_color%} "; \
            fi; \
        fi`'
    PROMPT+='%{$fg[white]%}$ %{$reset_color%}'
    unset -f __zsh_prompt
}
__zsh_prompt

# Check if the terminal is xterm
if [[ "$TERM" == "xterm" ]]; then
    preexec() {
        local cmd=${1}
        echo -ne "\033]0;${USER}@${HOSTNAME}: ${cmd}\007"
    }

    precmd() {
        echo -ne "\033]0;${USER}@${HOSTNAME}: ${SHELL}\007"
    }

    autoload -Uz add-zsh-hook
    add-zsh-hook preexec preexec
    add-zsh-hook precmd precmd
fi
```
## Bước 6: Sử dụng theme vừa tạo
```bash
nano ~/.zshrc
```

Tìm dòng và sửa:
```bash
ZSH_THEME="devcontainers"
```

🎯 Tuỳ chọn: Đặt zsh làm terminal mặc định trong VS Code
1. Mở VS Code.
2. Nhấn Ctrl + , để mở Settings.
3. Tìm: terminal.integrated.defaultProfile.linux
4. Chọn: zsh
* Tips: là vào trong workspaces trên github rồi vào xem tệp custom theme sau đó copy và tạo ra cái của mình hehe

