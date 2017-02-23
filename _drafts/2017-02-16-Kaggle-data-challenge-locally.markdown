---
layout:     post
title:      "Two Sigma Financial Modeling Challenge on Kaggle"
subtitle:   "running it locally in Windows on a Docker container"
date:       2017-02-16 16:32:00
author:     "Oleg Komarov"
header-img: "img/post-bg-01.png"
---
This is a story of hardhsips of software development in windows. Maybe one day I will have convinced myself that games are not worth over having a *nix OS. So far, I hit my head already a few times, and I might blog about it sometime, but here is another one of these sotires of fights. Or maybe one day ill meet a windows developer and he'll tell me how it's done, or maybe that dev is already staring at me in from the mirror. Anyways, here is a simple problem. 

To run the Two Sigma Financial Modeling Challenge locally on Windows 7 you will need the Docker Toolbox v1.12.3.[^1]

[^1]: The exact version is fundamental.

Once installed the toolbox, you will need [Kaggle's Python Docker container](https://github.com/Kaggle/docker-python) extended with their implementation of the [OpenAI's Gym](https://gym.openai.com/docs). Luckily, someone has done that for us and it is enough to clone [Gigles/kagglegym](https://github.com/Giqles/kagglegym) and execute instruction with caveats for:

    winpty docker run -it -v "$(pwd)/wd" -p 8888:8888 kagglegym jupyter notebook --port=8888 --ip=0.0.0.0
    docker run -td -v "$(PWD)/wd" -p 8888:8888 kagglegym jupyter notebook --port=8888 --ip=0.0.0.0

Then to get the authentication token 

    docker exec peaceful_noyce jupyter notebook list 

Can't see the current dir files! Found problem with docker toolbox: https://github.com/docker/toolbox/issues/607, downgrading to docker 1.12.3. Works!!!!!! FML took me 3 days.

- use winpty, kudos to https://github.com/docker/toolbox/issues/323
- the directory is "$(pwd)/wd" instead of $(pwd):/wd coz of...windows. I am starting to understand the :/ syntax, is to cat directories. Yet, need to figure out how to cat the pwd with wd in daemon style so that i can pwd where my notebook is, and make changes to the notebook and save it
- to launch jupyter notebook it's not localhost but the ip of the docker container (docker-machine ls), kudos to https://www.kaggle.com/getting-started/19293#110742

Do not run as -it (interactive) but as daemon -td, and name containter so that next time you don't lose your work!
http://stackoverflow.com/questions/36756907/tensorflow-on-docker-how-to-save-the-work-on-jupyter-notebook