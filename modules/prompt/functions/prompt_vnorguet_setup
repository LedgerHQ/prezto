#
# A (not so) simple theme that displays relevant, contextual information.
# This theme has 2 modes: Server and Desktop.
#
# Authors:
#   Inspired from 'sorin' theme
#   vnorguet <vincent.norguet@gmail.com>
#
#

# Load dependencies.
pmodload 'helper'

function prompt_vnorguet_pwd {
  local pwd="${PWD/#$HOME/~}"

  if [[ "$pwd" == (#m)[/~] ]]; then
    _prompt_vnorguet_pwd="$MATCH"
    unset MATCH
  else
    _prompt_vnorguet_pwd="${${${(@j:/:M)${(@s:/:)pwd}##.#?}:h}%/}/${pwd:t}"
  fi
}

function prompt_vnorguet_precmd {
  setopt LOCAL_OPTIONS
  unsetopt XTRACE KSH_ARRAYS

  # Format PWD.
  prompt_vnorguet_pwd

  # Get Git repository information.
  if (( $+functions[git-info] )); then
    git-info
  fi
  if (( $+functions[ruby-info] )); then
    ruby-info
  fi
}

function put_spacing() {
    local git=${git_info[prompt]}%
    if [ ${#git} != 0 ]; then
        ((git=${#git} - 10))
    else
        git=0
    fi
}

function prompt_vnorguet_setup {
  setopt LOCAL_OPTIONS
  unsetopt XTRACE KSH_ARRAYS
  prompt_opts=(cr percent subst)

  # Load required functions.
  autoload -Uz add-zsh-hook

  # Add hook for calling git-info before each command.
  add-zsh-hook precmd prompt_vnorguet_precmd

  # Set editor-info parameters.
  zstyle ':prezto:module:editor:info:completing' format '%B%F{red}...%f%b'
  zstyle ':prezto:module:editor:info:keymap:primary' format ' %B%F{red}❯%F{yellow}❯%F{green}❯%f%b'
  zstyle ':prezto:module:editor:info:keymap:primary:overwrite' format ' %F{red}♺%f'
  zstyle ':prezto:module:editor:info:keymap:alternate' format ' %B%F{green}❮%F{yellow}❮%F{red}❮%f%b'

  # Set git-info parameters.
  zstyle ':prezto:module:git:info' verbose 'yes'
  zstyle ':prezto:module:git:info:action' format ':%%B%F{yellow}%s%f%%b'
  zstyle ':prezto:module:git:info:added' format '%%B%F{green}+%f%%1b'
  zstyle ':prezto:module:git:info:ahead' format ' %%B%F{yellow}⬆%f%%b'
  zstyle ':prezto:module:git:info:behind' format ' %%B%F{yellow}⬇%f%%b'
  zstyle ':prezto:module:git:info:branch' format '%F{green}%b%f'
  zstyle ':prezto:module:git:info:commit' format '%F{yellow}%.7c%f'
  zstyle ':prezto:module:git:info:deleted' format '%%B%F{red}-%f%%b'
  zstyle ':prezto:module:git:info:modified' format '%F{green}%m%f'
  zstyle ':prezto:module:git:info:position' format ':%F{red}%p%f'
  zstyle ':prezto:module:git:info:renamed' format ' %%B%F{magenta}➜%f%%b'
  zstyle ':prezto:module:git:info:stashed' format ' %%B%F{cyan}✭%f%%b'
  zstyle ':prezto:module:git:info:unmerged' format '%%B%F{yellow}═%f%%b'
  zstyle ':prezto:module:git:info:untracked' format '%%B%F{white}◼%f%%b'
  zstyle ':prezto:module:git:info:keys' format \
    'prompt' '%F{green}[%f%b%F{green}]%f %c (%a%m/%d/%u/%U%%B)%%b' \
    'rprompt' ' '
 zstyle ':prezto:module:ruby:info:version' format '[%v]'

  PROMPT='%B%F{red}%m%f %F{white}[%~]%f$(put_spacing) ${git_info[prompt]}%b%F{blue}%f
%F{blue}->%B%F{blue} %#%f%b '

  PROMPT=$PROMPT

}

prompt_vnorguet_setup "$@"
