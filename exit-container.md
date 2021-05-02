### Exit a docker container from inside the container

Want to exit a docker container? You have several options to choose from.

You can either “detach” from the interactive session to leave your conainer running in the background, or you can exit it. Let’s look at both.

This is relevant if you have started your container with something like:

`docker run -it busybox sh`

And are currently in a shell session inside the container.

If you’re not sure whether you’re in a container - you can usually see it by the weird host name in the prompt if you are using bash, or by running `uname -a`. If the second “word” is a hash, you’re probably in a container session.

Just Stopping the Container

If you want to stop and exit the container, and are in an interactive, responsive shell - press ctrl+d to exit the session. You could as well type the exit command.

    `TL;DR: press ctrl+c then ctrl+d - that means, keep the ctrl key pressed, type a c, and let go of ctrl. Then the same with ctrl and d`.

If there’s a non-shell process running, the combination is `ctrl+c` to interrupt it. Then you can exit the shell, or the container might exit already.

#### But what if you want to keep the container running, but without occupying your terminal?
Keep Your Container Running In The Background

You can detach from an interactive Docker session without exiting the container. You “daemonize” the container. The effect will be, as if you had started it with the -d flag in the first place.

You have to use two combinations, one after the other: ctrl+p followed by ctrl+q. You turn interactive mode to daemon mode, which keeps the container running but frees up your terminal.

You can attach to it later using docker attach, if you need to interact with the container more.

#### An Alternative Workflow

If you start a container, and need to detach from it frequently, consider running it directly in the background, by starting it in “detached mode” with -d.

The same command from above would look like this:

`docker run -it -d busybox sh`

You can either attach to it, or run an exec-command, such as:

`docker exec -ti CONTAINER_ID bash`

The above will start a bash session in the same container, which is great for taking a look around if you need to and perform one-off maintenance tasks.

You can get the container id after executing the -d command, or you can look it up with docker ps.
