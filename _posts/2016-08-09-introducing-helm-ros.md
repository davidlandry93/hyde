---
title: Introducing helm-ros
published: true
categories: projects
layout: post
---

As a huge [spacemacs](https://www.spacemacs.org) fan, I was disappointed when I
realized that no layer existed to interact with [ROS](htps://www.ros.org). There
*is* an Emacs package out there called [rosemacs](https://wiki.ros.org/rosemacs)
that solves part of that problem. However that package has some caveats. First
it cannot be shipped through [melpa](http://www.melpa.org). `rosemacs` contains
some Common LISP code that has to be compiled beforehand. For that reason this
package has to be shipped through ROS repositories, and it keeps us from
installing the package automatically from a `.emacs` or `.spacemacs` file. Also,
`rosemacs` does not leverage some of the modern tools in emacsland, like
[helm](https://emacs-helm.github.io/helm/). I feel that we could provide a good
subset of the features of `rosemacs` with a lot less code because of that.
Finally `rosemacs` was packaged with ROS indigo and jade, but not kinetic,
which casts some doubt about the status of the project.

At this point, the correct reaction would have been to fork `rosemacs` and fix
some of these problems. However I had very little experience in elisp at the time.
As a way of teaching myself to code in elisp and get the tools I wanted to interact
with ROS, I began working on [helm-ros](https://github.com/davidlandry93/helm-ros).

`helm-ros` is an emacs package that interfaces ROS with helm. It allows you to find
things related to ROS such as launchfiles, nodes, services, and so on. All of this 
is done through helm's search interface. A few other goodies are included, like 
shortcuts to start ROS processes. It is available through melpa.

![Animated gif of the helm-ros package](https://raw.githubusercontent.com/davidlandry93/helm-ros/master/doc/screencap.gif)

This package is still in early development. My objective is to write a spacemacs
layer once `helm-ros` is a bit more mature. In the meantime, I hope this is useful
to some ROS developers out there!

/David
