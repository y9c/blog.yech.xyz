title: ubuntu安装nodejs5
date: 2015-12-20 16:21:23
tags: [tech]
---

- 将nodejs添加到源

```bash
wget -qO- https://deb.nodesource.com/setup_5.x | sudo bash -
```

- 安装nodejs

```bash
sudo apt-get install --yes nodejs
```

---

```bash
node -v
```
V5.3.0

```bash
npm -v
```
3.5.1
