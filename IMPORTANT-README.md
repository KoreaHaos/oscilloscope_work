# Importan ToDo!

***problem***

After creating repository for my oscilloscope project, i tried to push it to GitHub. The Arduino and Processing runners are too big.

Here is the error encountered:



```bash
koreahaos:~/workspace/oscilloscope_work (master) $ git push --all
Username for 'https://github.com': koreahaos
Password for 'https://koreahaos@github.com': 
Counting objects: 18, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (18/18), 253.95 MiB | 1.43 MiB/s, done.
Total 18 (delta 0), reused 0 (delta 0)
remote: error: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: error: Trace: e321465cc432f214268bf9115d059902
remote: error: See http://git.io/iEPt8g for more information.
remote: error: File tools/linux/arduino-1.6.8-linux64-with_runner.tar.tgz is 140.36 MB; this exceeds GitHub's file size limit of 100.00 MB
remote: error: File tools/linux/processing-3.0.2-linux64-with_runner.tgz is 115.23 MB; this exceeds GitHub's file size limit of 100.00 MB
To https://github.com/KoreaHaos/oscilloscope_work.git
 ! [remote rejected] master -> master (pre-receive hook declined)
error: failed to push some refs to 'https://github.com/KoreaHaos/oscilloscope_work.git'
koreahaos:~/workspace/oscilloscope_work (master) $ 
```

***possible solutions***

1. Make the zip files smaller.
2. Figure out [Git Large File Storage](https://git-lfs.github.com)
3. Create scripts that setup the needed tools.
4. ?


Fix attempt #1

```bash
# This line runs a script it downloads.
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash

# Gets the install package for git lfs.
wget https://github.com/github/git-lfs/releases/download/v1.2.0/git-lfs-linux-amd64-1.2.0.tar.gz

# Unzip/decompress it.
tar -zxvf git-lfs-linux-amd64-1.2.0.tar.gz

# Move into the unzip/decompressed directory.
cd git-lfs-1.2.0/

# Install it.
sudo bash install.sh

cd ..
cd oscilloscope_work/
git lfs track "*.tar.tgz"

git add .
git commit -m 'Figuring out git lfs.'
git push origin master
```
