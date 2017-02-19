---
layout:     post
title:      "Two Sigma Financial Modeling Challenge on Kaggle"
subtitle:   "running it locally in Windows on a Docker container"
date:       2017-02-16 16:32:00
author:     "Oleg Komarov"
header-img: "img/post-bg-01.png"
---
This is a story of hardhsips of software development in windows. Maybe one day I will have convinced myself that games are not worth over having a *nix OS. So far, I hit my head already a few times, and I might blog about it sometime, but here is another one of these sotires of fights. Or maybe one day ill meet a windows developer and he'll tell me how it's done, or maybe that dev is already staring at me in from the mirror. Anyways, here is a simple problem. 

To run kaggle data challenge with kaggle gym locally

clone https://github.com/Giqles/kagglegym and execute instruction with caveats for:

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

<p>Never in all their history have men been able truly to conceive of the world as one: a single sphere, a globe, having the qualities of a globe, a round earth in which all the directions eventually meet, in which there is no center because every point, or none, is center — an equal earth which all men occupy as equals. The airman's earth, if free men make it, will be truly round: a globe in practice, not in theory.</p>

<p>Science cuts two ways, of course; its products can be used for both good and evil. But there's no turning back from science. The early warnings about technological dangers also come from science.</p>

<p>What was most significant about the lunar voyage was not that man set foot on the Moon but that they set eye on the earth.</p>

<p>A Chinese tale tells of some men sent to harm a young girl who, upon seeing her beauty, become her protectors rather than her violators. That's how I felt seeing the Earth for the first time. I could not help but love and cherish her.</p>

<p>For those who have seen the Earth from space, and for the hundreds and perhaps thousands more who will, the experience most certainly changes your perspective. The things that we share in our world are far more valuable than those which divide us.</p>

<h2 class="section-heading">The Final Frontier</h2>

<p>There can be no thought of finishing for ‘aiming for the stars.’ Both figuratively and literally, it is a task to occupy the generations. And no matter how much progress one makes, there is always the thrill of just beginning.</p>

<p>There can be no thought of finishing for ‘aiming for the stars.’ Both figuratively and literally, it is a task to occupy the generations. And no matter how much progress one makes, there is always the thrill of just beginning.</p>

<blockquote>The dreams of yesterday are the hopes of today and the reality of tomorrow. Science has not yet mastered prophecy. We predict too much for the next year and yet far too little for the next ten.</blockquote>

<p>Spaceflights cannot be stopped. This is not the work of any one man or even a group of men. It is a historical process which mankind is carrying out in accordance with the natural laws of human development.</p>

<h2 class="section-heading">Reaching for the Stars</h2>

<p>As we got further and further away, it [the Earth] diminished in size. Finally it shrank to the size of a marble, the most beautiful you can imagine. That beautiful, warm, living object looked so fragile, so delicate, that if you touched it with a finger it would crumble and fall apart. Seeing this has to change a man.</p>

<a href="#">
    <img src="{{ site.baseurl }}/img/post-sample-image.jpg" alt="Post Sample Image">
</a>
<span class="caption text-muted">To go places and do things that have never been done before – that’s what living is all about.</span>

<p>Space, the final frontier. These are the voyages of the Starship Enterprise. Its five-year mission: to explore strange new worlds, to seek out new life and new civilizations, to boldly go where no man has gone before.</p>

<p>As I stand out here in the wonders of the unknown at Hadley, I sort of realize there’s a fundamental truth to our nature, Man must explore, and this is exploration at its greatest.</p>

<p>Placeholder text by <a href="http://spaceipsum.com/">Space Ipsum</a>. Photographs by <a href="https://www.flickr.com/photos/nasacommons/">NASA on The Commons</a>.</p>
