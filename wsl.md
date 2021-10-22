---
id: FxVKGX3z9TKjZwUrV85T6
title: Wsl
desc: ''
updated: 1634594094994
created: 1634593710025
---

# WSL Snippets

## Disabling/Improving `ls` folder highlighting

https://askubuntu.com/questions/466198/how-do-i-change-the-color-for-directories-with-ls-in-the-console

1. Open `.bashrc`
   - `nano ~/.bashrc`
1. Add this to the end:
   - `LS_COLORS=$LS_COLORS:'ow=1;34:' ; export LS_COLORS`
