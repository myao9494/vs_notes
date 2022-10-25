---
tags:
  - 01_チートシート
  - macbook
---

# homebrew

## インストール

```zsh
sudo mkdir /opt/homebrew
sudo chown -R $(whoami) /opt/homebrew
curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C /opt/homebrew
```

.zshrc に以下を追加すると、パスが通る

```zshrc
export PATH="/opt/homebrew/bin:$PATH"
```

インストールしたら、すべてを最新化

```zsh
brew upgrade
```

## 履歴

※ redis は sudo で実行する必要あり

```zsh
brew install gcc
brew install hwloc
brew install libevent
brew install open-mpi
brew install sphinx-doc
brew install cmake
brew install swig
brew install redis
brew install fceux
brew install tree
```
