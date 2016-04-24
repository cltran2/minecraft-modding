# Minecraft Modding

## Setup
+ download forge source/development kit 1.8 mdk from
http://files.minecraftforge.net

```
unzip forge-1.8-11.14.4.1577-mdk.zip forge-1.8
cd forge-1.8
```

+ Set up a forge workspace for eclipse
```
./gradlew setupDecompWorkspace eclipse
```

- Issue: OBJModel.java:617: error: cannot find symbol
> Solution: https://github.com/MinecraftForge/MinecraftForge/issues/2183#issuecomment-156540131

  - download vecmath-1.5.2.jar (originallly from http://www.java2s.com/Code/Jar/v/Downloadvecmathjar.htm)
  - place it in /Library/Java/Extensions/ so that it takes precedence over the OS X version provided in /System/Library/Java/Extensions/

    ```
    sudo cp vecmath-1.5.2.jar /Library/Java/Extensions/vecmath.jar
    ```

- Issue: open eclipse, launch client: Variable references empty selection: ${project_loc}
> Solution: in Package Explorer, select MDKExample > src/main/java

## Book
https://github.com/AdityaGupta1/minecraft-modding-book
