---
title: Introducing ros-helm
published: false
categories: projects
layout: post
---

As a big [spacemacs](https://www.spacemacs.org) fan, I was disappointed to find
that no [ROS](https://www.ros.org) layer existed. Further research led me to the
[rosemacs](https://wiki.ros.org/rosemacs) package. Rosemacs is a very complete
solution to combine the two tools, however it has some caveats. It is installed
through ROS instead of melpa, because it ships with some compiled common lisp
code. That means that even if you get the elisp code from the
[repo](https://github.com/code-iai/ros_emacs_utils) you will still get a warning
if you haven't compiled the common lisp code. Also, rosemacs doesn't leverage
the most recent tools in emacsland like
[helm](https://emacs-helm.github.io/helm/). It felt like I could reach
feature-parity with a lot less code by leveraging existing packages. Finally
rosemacs is not packaged for ROS Kinetic, but only for earlier versions.

Having very little experience coding in elisp, modifying rosemacs to suit my
needs felt daunting. I thought it would be easier to learn emacs by starting
this project from scratch instead of modifying existing code I could not
understand. So, as a way of teaching myself elisp and get the tools I wanted to
interact with ROS, I started working on [ros-helm](https://github.com/davidlandry93/ros-helm).

## Introducing ros-helm

![Animated gif of the ros-helm package](https://raw.githubusercontent.com/davidlandry93/ros-helm/master/doc/screencap.gif)

Ros-helm is an emacs package that interfaces ROS with helm. It allows you to
find things related to ROS such as launchfiles, nodes, services, and so on. All
of this is done through helm's very good search interface. A few other goodies
are included, such as facilities to launch ros processes from emacs, and various
tweaks to make ROS development easier. If you code for ROS in LISP you are still
better off with rosemacs.

## Introducing spaceros

On top of ros-helm, I also wrote a small spacemacs layer called
[spaceros](https://github.com/davidlandry93/spaceros). Its purpose is to
integrate the ros-helm package inside spacemacs with decent keybindings and
configuration. For the time being, it is not included in the actual spaceros
distribution, so you will have to install it as a custom layer.

I made a [screencast]() demoing the capacities of the layer.

Hopefully this is useful to other ROS developers out there!

/David
