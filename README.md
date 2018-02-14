# Git101

* Creating a repository
* Gathering, adding and commenting code
* Handle branches
* Stashing
* Handle conflicts

## Creating a repo
### From Github
* Open your profile
* Go to `Repository`
* Click on `New`
* Specify a name for you project, for example `MyProject`
* You can also set a README or a licence. To choose them see this [markdown guide](https://guides.github.com/features/mastering-markdown/) or [this guide](https://choosealicense.com) to choose your licence 
* Finally, use `git clone https://github.com/username/MyProject.git` to clone your project in your folder

### From existing sources
Considering the following:
```shell
~$ mkdir MyProject
~$ cd MyProject
~$ touch myCode.py
~$ echo "print('Hello World !')" > myCode.py
```
To add your super project `MyProject`
Create the remote repository: `https://github.com/username/MyProject.git`
Then
```shell
~$ cd MyProject
~$ git init
~$ git pull https://github.com/username/MyProject.git
~$ git add .
~$ git commit -m "Your commit message"
~$ git remote add origin https://github.com/username/MyProject.git
~$ git pull origin master
~$ git push origin master
```

## Properly gather, add and comment code
Time to add some code to this project !
```shell
~$ cp ~/MyCodeFiles/aVeryComplexCode.py ./
~$ git pull
~$ git add aVeryComplexCode.py
~$ git commit -m 'added my complex code'
~$ rm myCode.py
~$ git rm myCode.py
~$ git commit -m 'added my complex code'
~$ git push
```
* `git pull`
gather modification from origin
* `git commit -m "message"`
Allows you to to comment your modifications
* `git push`
Push your modifications to your branch

## Creating, navigating through and deleting branched
You now have a main branch with enough features, let's create another branch for development
```shell
~$ git checkout -b dev_branch
```
Now change branch and push it
```shell
~$ git checkout dev_branch
~$ git push origin branch
```
You can now list all your branches and see updates
```shell
~$ git branch
* dev_branch
  master
```
Merge master into your branch, add modifications and push it to master
```shell
~$ git merge master
~$ touch NewCode.py
~$ echo "print('Another print')" > NewCode.py
~$ git add newCode.py
~$ git commit -m "Added another source file"
~$ git push
~$ git checkout master
~$ git merge dev_branch
```
Now your branch is merged, you can safely delete it
```shell
~$ git push -d origin dev_branch
~$ git branch -d dev_branch
```

## Stashing your modifications
```shell
~$ git stash
~$ work...
~$ git stash pop
```

## Handle conflicts
Oups! Something went wrong!
```shell
~$ git pull
CONFLICT (content): Merge conflict in code_file.py
Automatic merge failed; fix conflicts and then commit the result.
```
### Resolving it "by hand"
Your file will look like something like this
```python
<<<<<<< HEAD:mergetest
print ("Hello World !")
=======
print ("Hello Me .")
>>>>>>> commit_id:mergetest
```
* `<<<<` marks the start of the conflict
* `====` marks the limit between comparaison
* `>>>>` marks the end of the conflict
You can delete by yourself the part you don't want to keep, and also delete `>>>>`, `====` and `>>>>` symbols.

For examle, you can edit it and keep:
```python
print ("Hello World !")
```
And then add, commit and push without any problem !

### Resolving it using git tools
Another way to solve it is by comparing the modification and add the one you want. In this example, I'm saving my modification using `--ours` but you can keep their code using `--theirs`
```bash
~$ git mergetool
~$ git checkout --ours code_file.py
~$ git add code_file.py
~$ git commit -m "Resolved conflict by keeping my modifications"
~$ git pull
```
