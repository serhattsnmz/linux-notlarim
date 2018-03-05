# Bg, Fg, &, Ctrl-Z – 5 Examples to Manage Unix Background Jobs

When you execute a unix shell-script or command that takes a long time, you can run it as a background job.

In this article, let us review how to execute a job in the background, bring a job to the foreground, view all background jobs, and kill a background job.

## 1. Executing a background job
Appending an ampersand ( & ) to the command runs the job in the background.

For example, when you execute a find command that might take a lot time to execute, you can put it in the background as shown below. Following example finds all the files under root file system that changed within the last 24 hours.

```
# find / -ctime -1 > /tmp/changed-file-list.txt &
```

## 2. Sending the current foreground job to the background using CTRL-Z and bg command
You can send an already running foreground job to background as explained below:

- Press ‘CTRL+Z’ which will suspend the current foreground job.
- Execute bg to make that command to execute in background.

For example, if you’ve forgot to execute a job in a background, you don’t need to kill the current job and start a new background job. Instead, suspend the current job and put it in the background as shown below.

```
# find / -ctime -1 > /tmp/changed-file-list.txt

# [CTRL-Z]
[2]+  Stopped                 find / -ctime -1 > /tmp/changed-file-list.txt

# bg
```

## 3. View all the background jobs using jobs command
You can list out the background jobs with the command jobs. Sample output of jobs command is

```
# jobs
[1]   Running                 bash download-file.sh &
[2]-  Running                 evolution &
[3]+  Done                    nautilus .
```

## 4. Taking a job from the background to the foreground using fg command
You can bring a background job to the foreground using fg command. When executed without arguments, it will take the most recent background job to the foreground.

```
# fg
```

If you have multiple background ground jobs, and would want to bring a certain job to the foreground, execute jobs command which will show the job id and command.

In the following example, fg %1 will bring the job#1 (i.e download-file.sh) to the foreground.

```
# jobs
[1]   Running                 bash download-file.sh &
[2]-  Running                 evolution &
[3]+  Done                    nautilus .

# fg %1
```

## 5. Kill a specific background job using kill %
If you want to kill a specific background job use, kill %job-number. For example, to kill the job 2 use

```
# kill %2
```