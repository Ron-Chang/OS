```bash
ssh-keygen -t rsa -b 4096 -C "YourEmail"
```

__Hit `Retrun` few times unitl process done.__

```bash
eval "$(ssh-agent -s)"
```

```bash
ssh-add ~/.ssh/id_rsa
```

```bash
sudo apt-get install xclip
```

```bash
xclip -sel clip < ~/.ssh/id_rsa.pub
```
*This command made the file is cellected on your clipboard.*  

Login Github on browser  
Go to ![https://github.com/settings/ssh/new](https://github.com/settings/ssh/new)  
Named it on __Title__, and past it on __Key__  
Click __Add SSH key__  
