---
tags:
  - base
---

# linux_mac

macOS でも WSL みたいな Linux 環境を手に入れる

https://qiita.com/chibiegg/items/eede37345f7058ce604d

## やったこと

```
brew install lima
brew tap knazarov/qemu-virgl
brew install qemu-virgl
brew unlink qemu
brew link qemu-virgl
```

ここでだめ、、、残念
