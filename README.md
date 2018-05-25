# Project Guidelines

These are some general rules of thumb to keep the project from becoming hard to handle once it gets big enough.

Anything that is not considered here, that you have doubts about or that you think should change please come and tell the programmers. You can be as angry as you see fit :)

## File & Folder Naming

To have a standard naming we will use [**PascalCase**](https://en.wikipedia.org/wiki/Camel_case) which basically tells us to write the name of a file with the first character of each word being a capital letter and without any spaces, underscores or punctuation. For example, an audio effect could be named **```HeavyBulletImpact.wav```**. Generally **```EveryFilenameShouldBeWrittenInThisFormat.extension```**.

Other important principles that should be followed are:

- Be as clear as you can. If the file has the model of a Remington shotgun call it ```Remington``` instead of ```Shotgun1```.
- Don't use version numbers or words, that means that you shouldn't add things like ```v1```, ```final``` or ```WIP``` to a filename.
- Avoid abbreviations where possible: use ```SmallRedHoverboard``` instead of ```SRHoverboard```.
- Use numbers only for files that are in a sequence and **start counting at 0**: Use them on things like ```Event0```, ```Event1```, ```Event2``` but not in ```Car0```, ```Car1```, ```Car2``` (try to identify these cars by what it makes them different).
- Put descriptors on the left, that is, use ```RedCar``` instead of ```CarRed```. If you want to easily find all the car models together, use a folder. In general, folders are for grouping, filenames are for identifying.
- For very specific things such as animations, it is ok to use a modifier at the end using something like an '**@**' or an underscore '**_**'. For example: Instead of ```JudgeDieAnimation``` use ```Judge@Death``` or for states of a button use ```Button_Active``` and ```Button_Inactive``` instead of something else.

## Folder Structure

In the root of the **```Assets```** folder we will have all the extensions, plugins or external files that require a specific folder structure to work (e.g. the Wwise folder needs to be at Assets/Wwise or other*wise* it won't work). Some of the files

- **```Extensions```**: All the third-party extensions/packages we might use should be here instead of at the root of the project.
- **```Plugins```**: Plug-ins that extend Unity's features. Generally these are native dynamic libraries in C or C++.
- **```ProjectAssets```**: This is the folder that contains all the assets that we made for the project. 
- **```Standard Assets```**: This is where Unity puts all of its standard assets.
- **```StreamingAssets```**: Assets to be loaded into the game as raw data, not using Unity's runtime importing system.


This will mainly refer to the structure of the **Assets/ProjectAssets** folder since there is where most if not all of the files to be created for this project will be added.

- **```DynamicAssets```**: Assets that are meant to be loaded by ```Resources.Load()```. If we load something from a server during runtime, it should also be loaded into a subfolder here.
  - **```Common```**: The dynamic assets that will be packed with the game.
    - **```Resources```**: Inside every folder in ```DynamicAssets``` there should be a ```resources``` folder that will make its contents available to dynamically load at runtime.
- **```Editor```**: Contains all the editor scripts.
- **```Scratchpad```**: Contains things that are not yet ready to include in the project or that are being tweaked/tested before adding them. To use this folder you  should be using a *subfolder with your name*.
- **```Scripts```**: All the scripts for the project. Inside they should be grouped in folders by their theme and functionality. E.g. the script that deals with the movement of the hoverboard could be in a ```hoverboard/``` or ```hoverboard/movement/``` folder.
- **```Shaders```**: Contains all the shader files that we might develop for the project.
- **```StaticAssets```**: Here we should place all of the assets that will be treated as static resources (Used directly into scenes). *This is probably the most relevant folder for non-programmers.* Also, the content if each of these folders should be organized by theme. That means that something like the models of a particular character should be in something like ```Models/Characters/ParticularCharacter/```. I think in general we all have an idea of where we should put stuff and when to group it in folders :D
  - **Animations**
  - **Effects**
  - **Models**
  - **Prefabs**
  - **Scenes**
  - **Sounds**
  - **Textures**

As mentioned, this is a structure that should change whenever the project requires it. Any suggestions that might make the job of someone in the team easier should be made sooner rather than later.

Also, this is not a hard structure, it is just to make our lives easier. When adding something to a folder like the ones on ```StaticAssets/``` feel free to try to organize it so it makes the most sense. E.g. it is not particularly critical to have a building model in something like ```/StaticAssets/Models/Buildings/Skyscrapers/``` or in  ```/StaticAssets/Models/City/``` as long as it is consistent and it makes sense.

### Folders Relevant for Artists

- **```ProjectAssets/StaticAssets/Animations```**
- **```ProjectAssets/StaticAssets/Models```**
- **```ProjectAssets/StaticAssets/Textures```**

### Folders Relevant for Designers

- **```ProjectAssets/StaticAssets/Prefabs```**
- **```ProjectAssets/StaticAssets/Scenes```**

### Folders Relevant for Audio

- **```ProjectAssets/StaticAssets/Sounds```**

## Coding Standards

In general we will use the standard [C# coding conventions defined by Microsoft](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions). But this is a general soft rule, when it makes sense feel free to stray from these.

Some particular notes that could be useful for us will be in the next subsections.

### TODOs, NOTEs and other annotations

To mark a section of the code with something relevant, the syntax to do so in a comment will be the following. Here ```name``` should have the name of the person who wrote it.

```cs
// @TODO(name): This is what needs to be done here
```

All of the possible annotations should be in this document so we can search for them in the whole project easily. That is, don't make your own ```@THIS_COULD_BREAK(Ruben)``` without telling the other programmers and adding that annotation type to this document.

#### Current Annotations

- ```// @TODO(name): Description of what needs to be done```
- ```// @NOTE(name): What you are annotating that people should have in mind when looking at the code```
- ```// @FIX(name): There is something wrong here, you try to explain what it is and what could be causing it```
- ```// @HACK(name): Marks that this is a hacky way to do something, why it is hacky and maybe what we could do to implement it correctly```
- ```// @DOING(name): Marks that you were working here but had to stop (went to work on some other part of the code, the working day was over, or some other thing). Describe here what you were doing and what you were planning to do to make it easier for yourself to come back.```

### Documenting Code

Code documentation should follow the usual [C# XML documentation](https://docs.microsoft.com/en-us/dotnet/csharp/codedoc). Feel free to use any of the supported tags if you think that is particularly relevant to your code. That is, in a method that is hard to understand it might be necessary to use ```<param>```,  ```<returns>``` or any other type of tag.

That said, since we don't want to significantly slow down development, the only required tag in classes and methods will be the **```<summary>```** tag. It only needs a brief sentence that explains that that class or methods is for. An example could be the following.

```cs
/// <summary>
/// The main class that deals with the flying movement of the hoverboard.
/// </summary>
public class HoverFlying : MonoBehaviour {

...

/// <summary>
/// Calculates the pitch that should be applyed to the hoverboard based on player input.
/// </summary>
private void CalculatePitch()
{
...
}

...

}
```

The common Unity methods such as the ones found in MonoBehaviour (```Update()```, ```Start()```, ```Awake()```, etc.) don't need to have this documenting tags unless they do something specific that should be pointed out.

## References

- http://developers.nravo.com/mastering-unity-project-folder-structure-level-2-assets-organization/#.WwFkt0gvz-g
- http://www.gamasutra.com/blogs/HermanTulleken/20160812/279100/50_Tips_and_Best_Practices_for_Unity_2016_Edition.php
- https://docs.unity3d.com/Manual/SpecialFolders.html
- https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/inside-a-program/coding-conventions
- https://docs.microsoft.com/en-us/dotnet/csharp/codedoc

