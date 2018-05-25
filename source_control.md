# Source Control

## Quick Changes

For quick changes during development we would suggest the use of [Unity Collaborate][collab] since this is extremely simple and direct, especially for non programmers. Another advantage is that it makes dealing with source control much more transparent. This would also reduce the time and effort required to make one small change and have the other people currently developing see it quickly.

This would make it so the most common commits will be done with Unity Collaborate, and then significant changes will be pushed with Git to the appropriate branch. Another advantage of this is that the only commits in the Git repository will be much cleaner and significant. There wont be "changed prefab parameter for camera shake" commits in Git since those small changes will be shared with Collaborate. This makes the list of commits and what they change much easier to read and understand what they are for.

## Branching Strategy

For our branching strategy we propose the structure described here in the following sections. The main reasons are that is simple enough that it won't get in the way of development but also flexible enough to work with a larger project if or when required.

![Describing Branches][complete_branches]

### Main Branches

- **```master```**: The source in this branch always represents a *production-ready* state. This is where every change or feature should be ultimately integrated when it is ready and polished. This would directly relate to the finished iterations of the project or the "*release*" of a new version.
- **```development```**: Here is where the main development of the project will be done. The changes made during development will be pushed here and iterated upon until they are ready to get merged onto the ```master``` branch.


### Supporting Branches


- **Feature Branches** (e.g. ```new-feature```): Created when the creation of a new feature will potentially require big enough changes to significantly differ from the develop branch. These should branch off from ```development``` and merge back into ```development``` in every case. 
- **Release Branches** (e.g. ```release-0.1```): Before importante releases, a new *release* branch should branch off from ```development``` instead of just merging ```development``` to master. This allows to polish the release, focus on possible bugfixes, etc. while keeping the development branch active for other areas of development that are not related to the current release. When this branch represents a *production-ready* release it will be merged into both ```development``` and ```master```.
- **Hotfix Branches** (e.g. ```hotfix-movement-bug```): These shouldn't be necessary for the moment but it is always good to have them in mind. There branch off from ```master``` when a quick fix is required, like a bug in production code. When the fix has been applied it should be merged back into both ```master``` and ```development```. 

## Git Client

[**SourceTree**][sourcetree] is the one proposed by us (the programming team) since it simplifies the interaction with Git repositories and has very useful visualization features for the branches, commits, etc.

In some instances, some members of the team (especially the programmers) might use the command line for conveniency and control when doing something critical.

## Level Locking

Ideally every member of the team shouldn't be working on the same scene (or files in general). Unity Collaborate helps dealing with that since it understands the scene files better than Git (which just parses them as text). If conflicts happen in Unity files (or other ones) they are already set up to be represented as text so they can be merged without much trouble.

## Large Files

[**Git Large File Storage**][gitlfs] or ```git-lfs``` will be set up to deal with large files that have to be added to the repository, this is meant to avoid storing old versions of large files (e.g. large binaries) and instead just having pointers to those files that will be downloaded as required locally.

## References

- https://www.gamasutra.com/blogs/AlistairDoulin/20150304/237814/Git_for_Unity_Developers.php
- https://nvie.com/posts/a-successful-git-branching-model/
- https://www.gamasutra.com/blogs/TimPettersen/20161206/286981/The_complete_guide_to_Unity__Git.php

[complete_branches]: https://nvie.com/img/git-model@2x.png
[sourcetree]: https://www.sourcetreeapp.com/
[gitlfs]: https://git-lfs.github.com/
[collab]: https://unity3d.com/unity/features/collaborate
