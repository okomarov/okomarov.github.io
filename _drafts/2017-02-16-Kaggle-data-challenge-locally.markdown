---
layout:     post
title:      "Two Sigma Financial Modeling Challenge on Kaggle"
subtitle:   "running it locally in Windows on a Docker container"
date:       2017-02-16 16:32:00
author:     "Oleg Komarov"
header-img: "img/post-bg-01.png"
---

This is a story of hardhsips of software development in windows. Maybe one day I will have convinced myself that games are not worth over having a *nix OS. So far, I hit my head already a few times, and I might blog about it sometime, but here is another one of these sotires of fights. Or maybe one day ill meet a windows developer and he'll tell me how it's done, or maybe that dev is already staring at me in from the mirror. Anyways, here is a simple problem. 

To run the Two Sigma Financial Modeling Challenge locally on Windows 7, you will need the [Docker Toolbox v1.12.3](https://github.com/docker/toolbox/releases/tag/v1.12.3).[^1] After installing the toolbox, you can edit the properties of the Docker Quickstart Terminal shortcut to target the _[minnty](https://mintty.github.io/)_ console, because it is just so much better than _bash-git_ or _cmd.exe_ shells. Basically, simply paste this into the target of the shortcut:

    "C:\Program Files\Git\usr\bin\mintty.exe" -i "c:\Program Files\Docker Toolbox\docker-quickstart-terminal.ico" /usr/bin/bash --login -i  "c:\Program Files\Docker Toolbox\start.sh"

[^1]: Initially, the command to run a jupyter notebook from the container issued errors. Thinking it was a Win vs *nix path issue, I hacked into the command the option `-v "$(PWD)/wd"` instead of the correct `$(PWD):/wd`. The command executed but the Docker container did not list any content in the current folder. It turned out ot be a [bug](https://github.com/docker/toolbox/issues/607) in the recent version of the Docker Toolbox, and I had to revert to v1.12.3 to get things running smoothly. This cost me three days of sporadic attempts!

Once installed the toolbox, you will need [Kaggle's Python Docker container](https://github.com/Kaggle/docker-python) and their implementation of the [OpenAI's Gym](https://gym.openai.com/docs). Luckily, someone has done that for us and it is enough to clone [Gigles/kagglegym](https://github.com/Giqles/kagglegym) and execute the following instruction:

    winpty docker run --name=twosigma -it -v $(PWD):/wd -p 8888:8888 kagglegym jupyter notebook --port=8888 --ip=0.0.0.0
           docker run --name=twosigma -td -v $(PWD):/wd -p 8888:8888 kagglegym jupyter notebook --port=8888 --ip=0.0.0.0

Then to get the authentication token 

    docker exec peaceful_noyce jupyter notebook list 

- use winpty, kudos to [https://github.com/docker/toolbox/issues/323](https://github.com/docker/toolbox/issues/323)
- to launch jupyter notebook it's not localhost but the ip of the docker container (docker-machine ls), kudos to [https://www.kaggle.com/getting-started/19293#110742](https://www.kaggle.com/getting-started/19293#110742)

Do not run as -it (interactive) but as daemon -td, and name containter so that next time you don't lose your work!
[http://stackoverflow.com/questions/36756907/tensorflow-on-docker-how-to-save-the-work-on-jupyter-notebook](http://stackoverflow.com/questions/36756907/tensorflow-on-docker-how-to-save-the-work-on-jupyter-notebook)